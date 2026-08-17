# Glosarium

## Istilah Sistem

| Istilah | Definisi |
| --- | --- |
| Already-state | Kondisi ketika status perangkat sudah sesuai sehingga tidak perlu aktuasi |
| Behavioral accuracy | Persentase keputusan yang memenuhi tujuan atau aturan tanpa pemanggilan fungsi |
| Core node | Komputer utama yang menjalankan STT, SLM, n8n, dan TTS |
| Dry-run | Mode pengujian alur tanpa memanggil Home Assistant |
| False execution | Aktuasi yang muncul pada contoh yang seharusnya tidak menjalankan perangkat |
| Frozen test | Data uji akhir yang tidak digunakan untuk training atau penyesuaian evaluator |
| GGUF | Format model yang digunakan oleh llama.cpp untuk menjalankan model secara efisien |
| Goal-condition | Kondisi yang harus tercapai agar keputusan dianggap berhasil |
| Native tool call | Struktur pemanggilan fungsi yang dihasilkan model, bukan sekadar teks aksi |
| No-tool | Keputusan untuk menjawab tanpa memanggil aktuator |
| Orkestrator | Bagian yang menghubungkan status perangkat, model, pemeriksaan hasil, eksekusi, dan jawaban |
| Q4_K_M | Skema kuantisasi 4-bit GGUF untuk menjalankan model dengan penggunaan memori lebih kecil |
| SLM | Small Language Model untuk domain terbatas |
| Voice satellite | Perangkat suara untuk mendeteksi wake word, merekam audio, dan menampilkan status LED |
| Wake word | Kata aktivasi lokal; pada prototipe menggunakan “Omega” |

## Istilah Evaluasi

| Istilah | Definisi |
| --- | --- |
| Tool exact match | Nama fungsi dan seluruh argumennya sama dengan jawaban acuan |
| Schema-valid execution | Pemanggilan fungsi memenuhi skema dan rentang nilai yang ditentukan |
| No-tool accuracy | Persentase contoh tanpa aksi yang tidak menghasilkan pemanggilan fungsi |
| BERTScore | Kemiripan semantik teks; tidak membuktikan aktuasi berhasil |
| Development split | Bagian data untuk memantau dan memilih checkpoint selama pengembangan |
| Frozen split | Bagian data uji akhir yang dikunci dan tidak digunakan untuk perbaikan model |
