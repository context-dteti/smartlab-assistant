# Pemasangan Model dan Pemulihan

## Prinsip Dasar

Pemasangan model dilakukan sebagai perubahan tersendiri agar mudah diperiksa dan dibatalkan. Saat model diganti, alamat layanan, kredensial, alur n8n, STT, TTS, dan Home Assistant tetap menggunakan konfigurasi yang sama.

## Berkas yang Disiapkan

Satu paket model sekurang-kurangnya memuat:

- File GGUF dengan nama stabil.
- Catatan asal model dan checksum SHA-256.
- Konfigurasi konversi dan kuantisasi.
- Hasil evaluasi model HF dan Q4 yang terpisah.
- Hasil uji pemuatan `llama-server` dan uji fungsi singkat.
- Salinan model sebelumnya untuk pemulihan.

## Urutan Pemasangan

1. Cocokkan checksum file sumber dan tujuan.
2. Pastikan model dapat dimuat tanpa mengubah layanan aktif.
3. Cadangkan konfigurasi layanan dan catat lokasi model lama.
4. Ubah hanya lokasi model pada konfigurasi layanan.
5. Muat ulang konfigurasi dan mulai ulang layanan SLM.
6. Periksa status layanan dan log pemuatan GPU.
7. Uji perintah eksplisit, status, implisit, kondisi yang sudah sesuai, dan penolakan tanpa aktuasi perangkat.
8. Lakukan satu uji fisik yang aman dan terkontrol.
9. Pantau kesalahan aktuasi, penolakan, waktu respons, dan keluaran suara.

## Cara Memulihkan Model Sebelumnya

```text
1. Hentikan sementara permintaan baru.
2. Kembalikan konfigurasi ke model stabil sebelumnya.
3. Muat ulang konfigurasi dan mulai ulang layanan SLM.
4. Periksa status layanan dan checksum model aktif.
5. Uji pembacaan status dan satu aktuasi yang aman.
6. Catat alasan pemulihan dan hasil pemeriksaan.
```

Perintah lengkap, alamat perangkat, nama pengguna, dan lokasi file internal disimpan dalam panduan privat, bukan pada dokumentasi web publik.

## Kapan Model Perlu Dikembalikan

- Model gagal dimuat atau layanan tidak stabil.
- Akurasi pemanggilan fungsi turun jauh dari hasil acuan.
- Terjadi aktuasi pada contoh yang seharusnya tidak menjalankan perangkat.
- Validator menerima argumen di luar kontrak.
- Waktu respons atau penggunaan memori mengganggu layanan lain.
- TTS gagal dan menimbulkan pengulangan alur yang tidak aman.

## Cadangan

Cadangan sebelum perubahan mencakup konfigurasi layanan, alur n8n, basis data n8n, catatan model, dan konfigurasi lingkungan. Nilai rahasia tidak disalin ke dokumentasi publik.
