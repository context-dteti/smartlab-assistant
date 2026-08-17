# Deployment dan Rollback

## Prinsip deployment

Deployment model harus menjadi perubahan kecil, dapat diverifikasi, dan dapat dibatalkan. Mengganti model tidak semestinya mengubah endpoint, credential, workflow n8n, STT, TTS, atau Home Assistant pada saat yang sama.

## Artifact yang dipromosikan

Satu paket kandidat sekurang-kurangnya memuat:

- File GGUF dengan nama stabil.
- Manifest provenance dan checksum SHA-256.
- Konfigurasi conversion/quantization.
- Metrics frozen test HF dan Q4 yang terpisah.
- Hasil preflight `llama-server` dan smoke test.
- Catatan model sebelumnya untuk rollback.

## Urutan promosi

1. Verifikasi checksum artifact sumber dan tujuan.
2. Jalankan preflight load tanpa mengubah service aktif.
3. Backup unit service dan catat path model lama.
4. Ubah hanya path model pada konfigurasi service.
5. Reload systemd dan restart layanan inference.
6. Periksa health endpoint serta log load GPU.
7. Jalankan dry-run explicit, status, implicit, already-state, dan refusal.
8. Jalankan smoke test fisik terkontrol.
9. Pantau false execution, rejection, latensi, dan respons audio.

## Rollback konseptual

```text
1. Hentikan penerimaan request baru.
2. Pulihkan unit service yang menunjuk model stabil sebelumnya.
3. Reload systemd dan restart inference service.
4. Verifikasi health serta checksum model aktif.
5. Jalankan smoke test read-only dan satu aktuasi aman.
6. Catat alasan rollback dan evidence regresi.
```

Perintah konkret, alamat host, username, dan path internal disimpan pada runbook privat, bukan dokumentasi web publik.

## Kondisi yang memicu rollback

- Model gagal dimuat atau health check tidak stabil.
- Native tool call turun jauh dari baseline yang disetujui.
- Terjadi false execution pada uji safety.
- Validator menerima argumen di luar kontrak.
- Latensi atau penggunaan memori mengganggu service lain.
- TTS gagal dan menimbulkan pengulangan alur yang tidak aman.

## Backup

Backup sebelum perubahan infrastruktur harus mencakup konfigurasi service, workflow n8n, database n8n, manifest model, dan konfigurasi environment tanpa menyalin nilai secret ke dokumentasi publik.
