# Perangkat Suara (Raspberry Pi)

## Peran Perangkat

Raspberry Pi bertugas mendeteksi wake word, merekam suara, mengirim audio, dan menampilkan status melalui LED. Wake word diproses langsung pada Raspberry Pi sehingga audio saat siaga tidak terus-menerus dikirim ke komputer utama.

## Komponen

| Komponen | Fungsi |
| --- | --- |
| Raspberry Pi 3 Model B Rev 1.2 | Menjalankan voice client sebagai service |
| ReSpeaker 2-Mic HAT | Capture audio dan playback/antarmuka audio |
| `omega.tflite` | Model OpenWakeWord aktif |
| SPI status LED | Standby, listening, processing, dan error |
| Systemd service | Menjaga client aktif setelah reboot |

## Alur pada Raspberry Pi

```mermaid
flowchart TB
    accTitle: Alur Perangkat Suara
    accDescr: Proses lokal dari pemantauan wake word hingga streaming audio dan pemulihan sesi

    standby([Siaga]) --> detect{Omega terdeteksi?}
    detect -->|Belum| standby
    detect -->|Ya| listen[Buka sesi audio]
    listen --> stream[Kirim PCM 16 kHz]
    stream --> processing[Tunggu hasil]
    processing --> ready([Kembali siaga])
    processing -->|Koneksi gagal| reconnect[Hubungkan ulang]
    reconnect --> standby
```

## Pengujian yang Disarankan

- Recall Omega pada variasi pembicara, jarak, tempo, dan kebisingan.
- False activations per hour pada audio negatif kontinu.
- Recovery setelah Wi-Fi terputus dan setelah reboot.
- Sinkronisasi LED dengan state sesi.
- Kualitas audio 16 kHz mono pada perangkat ReSpeaker asli.

!!! info "Screenshot yang dibutuhkan"
    Tambahkan foto Raspberry Pi, ReSpeaker, dan LED. Pastikan tidak ada label jaringan atau kredensial yang terlihat.
