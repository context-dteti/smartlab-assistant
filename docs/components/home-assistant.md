# Home Assistant

## Peran gateway IoT

Home Assistant menjadi sumber state perangkat dan satu-satunya gateway aktuasi pada prototipe. Local SLM tidak mengetahui credential maupun memanggil API Home Assistant secara langsung.

## Pembacaan state

n8n mengambil state dan atribut, lalu memfilter hanya entitas yang tercantum pada inventaris logis. Konteks yang dikirim ke model sebaiknya membedakan:

- `on`, `off`, dan `unavailable`.
- Nilai sensor beserta unitnya.
- Brightness, warna, dan color temperature aktual.
- Target temperature dan mode HVAC.

Nilai yang tidak tersedia tidak boleh diam-diam diganti dengan angka sintetis karena dapat mengubah keputusan already-state.

## Aktuasi

| Proposal logis | Bentuk eksekusi |
| --- | --- |
| Turn on/off | Service domain entity |
| Atur brightness/warna/color temperature | Service lampu dengan satu perubahan yang tervalidasi |
| Atur suhu AC | Service climate dengan rentang aman |
| Mode gabungan tertentu | Scene yang dipetakan pada executor |

## Verifikasi

Respons API menunjukkan bahwa Home Assistant menerima service call. Untuk klaim keberhasilan fisik, pengujian demonstrasi perlu mengamati perangkat atau membaca state sesudah aktuasi.

!!! info "Screenshot yang dibutuhkan"
    Tambahkan dashboard Home Assistant yang hanya menampilkan entitas SmartLab. Hindari menu credential, token, alamat internal, dan integrasi administratif.
