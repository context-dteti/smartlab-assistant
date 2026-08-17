# Skenario Video Demonstrasi

## Pengaturan Dua Kamera

| Kamera | Framing | Tujuan |
| --- | --- | --- |
| Kamera A | Pengguna dan perangkat suara | Menunjukkan cara pengguna berbicara dan mengucapkan wake word |
| Kamera B | Perangkat atau dashboard Home Assistant | Menunjukkan perubahan kondisi perangkat |

Gunakan audio utama dari Kamera A atau mikrofon terpisah. Sinkronkan kedua kamera dengan satu tepukan sebelum pengambilan gambar.

## Susunan Video 2–3 Menit

1. **Pembuka 10–15 detik:** tampilkan ruang laboratorium dan jelaskan tujuan prototipe dalam satu kalimat.
2. **Arsitektur 15 detik:** overlay diagram konteks sistem.
3. **Demo eksplisit 30–40 detik:** dua kontrol langsung.
4. **Demo status 20 detik:** ajukan satu pertanyaan yang hanya membaca kondisi perangkat.
5. **Demo implisit 30–40 detik:** satu kondisi termal dan satu pencahayaan.
6. **Keamanan 20 detik:** tunjukkan kondisi yang tidak memerlukan aksi atau permintaan yang ditolak.
7. **Penutup 10 detik:** ringkas pemrosesan lokal dan hasil demonstrasi.

## Daftar Adegan

| Adegan | Ucapan | Visual utama | Overlay |
| --- | --- | --- | --- |
| Wake word | “Omega” | LED berpindah hijau → biru | `Omega terdeteksi` |
| Perintah langsung | “matikan lampu warna” | Lampu dan status Home Assistant | `Perintah langsung` |
| Mengatur warna | “ubah lampu ke hijau” | Lampu berubah hijau | `Perintah telah diperiksa` |
| Membaca status | “berapa suhu ruangan?” | Dashboard sensor | `Tanpa mengubah perangkat` |
| Keluhan suhu | “ruangan panas” | Target suhu AC | `Memahami kondisi ruangan` |
| Keluhan silau | “terlalu silau” | Lampu diredupkan | `Menyesuaikan kondisi lampu` |
| Kondisi sudah sesuai | “terlalu silau” saat lampu sudah redup | Tidak ada perubahan | `Tidak perlu aksi` |
| Permintaan ditolak | Permintaan perangkat di luar daftar | Tidak ada perubahan | `Ditolak dengan aman` |

## Cara Mengambil Gambar

- Tampilkan pengguna pada pembuka dan dua perintah pertama. Setelah alurnya jelas, kamera dapat berfokus pada perangkat.
- Jangan hanya merekam dashboard. Sertakan perangkat fisik agar keberhasilan aktuasi dapat diamati.
- Rekam satu pengambilan utama dan satu cadangan untuk setiap skenario.
- Sisakan 2–3 detik sebelum dan sesudah ucapan untuk editing.
- Hindari menampilkan URL, token, credential, dan notification pribadi pada layar.
- Gunakan overlay singkat satu baris; jangan menutupi perangkat.

## Catatan Hasil Pengambilan

| Take | STT benar | Keputusan benar | Perangkat berubah/tetap sesuai | TTS jelas | Dipakai |
| --- | --- | --- | --- | --- | --- |
| 1 |  |  |  |  |  |
| 2 |  |  |  |  |  |
| 3 |  |  |  |  |  |

Video demonstrasi membuktikan perilaku pada skenario yang direkam, bukan menggantikan frozen evaluation atau pengujian keselamatan sistematis.
