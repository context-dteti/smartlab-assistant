# Instalasi

SmartLab terdiri dari beberapa layanan yang berjalan pada perangkat berbeda. Instalasi dilakukan per komponen, kemudian seluruh jalur diuji dari perangkat suara sampai Home Assistant.

## Perangkat yang Diperlukan

| Perangkat | Kebutuhan utama |
| --- | --- |
| Raspberry Pi 3B | ReSpeaker 2-Mic HAT, LED status, dan koneksi jaringan |
| Komputer utama | NVIDIA Jetson Orin NX, penyimpanan model, dan speaker |
| Home Assistant | Host yang sudah terhubung dengan perangkat laboratorium |
| Komputer training | GPU terpisah untuk fine-tuning dan ekspor model |

## Perangkat Lunak

| Komponen | Implementasi |
| --- | --- |
| Wake word | OpenWakeWord dengan model Omega |
| Speech-to-Text | Faster-Whisper dan model Bahasa Indonesia |
| Decision engine | `llama-server` dan model Qwen3.5-0.8B dalam format GGUF |
| Orkestrasi | n8n dan PostgreSQL |
| Otomasi perangkat | Home Assistant |
| Text-to-Speech | Piper TTS |
| Koneksi publik terbatas | HTTPS/WSS melalui tunnel terkelola |

## Urutan Instalasi

### 1. Siapkan Home Assistant

Hubungkan perangkat laboratorium ke Home Assistant, lalu pastikan setiap entitas dapat dibaca dan dikendalikan dari dashboard. Catat hanya entitas yang akan digunakan oleh prototipe.

### 2. Siapkan komputer utama

Pasang runtime untuk STT, `llama-server`, n8n, dan Piper TTS. Setiap layanan dijalankan melalui service system agar aktif kembali setelah reboot. Simpan token layanan pada environment file dengan izin terbatas, bukan di source code.

### 3. Pasang model SLM

Salin model GGUF yang telah dievaluasi ke direktori model. Cocokkan checksum SHA-256 dengan manifest, lakukan uji pemuatan, kemudian arahkan service SLM ke file tersebut. Panduan pergantian tersedia pada halaman [Mengganti dan Memulihkan Model](../operations/deployment.md).

### 4. Impor workflow n8n

Impor workflow SmartLab, hubungkan credential Home Assistant, lalu isi endpoint STT, SLM, dan TTS menggunakan konfigurasi lingkungan. Jalankan workflow dalam mode dry-run sebelum mengizinkan aktuasi.

### 5. Siapkan perangkat suara

Pasang ReSpeaker pada Raspberry Pi, periksa input dan output audio, lalu instal voice client serta model wake word Omega. Pastikan service kembali aktif setelah reboot dan LED mengikuti status siaga, mendengarkan, memproses, serta gangguan.

### 6. Hubungkan layanan

Gunakan token berbeda untuk jalur perangkat suara ke STT, STT ke n8n, n8n ke SLM, dan n8n ke TTS. Jangan menaruh token pada dokumentasi, screenshot, atau repository publik.

## Pemeriksaan Instalasi

| Pemeriksaan | Hasil yang diharapkan |
| --- | --- |
| Wake word | Omega mengubah perangkat dari siaga ke mode mendengarkan |
| STT | Audio mono 16 kHz menghasilkan teks Bahasa Indonesia |
| n8n | Status perangkat terbaca dan konteks terbentuk |
| SLM | Respons teks atau satu tool call valid dihasilkan |
| Home Assistant | Dry-run menunjukkan service dan parameter yang benar |
| TTS | Jawaban akhir menghasilkan audio WAV dan diputar satu kali |
| Reboot | Seluruh service kembali aktif tanpa konfigurasi manual |

## Informasi Konfigurasi

Dokumentasi publik tidak menyertakan alamat internal, password, token, credential ID, atau lokasi file pada perangkat produksi. Nilai tersebut diisi oleh operator melalui environment file dan panduan internal saat deployment.
