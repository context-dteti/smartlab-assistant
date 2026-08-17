# Text-to-Speech

## Peran layanan

Piper TTS mengubah jawaban final yang telah disanitasi menjadi audio WAV. Model resident disimpan di memori untuk mengurangi waktu muat antar-request.

## Jalur audio

1. n8n menghasilkan respons final yang singkat.
2. Sanitizer menghapus Markdown dan karakter yang tidak perlu dibacakan.
3. n8n memanggil endpoint TTS menggunakan bearer token.
4. Piper menghasilkan WAV dengan padding awal singkat.
5. n8n menulis file output pada shared path.
6. Audio player mendeteksi file selesai ditulis dan memutarnya pada speaker core node.

## Batas implementasi

- Respons audio saat ini diputar pada speaker core node.
- Satu nama file output bersama mengasumsikan satu request aktif.
- TTS gagal tidak boleh menyebabkan executor mengulang aksi Home Assistant.
- Teks error internal dan identifier teknis harus disanitasi sebelum dibacakan.

## Pemeriksaan minimum

| Pemeriksaan | Hasil yang diharapkan |
| --- | --- |
| Request teks valid | MIME audio dan body WAV non-empty |
| Token tidak ada/salah | Request ditolak |
| Teks kosong | Ditolak atau dilewati tanpa file rusak |
| Playback | Audio terdengar satu kali tanpa pengulangan aktuasi |

!!! info "Screenshot yang dibutuhkan"
    Tambahkan foto speaker dan satu cuplikan waveform atau pemutar audio hasil sintesis. Jangan tampilkan path home atau header autentikasi.
