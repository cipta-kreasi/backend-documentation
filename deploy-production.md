# 🚀 Panduan Deploy ke Production

## Deploy otomatis

jalankan script berikut di root project

```sh
./scripts/push.sh
```

## 🔨 Langkah-Langkah Deploy manual

### 1️⃣ **Membangun Docker Image**
Jalankan perintah berikut untuk membuat image Docker:

```sh
docker build . -t lakukan/business --platform linux/amd64
```

### 2️⃣ **Menambahkan Tag ke Image**
Tambahkan tag ke image yang telah dibuat agar bisa diunggah ke Docker Hub:

```sh
docker tag lakukan/business hesdevcorp/<name-service>
```

### 3️⃣ **Push Image ke Docker Hub**
Unggah image ke Docker Hub dengan perintah:

```sh
docker push hesdevcorp/lakukan-business
```

### 4️⃣ **Login ke Server**
Akses server tempat aplikasi akan dijalankan:

```sh
ssh user@server-ip
```

### 5️⃣ **Pull Image yang Diperbarui**
Setelah login ke server, unduh image terbaru dari Docker Hub:

```sh
docker pull hesdevcorp/lakukan-business:latest
```

### 6️⃣ **Jalankan Docker Compose**
Masuk ke direktori **lakukan-production/** dan jalankan perintah berikut:

```sh
cd lakukan-production/
docker-compose -f docker-compose.production.yml up -d --no-deps --force-recreate <name-service>
```

Gantilah `<name-service>` dengan nama layanan yang ingin diperbarui.

---


