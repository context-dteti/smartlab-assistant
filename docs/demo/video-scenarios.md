# Skenario Video Demonstrasi

## Format dua kamera

| Kamera | Framing | Tujuan |
| --- | --- | --- |
| Kamera A | Medium shot pengguna dan voice satellite | Menunjukkan interaksi natural dan wake word |
| Kamera B | Close-up perangkat/HA dashboard | Membuktikan perubahan state fisik |

Gunakan audio utama dari Kamera A atau mikrofon terpisah. Sinkronkan kedua kamera dengan satu tepukan sebelum pengambilan gambar.

## Struktur video 2–3 menit

1. **Pembuka 10–15 detik:** wide shot laboratorium dan satu kalimat tujuan prototipe.
2. **Arsitektur 15 detik:** overlay diagram konteks sistem.
3. **Demo eksplisit 30–40 detik:** dua kontrol langsung.
4. **Demo status 20 detik:** satu pertanyaan read-only.
5. **Demo implisit 30–40 detik:** satu kondisi termal dan satu pencahayaan.
6. **Safety 20 detik:** already-state atau refusal tanpa aktuasi.
7. **Penutup 10 detik:** ringkas on-premise inference dan hasil observasi.

## Daftar adegan

| Adegan | Ucapan | Visual utama | Overlay |
| --- | --- | --- | --- |
| Wake word | “Omega” | LED berpindah hijau → biru | `Wake word detected` |
| Explicit on/off | “matikan lampu warna” | Lampu dan HA state | `Explicit command` |
| Set warna | “ubah lampu ke hijau” | Lampu berubah hijau | `Validated tool call` |
| Status | “berapa suhu ruangan?” | Dashboard sensor | `Read-only · no actuation` |
| Implicit thermal | “ruangan panas” | AC/state target suhu | `Context-aware request` |
| Implicit glare | “terlalu silau” | Lampu diredupkan | `State-aware adjustment` |
| Already-state | “terlalu silau” saat lampu sudah redup | Tidak ada perubahan | `No-tool: state already suitable` |
| Refusal | Permintaan perangkat di luar allowlist | Tidak ada perubahan | `Rejected safely` |

## Cara mengambil gambar

- Tampilkan pengguna pada opening dan dua perintah pertama; setelah konteks jelas, close-up perangkat sudah cukup.
- Jangan hanya merekam dashboard. Sertakan perangkat fisik agar keberhasilan aktuasi dapat diamati.
- Rekam satu take bersih per skenario dan satu take cadangan.
- Sisakan 2–3 detik sebelum dan sesudah ucapan untuk editing.
- Hindari menampilkan URL, token, credential, dan notification pribadi pada layar.
- Gunakan overlay singkat satu baris; jangan menutupi perangkat.

## Acceptance sheet saat shooting

| Take | STT benar | Keputusan benar | Perangkat berubah/tetap sesuai | TTS jelas | Dipakai |
| --- | --- | --- | --- | --- | --- |
| 1 |  |  |  |  |  |
| 2 |  |  |  |  |  |
| 3 |  |  |  |  |  |

Video demonstrasi membuktikan perilaku pada skenario yang direkam, bukan menggantikan frozen evaluation atau pengujian keselamatan sistematis.
