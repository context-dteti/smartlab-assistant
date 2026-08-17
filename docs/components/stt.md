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

## Jika Transkripsi Tidak Berhasil

Jika suara tidak terdengar jelas atau hasil transkripsi kosong, sesi diakhiri tanpa menjalankan perintah perangkat. Raspberry Pi kemudian kembali ke mode siaga agar pengguna dapat mencoba lagi.

Jika hasil transkripsi tidak dapat diteruskan ke n8n, sistem memberi tahu pengguna bahwa permintaan belum berhasil dan tidak mengulangi perintah secara otomatis. Koneksi yang tidak valid ditolak sebelum audio diproses, sedangkan rekaman yang terlalu panjang dihentikan dengan aman.
