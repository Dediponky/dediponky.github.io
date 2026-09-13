# AI Forex Trading Bot Orchestrator — Dashboard

Repo ini adalah **situs statis** (GitHub Pages) untuk dashboard "AI Forex Trading Bot
Orchestrator": dashboard publik (status bot, performa, riwayat trading) dan dashboard
admin (kontrol AI Agent, follower, dsb). Backend (Google Apps Script) dan dokumentasi
arsitektur lengkap disimpan terpisah di project pengembangan (tidak ikut dipublish ke
sini karena berisi source backend, bukan bagian dari situs).

## Isi repo

```
index.html      ← dashboard publik (status bot, statistik, histori trading, login/kontak)
admin/          ← dashboard admin (switch AI, setting provider AI/Telegram, CRUD follower)
```

## Konfigurasi wajib sebelum situs berfungsi

Kedua halaman butuh **URL Web App Google Apps Script** (backend) yang sudah dideploy:

- `index.html`: cari konstanta `GAS_WEB_APP_URL` di bagian atas blok `<script>`, isi
  dengan URL backend (diakhiri `/exec`). Selama kosong, dashboard menampilkan banner
  peringatan dan tidak melakukan fetch data.
- `admin/index.html`: URL backend **tidak** ditulis di kode, tapi diisi manual sekali
  lewat layar "Masuk sebagai Admin" (disimpan di `localStorage` browser), sekalian
  dengan `ADMIN_TOKEN` untuk otentikasi.

Tidak ada API key/token AI, Telegram, atau EA yang pernah ditulis di file-file ini —
semua secret disimpan di backend (Script Properties Google Apps Script), sesuai desain
keamanan project (frontend statis, backend yang menjembatani semua data sensitif).

## Catatan keamanan folder `/admin`

Halaman admin memang publik secara URL (GitHub Pages tidak punya proteksi akses
bawaan), tapi setiap aksi tulis (ubah config, CRUD follower) divalidasi `ADMIN_TOKEN`
di backend — siapa pun tanpa token yang benar tidak bisa mengubah apa pun, hanya bisa
melihat halaman kosong meminta login. Tetap jangan sebar-luaskan `ADMIN_TOKEN`.
