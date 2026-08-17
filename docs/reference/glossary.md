# Glosarium

## Istilah sistem

| Istilah | Definisi |
| --- | --- |
| Already-state | Kondisi ketika state perangkat sudah memenuhi tujuan sehingga tidak perlu aktuasi |
| Behavioral accuracy | Proporsi keputusan yang memenuhi goal-condition atau aturan no-tool |
| Core node | Perangkat utama yang menjalankan service inference dan orkestrasi |
| Dry-run | Eksekusi workflow tanpa memanggil Home Assistant |
| False execution | Aktuasi yang diusulkan pada contoh yang seharusnya no-tool |
| Frozen test | Holdout final yang tidak digunakan untuk training atau tuning evaluator |
| GGUF | Format model untuk runtime llama.cpp dan deployment quantized |
| Goal-condition | Kondisi keberhasilan yang ditetapkan sebelum inferensi |
| Native tool call | Struktur function call yang dihasilkan model, bukan teks aksi biasa |
| No-tool | Keputusan untuk menjawab tanpa memanggil aktuator |
| Orkestrator | Lapisan yang menghubungkan state, model, validator, executor, dan output |
| Q4_K_M | Skema kuantisasi 4-bit GGUF yang digunakan untuk deployment ringan |
| SLM | Small Language Model untuk domain terbatas |
| Voice satellite | Perangkat edge untuk wake word, capture audio, dan LED status |
| Wake word | Kata aktivasi lokal; pada prototipe menggunakan “Omega” |

## Istilah evaluasi

| Istilah | Definisi |
| --- | --- |
| Tool exact match | Nama tool dan seluruh argumen sama dengan reference |
| Schema-valid execution | Tool call memenuhi schema dan rentang kanonik |
| No-tool accuracy | Proporsi contoh no-tool yang tidak menghasilkan tool call |
| BERTScore | Kemiripan semantik teks; tidak membuktikan aktuasi berhasil |
| Development split | Split untuk monitoring dan pemilihan checkpoint |
| Frozen split | Split final untuk klaim evaluasi yang dikunci |
