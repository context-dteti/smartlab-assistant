# Small Language Model (SLM)

## Peran Model

SLM menerima kondisi perangkat dari Home Assistant, permintaan pengguna, dan empat fungsi yang tersedia. Model dapat menghasilkan jawaban teks, memilih fungsi, atau melakukan keduanya. Model tidak mengendalikan perangkat secara langsung karena hasilnya selalu diperiksa oleh n8n.

## Fungsi yang Tersedia

| Fungsi | Tujuan | Contoh parameter |
| --- | --- | --- |
| `HassTurnOn` | Menyalakan entitas yang diizinkan | `name` |
| `HassTurnOff` | Mematikan entitas yang diizinkan | `name` |
| `HassLightSet` | Mengatur satu atribut lampu | `name` + brightness, color, atau color temperature |
| `HassSetTemperature` | Mengatur target suhu AC | `name` + `temperature` |

n8n menerjemahkan fungsi tersebut menjadi scene atau layanan Home Assistant. Dengan cara ini, model tidak perlu mengetahui detail instalasi perangkat.

## Bentuk Input

Input model mencakup:

1. Instruksi domain dan aturan keselamatan.
2. Ringkasan kondisi perangkat yang diizinkan.
3. Query pengguna hasil STT.
4. Format fungsi yang dapat digunakan.

```text
Konteks perangkat:
- Lampu warna: on, brightness 75%, warna putih
- AC utama: on, target 24°C

Permintaan pengguna:
"ruangan terasa panas"
```

## Batas Keputusan

- Maksimal satu aksi per utterance pada kontrak saat ini.
- Perangkat tujuan wajib berada dalam daftar yang diizinkan.
- `HassLightSet` menggunakan satu atribut perubahan pada satu tool call.
- State sudah sesuai harus menghasilkan no-tool.
- Permintaan di luar domain tidak boleh dieksekusi.

## Model yang Digunakan

Model dasar yang digunakan adalah **Qwen3.5-0.8B**. Model tersebut disesuaikan untuk Bahasa Indonesia dan fungsi SmartLab, kemudian dikonversi ke format **GGUF Q4_K_M** agar dapat dijalankan secara lokal pada Jetson Orin NX melalui `llama.cpp`.

| Bagian | Implementasi |
| --- | --- |
| Model dasar | Qwen3.5-0.8B |
| Kemampuan utama | Perintah eksplisit, pertanyaan status, dan keluhan implisit |
| Model yang terakhir terverifikasi aktif | Model SmartLab implisit Q4_K_M |
| Runtime deployment | `llama.cpp` dengan akselerasi GPU |
| Model cadangan | Baseline Q4_K_M |
| Kandidat terbaru | Model implisit dari baseline candidate; sudah dievaluasi, belum dipasang |

Model aktif dan model kandidat dibedakan dengan jelas. Hasil kandidat tidak dianggap sebagai kemampuan sistem yang sedang berjalan sampai model tersebut dipasang dan diuji pada alur n8n.

## Metode Training

Training dijalankan pada komputer GPU terpisah menggunakan **Unsloth** dan PyTorch dalam presisi **bfloat16**. Metode yang digunakan adalah full fine-tuning, sehingga seluruh parameter model disesuaikan pada data SmartLab, bukan hanya adapter tambahan.

| Bagian | Konfigurasi |
| --- | --- |
| Dataset implisit | 12.000 training, 1.200 development, dan 1.200 frozen test |
| Distribusi keputusan | 50% menjalankan fungsi dan 50% tanpa fungsi |
| Lama training | 3 epoch |
| Effective batch size | 16 |
| Presisi training | bfloat16 |
| GPU eksperimen terbaru | NVIDIA A100 |
| Ekspor dan evaluasi Q4 | NVIDIA L4 dan `llama.cpp` |

Model implisit terbaru dilanjutkan dari checkpoint HF baseline candidate, bukan dari file GGUF. Bagian development dipakai untuk memantau training, sedangkan frozen test hanya dipakai pada evaluasi akhir. Setelah evaluasi HF-F16, model diekspor dan dikuantisasi ke Q4_K_M, lalu diuji kembali karena hasil model terkuantisasi dapat berbeda dari checkpoint training.

Dokumentasi publik ini menjelaskan konfigurasi dan tahapan utama. Notebook, checksum, manifest, serta log eksperimen disimpan terpisah sebagai catatan reproduksibilitas penelitian.

## Format Model dan Pelaporan

Training dan evaluasi referensi menggunakan checkpoint HF-F16 pada komputer terpisah. Model yang dipasang pada komputer utama menggunakan format GGUF. Hasil HF-F16 dan Q4 dilaporkan secara terpisah karena format serta cara menjalankannya berbeda.
