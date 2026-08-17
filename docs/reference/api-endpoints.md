# Endpoint dan Format Data

## Ringkasan Endpoint

Hostname konkret ditentukan oleh deployment dan sengaja tidak ditulis pada dokumentasi publik.

| Layanan | Koneksi | Path / antarmuka | Autentikasi |
| --- | --- | --- | --- |
| STT | WSS | `/ws/audio` | Header token saat handshake |
| n8n voice webhook | HTTPS | `/api/smartlab-voice` atau path webhook aktif | Header token webhook |
| SLM lokal | HTTPS/HTTP internal | OpenAI-compatible chat/completions | Bearer token |
| Piper TTS | HTTPS/HTTP internal | `/synthesize` | Bearer token terpisah |
| Home Assistant | HTTPS | `/api/states` dan service API | Long-lived credential di n8n |

## WebSocket STT

### Perangkat ke Server

Audio dikirim sebagai frame biner PCM mono 16 kHz signed 16-bit little-endian.

### Server ke Perangkat

| Pesan | Makna |
| --- | --- |
| `PROCESSING` | Server mendeteksi pengguna selesai berbicara dan mulai memproses audio |
| `AI_REPLY:<text>` | Respons akhir tersedia |

Koneksi tanpa token valid harus ditolak pada handshake.

## Webhook Perintah Suara

Contoh body konseptual:

```json
{
  "query": "ruangan terasa panas"
}
```

Respons alur n8n berisi teks akhir dan informasi eksekusi yang aman untuk dikirim kembali. Perangkat klien hanya menggunakan field yang telah didokumentasikan.

## SLM Lokal

Permintaan mengikuti format OpenAI-compatible dan memuat:

- `messages` berisi konteks sistem dan perintah pengguna.
- `tools` berisi empat fungsi SmartLab.
- Batas keluaran pendek dan pengaturan konsisten untuk evaluasi.

Contoh pemanggilan fungsi:

```json
{
  "name": "HassSetTemperature",
  "arguments": {
    "name": "climate.allowed_ac",
    "temperature": 20
  }
}
```

Identitas perangkat pada contoh bukan entitas produksi.

## Piper TTS

Permintaan membawa teks akhir yang telah diperiksa. Respons yang benar berupa audio WAV yang tidak kosong. TTS tidak memiliki akses untuk memanggil Home Assistant.

## Home Assistant

n8n membaca status perangkat, lalu memanggil layanan setelah hasil model lolos pemeriksaan. Kredensial Home Assistant tidak pernah dikirim kepada SLM atau perangkat suara.

## Respons Kesalahan

| Status | Makna umum | Respons client |
| --- | --- | --- |
| `400` | Data tidak valid | Perbaiki format; jangan kirim ulang tanpa perubahan |
| `401/403` | Autentikasi gagal | Hentikan permintaan dan periksa token layanan |
| `404` | Path tidak tersedia | Pastikan endpoint yang digunakan aktif |
| `413` | Permintaan terlalu besar | Kurangi ukuran data atau audio |
| `429` | Terlalu banyak permintaan | Tunggu sebelum mencoba kembali dan jangan mengulang aktuasi |
| `5xx` | Layanan mengalami gangguan | Hentikan aktuasi dan catat `trace_id` |
