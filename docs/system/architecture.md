# Arsitektur Sistem

## Konteks Sistem

SmartLab membagi pekerjaan ke beberapa perangkat. Raspberry Pi menangani input suara, komputer utama menjalankan STT, n8n, SLM, dan TTS, sedangkan Home Assistant menghubungkan sistem dengan perangkat laboratorium. Training dilakukan pada komputer GPU yang terpisah dan tidak ikut menangani permintaan sehari-hari.

```mermaid
flowchart LR
    accTitle: Arsitektur Tingkat Tinggi SmartLab
    accDescr: Aliran utama dari pengguna menuju perangkat suara, layanan pemrosesan lokal, Home Assistant, perangkat laboratorium, dan jawaban audio

    user([Pengguna]) --> satellite[Perangkat suara]
    satellite --> stt[Whisper STT]
    stt --> orchestrator[Orkestrasi n8n]
    orchestrator <--> slm[SLM lokal]
    orchestrator <--> ha[Home Assistant]
    ha --> devices[Perangkat laboratorium]
    orchestrator --> tts[Piper TTS]
    tts --> speaker([Speaker lokal])

    classDef edge fill:#ede9fe,stroke:#7c3aed,stroke-width:2px,color:#3b0764
    classDef service fill:#dbeafe,stroke:#2563eb,stroke-width:2px,color:#1e3a5f
    classDef physical fill:#dcfce7,stroke:#16a34a,stroke-width:2px,color:#14532d

    class user,satellite edge
    class stt,orchestrator,slm,tts service
    class ha,devices,speaker physical
```

## Topologi Fisik

<figure markdown="span">
  ![Topologi fisik SmartLab](../assets/diagrams/deployment-topology.png)
  <figcaption>Penempatan Raspberry Pi, komputer utama, Home Assistant, penyimpanan n8n, dan komputer training.</figcaption>
</figure>

!!! info "Inventaris terverifikasi"
    Label **Raspberry Pi 3B** pada gambar sudah benar. Perangkat aktif teridentifikasi sebagai **Raspberry Pi 3 Model B Rev 1.2** melalui `/proc/device-tree/model`.

## Peran Setiap Perangkat

| Node | Peran utama | Komponen |
| --- | --- | --- |
| Perangkat suara | Merekam audio dan menampilkan status proses | ReSpeaker 2-Mic, OpenWakeWord Omega, LED status |
| Komputer utama | Menjalankan pemrosesan suara dan pengambilan keputusan | STT, n8n, PostgreSQL, llama-server, Piper, pemutar audio |
| Home Assistant | Membaca status dan mengendalikan perangkat | Home Assistant Core dan integrasi perangkat |
| Komputer training | Melatih dan mengevaluasi model secara terpisah | Unsloth, evaluator, llama.cpp, ekspor GGUF |
