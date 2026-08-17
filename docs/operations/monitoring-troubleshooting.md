# Monitoring dan Troubleshooting

## Health check minimum

| Komponen | Pemeriksaan | Hasil sehat |
| --- | --- | --- |
| Voice satellite | Journal service | Model Omega load dan standby |
| STT | Status service dan handshake WSS | Service aktif, handshake authorized diterima |
| n8n | Container dan workflow | Container sehat, workflow aktif |
| Local SLM | Health endpoint dan log model | HTTP sukses, model dan GPU layer termuat |
| Home Assistant | State read dengan credential n8n | Daftar state valid |
| TTS | Request teks uji | WAV non-empty |
| Audio player | Journal dan playback | Satu file diputar satu kali |

## Trace satu request

Satu `trace_id` sebaiknya mengikuti permintaan dari STT, n8n, SLM, Home Assistant, TTS, hingga playback. Catat timestamp berikut tanpa menyimpan audio atau query sensitif lebih lama dari yang diperlukan:

- Wake word dan mulai capture.
- End-of-speech dan selesai STT.
- Context build dan inference.
- Validasi dan Home Assistant call.
- TTS selesai dan time-to-first-audio.

## Masalah umum

### Wake word tidak konsisten

1. Periksa gain dan device input ReSpeaker.
2. Bandingkan skor maksimum dengan threshold aktif.
3. Uji jarak, pembicara, dan noise secara terpisah.
4. Jangan langsung menurunkan threshold tanpa mengukur false activations per hour.

### STT terhubung tetapi workflow tidak berjalan

1. Pastikan query hasil transkripsi tidak kosong.
2. Periksa header auth webhook.
3. Verifikasi URL production webhook, bukan test webhook yang tidak aktif.
4. Korelasikan log STT dan execution n8n menggunakan waktu/trace ID.

### SLM menjawab teks tanpa tool call

1. Pastikan prompt, chat template, dan schema tool sesuai kontrak training.
2. Periksa backend endpoint dan mode native tool call.
3. Bandingkan HF dan GGUF menggunakan frozen input yang sama.
4. Jangan menganggap teks aksi sebagai aktuasi berhasil pada strict evaluation.

### Home Assistant tidak berubah

1. Periksa apakah workflow berada pada dry-run.
2. Periksa hasil validator dan entity allowlist.
3. Verifikasi service/domain serta payload data.
4. Baca kembali state dan observasi perangkat fisik.

### Jawaban suara tidak terdengar

1. Pastikan TTS mengembalikan WAV non-empty.
2. Periksa shared output path dan permission.
3. Periksa journal audio player serta ALSA device.
4. Jangan mengulang aktuasi hanya untuk memperbaiki audio.

## Evidence insiden

Simpan waktu, komponen, gejala, request ID, status health, dan tindakan pemulihan. Sensor token, credential, IP privat, dan isi query pengguna sebelum evidence dibagikan.
