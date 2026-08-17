# Home Assistant

## Peran Home Assistant

Home Assistant menyimpan status perangkat dan menjadi satu-satunya jalur untuk mengendalikan perangkat pada prototipe. SLM tidak menerima kredensial dan tidak memanggil API Home Assistant secara langsung.

## Membaca Status Perangkat

n8n mengambil status dan atribut, lalu memilih hanya perangkat yang tercantum dalam inventaris. Informasi yang dikirim ke model membedakan:

- `on`, `off`, dan `unavailable`.
- Nilai sensor beserta unitnya.
- Brightness, warna, dan color temperature aktual.
- Target suhu dan mode AC.

Nilai yang tidak tersedia tidak boleh diganti dengan angka buatan karena dapat membuat model salah mengira kondisi perangkat sudah sesuai.

## Mengendalikan Perangkat

| Proposal logis | Bentuk eksekusi |
| --- | --- |
| Menyalakan atau mematikan | Layanan sesuai jenis perangkat |
| Mengatur tingkat terang, warna, atau suhu warna | Layanan lampu dengan satu perubahan yang telah diperiksa |
| Mengatur suhu AC | Layanan AC dengan rentang aman |
| Beberapa perubahan yang telah ditentukan | Scene Home Assistant |

## Verifikasi

Respons API menunjukkan bahwa Home Assistant menerima perintah. Untuk memastikan perubahan benar-benar terjadi, perangkat perlu diamati atau statusnya dibaca kembali setelah aktuasi.
