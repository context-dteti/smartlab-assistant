# Text-to-Speech

## Peran Layanan

Piper TTS mengubah jawaban akhir menjadi audio WAV. Model tetap berada di memori agar tidak perlu dimuat ulang untuk setiap permintaan.

## Alur Audio

1. n8n menghasilkan respons final yang singkat.
2. n8n menghapus Markdown dan karakter yang tidak perlu dibacakan.
3. n8n memanggil endpoint TTS menggunakan bearer token.
4. Piper menghasilkan WAV dengan padding awal singkat.
5. n8n menyimpan file audio pada folder bersama.
6. Pemutar audio mendeteksi file yang selesai ditulis dan memutarnya melalui speaker komputer utama.

## Batas Saat Ini

- Jawaban audio saat ini diputar melalui speaker komputer utama.
- Satu nama file audio digunakan bersama sehingga sistem mengutamakan satu permintaan aktif.
- Kegagalan TTS tidak boleh membuat n8n mengulang aksi Home Assistant.
- Teks error internal dan identifier teknis harus disanitasi sebelum dibacakan.

## Pemeriksaan Minimum

| Pemeriksaan | Hasil yang diharapkan |
| --- | --- |
| Teks dan token valid | Respons audio berisi WAV yang dapat diputar |
| Token tidak ada/salah | Permintaan ditolak |
| Teks kosong | Ditolak atau dilewati tanpa file rusak |
| Pemutaran | Audio terdengar satu kali tanpa pengulangan aktuasi |

!!! info "Screenshot yang dibutuhkan"
    Tambahkan foto speaker dan satu cuplikan waveform atau pemutar audio hasil sintesis. Jangan tampilkan path home atau header autentikasi.
