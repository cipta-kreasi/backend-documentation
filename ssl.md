# 🔒 Konfigurasi SSL di Kong

## 🎯 Pendahuluan
SSL (Secure Sockets Layer) digunakan untuk mengenkripsi komunikasi antara klien dan server, memastikan keamanan data. Kong mendukung SSL dan memungkinkan pengelolaannya melalui API.

Secara default, SSL di Kong akan diperbarui otomatis setiap **3 bulan**. Anda dapat mengecek jadwalnya melalui **crontab** atau memperbaruinya secara manual jika diperlukan.

---

## 🔄 Mengecek Jadwal Pembaruan Otomatis
Jalankan perintah berikut untuk melihat jadwal pembaruan otomatis SSL:

```sh
crontab -e
```

---

## 🛠 Memperbarui SSL Secara Manual
Jika ingin memperbarui SSL secara manual, Anda bisa menjalankan skrip berikut:

```sh
cd /root/documentation/ssl/
./ssl-renew.sh
```

Skrip ini akan memperbarui sertifikat SSL secara manual.

---

## ⚙️ Mengatur SSL Secara Manual
Jika ingin mengatur SSL secara manual, ikuti langkah-langkah berikut:

### 1️⃣ **Hasilkan Sertifikat dan Kunci SSL**
Pastikan Anda memiliki file **.cert** dan **.key** yang valid sebelum menggunakannya di Kong.

### 2️⃣ **Cek ID SSL yang Sudah Ada**
Sebelum mengubah SSL, cek daftar sertifikat yang ada dengan perintah:

```sh
curl -s http://localhost:8001/certificates | jq
```

### 3️⃣ **Hapus Sertifikat SSL Lama**
Jika perlu menghapus sertifikat SSL lama sebelum menggantinya, jalankan:

```sh
curl -i -X DELETE http://localhost:8001/certificates/<id ssl>
```

Gantilah `<id ssl>` dengan ID sertifikat yang ingin dihapus.

### 4️⃣ **Menambahkan Sertifikat SSL Baru**
Setelah memiliki sertifikat dan kunci SSL baru, daftarkan ke Kong dengan perintah berikut:

```sh
curl -i -X POST http://localhost:8001/certificates \
  --form "cert=@config.crt" \
  --form "key=@config.key"
```

Pastikan file **config.crt** dan **config.key** sesuai dengan sertifikat yang ingin Anda gunakan.

### 5️⃣ **Menetapkan SSL ke Domain (SNI Mapping)**
Setelah sertifikat berhasil diunggah, hubungkan dengan domain menggunakan perintah berikut:

```sh
curl -i -X POST http://localhost:8001/snis \
  --data "name=api.lakukan.co.id" \
  --data "certificate.id=<new id>"
```

Gantilah `<new id>` dengan ID sertifikat SSL yang baru saja Anda tambahkan.

---


