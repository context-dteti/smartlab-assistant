# Endpoint dan Kontrak

## Ringkasan endpoint

Hostname konkret ditentukan oleh deployment dan sengaja tidak ditulis pada dokumentasi publik.

| Layanan | Transport | Path / interface | Authentication |
| --- | --- | --- | --- |
| STT | WSS | `/ws/audio` | Header token saat handshake |
| n8n voice webhook | HTTPS | `/api/smartlab-voice` atau path webhook aktif | Header token webhook |
| Local SLM | HTTPS/HTTP internal | OpenAI-compatible chat/completions | Bearer token |
| Piper TTS | HTTPS/HTTP internal | `/synthesize` | Bearer token terpisah |
| Home Assistant | HTTPS | `/api/states` dan service API | Long-lived credential di n8n |

## STT WebSocket

### Client ke server

Audio dikirim sebagai frame biner PCM mono 16 kHz signed 16-bit little-endian.

### Server ke client

| Pesan | Makna |
| --- | --- |
| `PROCESSING` | Server mendeteksi akhir utterance dan mulai transkripsi/inference |
| `AI_REPLY:<text>` | Respons akhir tersedia |

Koneksi tanpa token valid harus ditolak pada handshake.

## Voice webhook

Contoh body konseptual:

```json
{
  "query": "ruangan terasa panas"
}
```

Respons workflow berisi teks final dan metadata eksekusi yang telah disanitasi. Nama field produksi dapat berkembang; client tidak boleh mengandalkan nilai internal yang tidak didokumentasikan.

## Local SLM

Request mengikuti kontrak OpenAI-compatible dan memuat:

- `messages` dengan system context dan query.
- `tools` berisi empat native function tool.
- Batas output pendek dan decoding deterministik untuk evaluasi.

Contoh tool call konseptual:

```json
{
  "name": "HassSetTemperature",
  "arguments": {
    "name": "climate.allowed_ac",
    "temperature": 20
  }
}
```

Identifier contoh bukan entity produksi.

## Piper TTS

Request membawa teks final yang telah disanitasi. Respons sehat menggunakan media type audio dan body WAV non-empty. TTS tidak memiliki wewenang untuk memanggil Home Assistant.

## Home Assistant

n8n membaca state lalu memanggil service hanya setelah proposal melewati validator. Credential Home Assistant tidak pernah dikirim kepada SLM atau voice satellite.

## Respons error

| Status | Makna umum | Respons client |
| --- | --- | --- |
| `400` | Payload tidak valid | Perbaiki format; jangan retry tanpa perubahan |
| `401/403` | Authentication gagal | Hentikan request dan periksa secret injection |
| `404` | Path tidak tersedia | Verifikasi endpoint aktif |
| `413` | Request terlalu besar | Kurangi payload/audio |
| `429` | Rate limit | Backoff tanpa mengulang aktuasi |
| `5xx` | Service gagal | Fail closed dan catat trace |
