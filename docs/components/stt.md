# Speech-to-Text

## Peran layanan

Layanan Speech-to-Text menerima frame PCM dari voice satellite, mendeteksi akhir utterance, menjalankan transkripsi Bahasa Indonesia, dan meneruskan hasilnya ke orkestrator.

## Konfigurasi konseptual

| Bagian | Implementasi |
| --- | --- |
| Model | Whisper Small Bahasa Indonesia |
| Runtime | CTranslate2 / Faster-Whisper |
| Presisi | INT8 untuk deployment edge-core |
| Input | PCM mono 16 kHz `int16` |
| Transport | Secure WebSocket |
| Output | Query teks per utterance |

## Pesan sesi

| Arah | Pesan | Fungsi |
| --- | --- | --- |
| Client → STT | Binary PCM | Mengirim chunk audio |
| STT → client | `PROCESSING` | Menandai akhir ucapan dan transkripsi |
| STT → client | `AI_REPLY:<text>` | Mengirim jawaban akhir untuk status sesi |
| STT → n8n | JSON query | Memulai workflow orkestrasi |

## Failure behavior

- Transkrip kosong tidak boleh memanggil aktuator.
- Kegagalan webhook harus menghasilkan respons error yang jelas, bukan retry aktuasi tanpa batas.
- Token WebSocket divalidasi saat handshake.
- Buffer audio harus dibatasi agar request berukuran tidak wajar ditolak.

!!! info "Screenshot yang dibutuhkan"
    Tambahkan cuplikan log anonim: model berhasil dimuat, WebSocket diterima, dan satu transkripsi berhasil. Hapus hostname, IP, token, dan path home.
