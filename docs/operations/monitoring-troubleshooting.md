# Pemantauan dan Penanganan Masalah

## Pemeriksaan Dasar

| Komponen | Pemeriksaan | Hasil sehat |
| --- | --- | --- |
| Perangkat suara | Log layanan | Model Omega dimuat dan perangkat dalam keadaan siaga |
| STT | Status layanan dan koneksi WSS | Layanan aktif dan token diterima |
| n8n | Container dan alur kerja | Container sehat dan alur kerja aktif |
| SLM lokal | Endpoint status dan log model | HTTP berhasil, model dan lapisan GPU termuat |
| Home Assistant | Pembacaan status dengan kredensial n8n | Daftar status perangkat dapat dibaca |
| TTS | Permintaan teks uji | File WAV berisi audio |
| Pemutar audio | Log layanan dan pemutaran | Satu file diputar satu kali |

## Menelusuri Satu Permintaan

Satu `trace_id` sebaiknya mengikuti permintaan dari STT, n8n, SLM, Home Assistant, TTS, hingga suara diputar. Catat waktu pada tahap berikut tanpa menyimpan audio atau isi perintah sensitif lebih lama dari yang diperlukan:

- Wake word terdeteksi dan perekaman dimulai.
- Pengguna selesai berbicara dan transkripsi selesai.
- Konteks disusun dan model memproses perintah.
- Hasil diperiksa dan Home Assistant dipanggil.
- TTS selesai dan suara mulai diputar.

## Masalah Umum

### Wake Word Tidak Konsisten

1. Periksa penguatan suara dan perangkat input ReSpeaker.
2. Bandingkan skor tertinggi dengan ambang deteksi yang digunakan.
3. Uji jarak, pembicara, dan kebisingan secara terpisah.
4. Jangan langsung menurunkan ambang tanpa mengukur jumlah aktivasi yang keliru.

### STT Terhubung tetapi Alur n8n Tidak Berjalan

1. Pastikan query hasil transkripsi tidak kosong.
2. Periksa token pada header webhook.
3. Pastikan URL yang digunakan adalah webhook produksi yang aktif.
4. Cocokkan log STT dan eksekusi n8n menggunakan waktu atau `trace_id`.

### SLM Menjawab Teks tanpa Memanggil Fungsi

1. Pastikan prompt, template percakapan, dan skema fungsi sesuai dengan data training.
2. Periksa endpoint model dan mode pemanggilan fungsi.
3. Bandingkan model HF dan GGUF menggunakan data uji yang sama.
4. Teks yang menyebut aksi belum dianggap sebagai aktuasi jika tidak ada pemanggilan fungsi yang valid.

### Status Home Assistant Tidak Berubah

1. Periksa apakah alur sedang berjalan dalam mode uji tanpa aktuasi.
2. Periksa hasil validator dan daftar entitas yang diizinkan.
3. Periksa layanan, domain, dan data yang dikirim.
4. Baca kembali state dan observasi perangkat fisik.

### Jawaban Suara Tidak Terdengar

1. Pastikan TTS menghasilkan file WAV yang berisi audio.
2. Periksa lokasi file keluaran dan hak aksesnya.
3. Periksa log pemutar audio dan perangkat ALSA.
4. Jangan mengulang aktuasi hanya untuk memperbaiki audio.

## Catatan Gangguan

Simpan waktu kejadian, komponen, gejala, ID permintaan, status layanan, dan tindakan pemulihan. Samarkan token, kredensial, IP privat, dan isi perintah pengguna sebelum catatan dibagikan.
