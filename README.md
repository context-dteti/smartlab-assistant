# SmartLab Documentation Web

Dokumentasi publik prototipe SmartLab berbasis Markdown dan Material for MkDocs.

## Menjalankan secara lokal

```bash
python3 -m venv .venv
source .venv/bin/activate
python -m pip install -r requirements.txt
mkdocs serve
```

Buka `http://127.0.0.1:8000`. Pemeriksaan sebelum publikasi:

```bash
mkdocs build --strict
```

## Publikasi GitHub Pages

1. Buat repository GitHub baru, misalnya `smartlab-docs`.
2. Push isi direktori ini ke branch `main`.
3. Buka **Settings → Pages → Source → GitHub Actions**.
4. Workflow `.github/workflows/docs.yml` akan membangun dan menerbitkan situs.

Ganti placeholder `repo_url`, `site_url`, dan identitas pengelola pada `mkdocs.yml` sebelum publikasi.

## Batas publikasi

Jangan menambahkan token, password, IP internal, credential ID n8n, file `.env`, dump database, raw snapshot Home Assistant, log produksi, atau workflow export yang memuat konfigurasi operasional.
