# Checklist Gambar dan Screenshot

## Gambar Draw.io yang Tersedia

| Gambar | Status | Tindakan sebelum publikasi |
| --- | --- | --- |
| Konteks sistem | Terverifikasi | Label telah diperbarui menjadi “Whisper STT” |
| Topologi fisik | Terverifikasi | Pertahankan “Raspberry Pi 3B”; perangkat aktif adalah Raspberry Pi 3 Model B Rev 1.2 |
| Tahap 1 runtime | Draf tersedia | Samakan kapitalisasi STT/n8n dan tambahkan caption versi |
| Tahap 2 runtime | Draf tersedia | Pastikan teks di sisi kanan tidak terpotong |

## Screenshot yang Perlu Ditambahkan

| Prioritas | Screenshot/foto | Halaman tujuan | Catatan |
| ---: | --- | --- | --- |
| P1 | Canvas penuh workflow n8n | Orkestrasi n8n | Sensor URL dan credential ID |
| P1 | Dashboard Home Assistant SmartLab | Home Assistant | Tampilkan hanya entitas relevan |
| P1 | Voice satellite lengkap | Voice satellite | Raspberry Pi, ReSpeaker, dan LED |
| P1 | Perangkat yang dikontrol | Beranda/demonstrasi | Lampu, AC, display, atau scene |
| P2 | Node Build Context | Orkestrasi n8n | Gunakan contoh state anonim |
| P2 | Node Parse and Validate | Orkestrasi n8n | Jangan tampilkan token |
| P2 | Log service sehat | Monitoring | Hapus hostname, IP, dan path home |
| P2 | Grafik evaluasi model | Dataset dan evaluasi | Cantumkan format, split, dan denominator |
| P3 | Speaker dan waveform TTS | Text-to-Speech | Gunakan audio non-sensitif |

## Standar Visual

- Gunakan resolusi minimal 1600 px pada sisi terpanjang untuk screenshot desktop.
- Export diagram sebagai SVG untuk web dan PNG untuk fallback.
- Gunakan legenda konsisten: biru untuk service, hijau untuk state/perangkat, kuning untuk verifikasi, merah untuk failure/risk.
- Sertakan judul, tanggal revisi, caption, dan alt text.
- Crop area kosong dan pastikan teks tetap terbaca pada layar laptop.
- Jangan menaruh password, token, IP internal, credential ID, atau raw user data.

## Pemeriksaan Sebelum Publikasi

- [ ] Label hardware sesuai inventaris.
- [ ] Endpoint digeneralisasi untuk publik.
- [ ] Tidak ada secret atau identifier privat.
- [ ] Alt text menjelaskan isi, bukan hanya nama file.
- [ ] Diagram terbaca dalam mode terang dan gelap.
- [ ] Caption menyebut status draf atau final.
