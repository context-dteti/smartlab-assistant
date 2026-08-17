# Decision Engine SLM

## Peran model

Small Language Model menerima konteks state Home Assistant, query pengguna, dan empat native function tool. Model menghasilkan respons teks, tool call, atau keduanya. Ia tidak menjalankan perangkat secara langsung; keputusan tetap melewati validator n8n.

## Native function tools

| Tool | Tujuan | Contoh argumen |
| --- | --- | --- |
| `HassTurnOn` | Menyalakan entitas yang diizinkan | `name` |
| `HassTurnOff` | Mematikan entitas yang diizinkan | `name` |
| `HassLightSet` | Mengatur satu atribut lampu | `name` + brightness, color, atau color temperature |
| `HassSetTemperature` | Mengatur target suhu AC | `name` + `temperature` |

Mapping tool logis ke scene atau service Home Assistant berada pada executor. Dengan demikian, dataset dan model tidak terikat langsung pada detail deployment fisik.

## Bentuk input

Input model mencakup:

1. Instruksi domain dan aturan keselamatan.
2. Ringkasan state perangkat yang masuk allowlist.
3. Query pengguna hasil STT.
4. Schema native function tool.

```text
Konteks perangkat:
- Lampu warna: on, brightness 75%, warna putih
- AC utama: on, target 24°C

Permintaan pengguna:
"ruangan terasa panas"
```

## Batas keputusan

- Maksimal satu aksi per utterance pada kontrak saat ini.
- Entity wajib berada dalam allowlist.
- `HassLightSet` menggunakan satu atribut perubahan pada satu tool call.
- State sudah sesuai harus menghasilkan no-tool.
- Permintaan di luar domain tidak boleh dieksekusi.

## Lifecycle model

Checkpoint HF-F16 dipakai untuk training dan evaluasi referensi. Deployment core menggunakan artifact GGUF yang telah melewati konversi, kuantisasi, preflight load, frozen evaluation, dan smoke test. Angka HF tidak boleh dilaporkan sebagai angka Q4 karena format dan runtime berbeda.
