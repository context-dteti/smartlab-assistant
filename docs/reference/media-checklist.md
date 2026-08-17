# Checklist Gambar dan Screenshot

## Gambar Draw.io yang Tersedia

| Gambar | Status | Tindakan sebelum publikasi |
| --- | --- | --- |
| Konteks sistem | Terverifikasi | Label telah diperbarui menjadi “Whisper STT” |
| Topologi fisik | Terverifikasi | Pertahankan “Raspberry Pi 3B”; perangkat aktif adalah Raspberry Pi 3 Model B Rev 1.2 |
| Tahap 1 alur proses | Draf tersedia | Samakan penulisan STT dan n8n, lalu tambahkan keterangan versi |
| Tahap 2 alur proses | Draf tersedia | Pastikan teks di sisi kanan tidak terpotong |

## Screenshot yang Perlu Ditambahkan

| Prioritas | Screenshot/foto | Halaman tujuan | Catatan |
| ---: | --- | --- | --- |
| P1 | Canvas penuh workflow n8n | Orkestrasi n8n | Sensor URL dan credential ID |
| P1 | Dashboard Home Assistant SmartLab | Home Assistant | Tampilkan hanya entitas relevan |
| P1 | Perangkat suara lengkap | Perangkat Suara | Raspberry Pi, ReSpeaker, dan LED |
| P1 | Perangkat yang dikontrol | Beranda/demonstrasi | Lampu, AC, display, atau scene |
| P2 | Node Build Context | Orkestrasi n8n | Gunakan contoh state anonim |
| P2 | Node Parse and Validate | Orkestrasi n8n | Jangan tampilkan token |
| P2 | Log layanan sehat | Pemantauan | Hapus nama host, IP, dan lokasi direktori pengguna |
| P2 | Grafik evaluasi model | Model dan Evaluasi | Cantumkan format, bagian data, dan jumlah sampel |
| P3 | Speaker dan bentuk gelombang TTS | Text-to-Speech | Gunakan audio yang tidak sensitif |

## Standar Visual

- Gunakan resolusi minimal 1600 px pada sisi terpanjang untuk screenshot desktop.
- Ekspor diagram sebagai SVG untuk web dan PNG sebagai format cadangan.
- Gunakan legenda yang konsisten: biru untuk layanan, hijau untuk status atau perangkat, kuning untuk pemeriksaan, dan merah untuk gangguan atau risiko.
- Sertakan judul, tanggal revisi, keterangan gambar, dan teks alternatif.
- Potong area kosong dan pastikan teks tetap terbaca pada layar laptop.
- Jangan menaruh kata sandi, token, IP internal, ID kredensial, atau data mentah pengguna.

## Pemeriksaan Sebelum Publikasi

- [ ] Label hardware sesuai inventaris.
- [ ] Endpoint digeneralisasi untuk publik.
- [ ] Tidak ada nilai rahasia atau identitas privat.
- [ ] Teks alternatif menjelaskan isi, bukan hanya nama file.
- [ ] Diagram terbaca dalam mode terang dan gelap.
- [ ] Keterangan gambar menyebut status draf atau final.
