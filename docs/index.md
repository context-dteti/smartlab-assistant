# SmartLab Private Voice Assistant

<p class="hero-copy">
SmartLab adalah prototipe asisten suara Bahasa Indonesia untuk pengendalian dan pemantauan perangkat laboratorium. Pemrosesan suara, pengambilan keputusan, dan sintesis jawaban berjalan pada infrastruktur milik laboratorium dengan integrasi Home Assistant.
</p>

## Kemampuan Utama

- Aktivasi tanpa sentuhan melalui wake word **Omega**.
- Transkripsi ucapan Bahasa Indonesia secara lokal.
- Pemahaman perintah eksplisit dan keluhan kontekstual terbatas.
- Pemeriksaan state perangkat sebelum menentukan aksi.
- Validasi deterministik sebelum aktuasi Home Assistant.
- Jawaban suara menggunakan Text-to-Speech lokal.

## Gambaran Sistem

<figure markdown="span">
  ![Konteks sistem SmartLab](assets/diagrams/system-context.png)
  <figcaption>Alur utama dari pengguna, perangkat suara, pemrosesan lokal, Home Assistant, hingga jawaban melalui speaker.</figcaption>
</figure>

## Urutan Membaca

1. Mulai dari [Gambaran umum](getting-started/overview.md).
2. Pahami [Arsitektur](system/architecture.md) dan [Alur runtime](system/runtime-flow.md).
3. Buka [Orkestrasi n8n](components/n8n.md) untuk fungsi setiap node.
4. Gunakan [Deployment dan rollback](operations/deployment.md) saat mengoperasikan prototipe.
5. Periksa [Dataset dan evaluasi](models/dataset-evaluation.md) sebelum mengutip hasil riset.

## Batas Dokumentasi Publik

Dokumentasi ini menjelaskan desain dan perilaku prototipe tanpa memuat password, token, alamat IP internal, credential ID, dump database, atau konfigurasi rahasia. Nilai operasional sensitif disimpan terpisah dan hanya tersedia bagi personel berwenang.

---

_Status dokumentasi: draf publik, 17 Agustus 2026._
