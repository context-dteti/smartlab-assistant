# Speech-to-Text

## Peran Layanan

Layanan Speech-to-Text menerima potongan audio PCM dari Raspberry Pi, mendeteksi akhir ucapan, mengubah ucapan Bahasa Indonesia menjadi teks, lalu meneruskannya ke n8n.

## Konfigurasi Utama

| Bagian | Implementasi |
| --- | --- |
| Model | Whisper Small Bahasa Indonesia |
| Runtime | CTranslate2 / Faster-Whisper |
| Presisi | INT8 untuk deployment edge-core |
| Input | PCM mono 16 kHz `int16` |
| Transport | Secure WebSocket |
| Output | Query teks per utterance |

## Pesan Selama Sesi

| Arah | Pesan | Fungsi |
| --- | --- | --- |
| Client → STT | Binary PCM | Mengirim chunk audio |
| STT → client | `PROCESSING` | Menandai akhir ucapan dan transkripsi |
| STT → client | `AI_REPLY:<text>` | Mengirim jawaban akhir untuk status sesi |
| STT → n8n | JSON query | Memulai workflow orkestrasi |

## Penanganan Kegagalan

- Transkrip kosong tidak boleh memanggil aktuator.
- Kegagalan webhook harus menghasilkan pesan yang jelas dan tidak boleh mengulang aktuasi tanpa batas.
- Token WebSocket divalidasi saat handshake.
- Ukuran audio harus dibatasi agar kiriman yang terlalu besar dapat ditolak.

!!! info "Screenshot yang dibutuhkan"
    Tambahkan cuplikan log anonim: model berhasil dimuat, WebSocket diterima, dan satu transkripsi berhasil. Hapus hostname, IP, token, dan path home.
