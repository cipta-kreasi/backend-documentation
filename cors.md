# 📌 Konfigurasi CORS dengan Kong Plugin

## 🎯 Pendahuluan
Cross-Origin Resource Sharing (CORS) adalah mekanisme keamanan yang membatasi bagaimana sumber daya di suatu domain dapat diakses oleh halaman web dari domain lain. Dalam hal ini, kita akan mengaktifkan CORS menggunakan Kong API Gateway.

---

## ⚙️ Mengaktifkan Plugin CORS di Kong

### 1️⃣ **Aktifkan Plugin CORS untuk Route**
Jalankan perintah berikut untuk menambahkan plugin CORS ke route tertentu di Kong:

```sh
curl -X POST http://localhost:8001/routes/YOUR_ROUTE_ID/plugins \
  --data "name=cors" \
  --data "config.origins=<origin fe>" \
  --data "config.methods[]=GET" \
  --data "config.methods[]=POST" \
  --data "config.methods[]=OPTIONS" \
  --data "config.methods[]=PUT" \
  --data "config.methods[]=DELETE" \
  --data "config.headers[]=Content-Type" \
  --data "config.headers[]=Authorization" \
  --data "config.credentials=true" \
  --data "config.preflight_continue=true"
```

Gantilah `YOUR_ROUTE_ID` dengan ID route yang ingin dikonfigurasi, serta `<origin fe>` dengan domain frontend yang diizinkan (misalnya `https://example.com`).

### 2️⃣ **Cek ID Route**
Jika belum mengetahui ID route, gunakan perintah berikut untuk melihat daftar layanan yang tersedia:

```sh
curl -i -s -X GET http://localhost:8001/services
```

Cari ID route yang sesuai dengan layanan yang ingin dikonfigurasi.

---

## 🔄 Memperbarui Konfigurasi CORS
Jika plugin CORS sudah diaktifkan sebelumnya, gunakan perintah berikut untuk memperbarui konfigurasi metode HTTP yang diizinkan:

```sh
curl -X PATCH http://localhost:8001/routes/YOUR_ROUTE_ID/plugins \
  --data "config.methods[]=POST" \
  --data "config.methods[]=GET" \
  --data "config.methods[]=PUT" \
  --data "config.methods[]=DELETE" \
  --data "config.methods[]=PATCH" \
  --data "config.methods[]=OPTIONS"
```

Gantilah `YOUR_ROUTE_ID` dengan ID route yang sesuai.

---

## 🔎 Verifikasi Konfigurasi
Untuk memastikan bahwa konfigurasi sudah berhasil diterapkan, jalankan perintah berikut:

```sh
curl -i -s -X GET http://localhost:8001/routes/YOUR_ROUTE_ID/plugins
```

Jika konfigurasi berhasil, Anda akan melihat plugin CORS dengan pengaturan yang telah ditentukan.

---
