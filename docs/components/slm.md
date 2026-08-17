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

## Training dan Model Terpasang

Training dan evaluasi referensi menggunakan checkpoint HF-F16 pada komputer terpisah. Model yang dipasang pada komputer utama menggunakan format GGUF. Hasil HF-F16 dan Q4 dilaporkan secara terpisah karena format serta cara menjalankannya berbeda.
