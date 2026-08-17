# Alur Proses SmartLab

## Tahap 1 — Dari Wake Word sampai Transkripsi

<figure markdown="span">
  ![Tahap wake word, perekaman, dan transkripsi](../assets/diagrams/runtime-stage-1.png)
  <figcaption>Raspberry Pi mulai merekam setelah Omega terdeteksi. STT menentukan akhir ucapan, lalu meneruskan hasil transkripsi ke n8n.</figcaption>
</figure>

Urutan proses:

1. OpenWakeWord memantau audio lokal tanpa mengirimkannya ke server.
2. Skor Omega melewati ambang deteksi dan LED berubah dari siaga ke merekam.
3. Audio mono 16 kHz `int16` dikirim sebagai frame PCM melalui WebSocket aman.
4. STT mengumpulkan audio dan mendeteksi akhir ucapan.
5. STT mengirim sinyal `PROCESSING`, membuat transkripsi, lalu meneruskan teks ke webhook n8n.

## Tahap 2 — Dari Keputusan sampai Jawaban Suara

<figure markdown="span">
  ![Tahap konteks, keputusan, aktuasi, dan suara](../assets/diagrams/runtime-stage-2.png)
  <figcaption>n8n membaca kondisi perangkat, meminta keputusan dari SLM, memeriksa hasilnya, menjalankan aksi yang valid, dan membuat jawaban suara.</figcaption>
</figure>

```mermaid
sequenceDiagram
    accTitle: Siklus Permintaan SmartLab
    accDescr: Urutan komunikasi n8n dengan Home Assistant, SLM lokal, dan Piper TTS untuk satu permintaan pengguna

    participant N as n8n
    participant H as Home Assistant
    participant S as SLM lokal
    participant T as Piper TTS

    N->>H: Ambil status perangkat
    H-->>N: Status dan atribut
    N->>N: Pilih perangkat yang diizinkan dan buat konteks
    N->>S: Kirim konteks, permintaan, dan daftar fungsi
    S-->>N: Jawaban teks dan fungsi bila diperlukan
    N->>N: Baca dan periksa hasil

    alt Perintah dapat dijalankan
        N->>H: Panggil scene atau layanan
        H-->>N: Hasil pemanggilan layanan
    else Tanpa aksi, ditolak, atau mode uji
        N->>N: Tidak mengubah perangkat
    end

    N->>N: Bentuk respons final
    N->>T: Kirim teks tersanitasi
    T-->>N: Audio WAV
```

## Status yang Dilihat Pengguna

| Status | Indikator | Makna |
| --- | --- | --- |
| Siaga | LED hijau | Menunggu wake word |
| Merekam | LED biru | Merekam perintah |
| Memproses | LED ungu | STT dan n8n sedang bekerja |
| Selesai | Kembali hijau | Sesi telah selesai |
| Gangguan koneksi | Pola khusus | Koneksi sedang dipulihkan |

## Batas Penggunaan Saat Ini

- Sistem saat ini mengutamakan satu permintaan aktif pada satu waktu.
- Jawaban suara diputar melalui speaker pada komputer utama, bukan dikirim kembali ke Raspberry Pi.
- Sistem belum dirancang untuk beberapa perangkat suara yang berbicara secara bersamaan.
- Respons berhasil dari Home Assistant menunjukkan bahwa layanan telah dipanggil. Keberhasilan fisik tetap perlu dilihat pada perangkat atau diperiksa melalui status terbaru.
