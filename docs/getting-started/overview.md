# Gambaran Umum

## Tujuan Prototipe

SmartLab dirancang untuk mengeksplorasi interaksi suara privat pada ruang laboratorium. Pengguna dapat meminta status perangkat, memberi perintah langsung, atau menyampaikan kondisi seperti “ruangan panas” dan “terlalu silau”. Sistem menggabungkan ucapan tersebut dengan state aktual perangkat sebelum memilih respons.

## Batas Prototipe

| Area | Termasuk | Belum menjadi fokus |
| --- | --- | --- |
| Input | Wake word, audio mikrofon, Bahasa Indonesia | Percakapan multi-turn panjang |
| Pemahaman | Perintah eksplisit, status, kondisi implisit terbatas | Pengetahuan umum terbuka |
| Perangkat | Perangkat laboratorium yang telah didaftarkan | Perangkat di luar inventaris |
| Eksekusi | Scene dan service Home Assistant tervalidasi | Eksekusi kode bebas |
| Output | Respons teks singkat dan audio lokal | Streaming audio kembali ke satelit |
| Operasi | Satu permintaan aktif pada satu waktu | Beberapa perangkat suara secara bersamaan |

## Komponen Utama

| Komponen | Peran |
| --- | --- |
| Raspberry Pi + ReSpeaker | Mendeteksi Omega, merekam audio, dan menampilkan status LED |
| Whisper STT | Mengubah PCM 16 kHz mono menjadi teks Bahasa Indonesia |
| n8n | Mengambil state, membangun konteks, memanggil SLM, memvalidasi, dan mengorkestrasi respons |
| SLM lokal | Memilih jawaban atau fungsi yang sesuai dalam domain terbatas |
| Home Assistant | Menyediakan state dan menjalankan service perangkat |
| Piper TTS | Mengubah respons final menjadi audio WAV |
| Speaker lokal | Memutar jawaban pada komputer utama |

## Prinsip Keselamatan

1. Hanya entitas yang terdaftar yang boleh diakses.
2. Proposal model tidak langsung menjadi aksi fisik.
3. n8n memeriksa fungsi, perangkat tujuan, jenis nilai, rentang nilai, dan jumlah aksi.
4. Permintaan tidak jelas, state yang sudah sesuai, atau target yang tidak diizinkan harus berakhir tanpa aktuasi.
5. Kegagalan TTS tidak boleh mengulang aksi fisik yang sudah dijalankan.

## Privasi Sistem

STT, SLM, dan TTS berjalan pada perangkat milik laboratorium dan tidak menggunakan API model bahasa publik. Beberapa koneksi melewati tunnel HTTPS/WSS yang dikelola. Dengan demikian, sistem dapat dijelaskan sebagai **pemrosesan lokal dengan koneksi terenkripsi**, bukan sebagai sistem yang sepenuhnya terputus dari jaringan.
