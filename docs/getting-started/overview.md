# Gambaran Umum

## Tujuan prototipe

SmartLab dirancang untuk mengeksplorasi interaksi suara privat pada ruang laboratorium. Pengguna dapat meminta status perangkat, memberi perintah langsung, atau menyampaikan kondisi seperti “ruangan panas” dan “terlalu silau”. Sistem menggabungkan ucapan tersebut dengan state aktual perangkat sebelum memilih respons.

## Ruang lingkup

| Area | Termasuk | Di luar scope saat ini |
| --- | --- | --- |
| Input | Wake word, audio mikrofon, Bahasa Indonesia | Percakapan multi-turn panjang |
| Pemahaman | Perintah eksplisit, status, kondisi implisit terbatas | Pengetahuan umum terbuka |
| Perangkat | Entitas laboratorium yang masuk allowlist | Perangkat di luar inventaris |
| Eksekusi | Scene dan service Home Assistant tervalidasi | Eksekusi kode bebas |
| Output | Respons teks singkat dan audio lokal | Streaming audio kembali ke satelit |
| Operasi | Satu request aktif pada satu waktu | Multi-satellite concurrency |

## Komponen utama

| Komponen | Peran |
| --- | --- |
| Raspberry Pi + ReSpeaker | Mendeteksi Omega, merekam audio, dan menampilkan status LED |
| Whisper STT | Mengubah PCM 16 kHz mono menjadi teks Bahasa Indonesia |
| n8n | Mengambil state, membangun konteks, memanggil SLM, memvalidasi, dan mengorkestrasi respons |
| Local SLM | Memilih respons atau native function tool dalam domain terbatas |
| Home Assistant | Menyediakan state dan menjalankan service perangkat |
| Piper TTS | Mengubah respons final menjadi audio WAV |
| Speaker lokal | Memutar jawaban pada core node |

## Prinsip keselamatan

1. Hanya entitas yang terdaftar yang boleh diakses.
2. Proposal model tidak langsung menjadi aksi fisik.
3. Validator memeriksa nama tool, entity, tipe, rentang nilai, dan jumlah aksi.
4. Permintaan tidak jelas, state yang sudah sesuai, atau target yang tidak diizinkan harus berakhir tanpa aktuasi.
5. Kegagalan TTS tidak boleh mengulang aksi fisik yang sudah dijalankan.

## Istilah privasi yang tepat

STT, SLM, dan TTS berjalan pada perangkat milik laboratorium dan tidak menggunakan API model bahasa publik. Beberapa koneksi dapat melewati tunnel HTTPS/WSS terkelola. Karena itu, deskripsi yang tepat adalah **private on-premise inference dengan secure managed tunnel**, bukan sistem air-gapped.
