# 🚀 Laravel 11 Dockerized Starter Template

Template ini menyediakan lingkungan pengembangan Laravel 11 berbasis **Docker** dengan konfigurasi lengkap, cocok untuk pengembangan lokal maupun on-premise server.

---

## 📦 Stack yang Digunakan

-   PHP 8.3 (FPM)
-   Laravel 11
-   MySQL 5.7
-   Redis
-   Nginx (Alpine)
-   Mailpit (SMTP testing)
-   phpMyAdmin
-   Supervisor (untuk PHP-FPM + Queue Worker + Horizon)

---

## 🛠️ Cara Menggunakan

1. Clone atau Buat Project Laravel

```bash
composer create-project laravel/laravel:^11 cmms-app
cd cmms-ap
```

2. Salin File Konfigurasi Docker

Pastikan struktur file kamu seperti berikut:

```bash
cmms-app/
├── Dockerfile
├── docker-compose.yml
├── supervisord.conf
├── storage/
│   ├── php.ini
│   └── app.conf
```

Jika folder storage/ belum ada, buat manual lalu tambahkan php.ini dan app.conf. 3. Jalankan Docker

```bash
docker compose up -d --build
```

4. Akses Aplikasi
   Layanan URL
   Laravel App http://localhost:8081
   phpMyAdmin http://localhost:7001
   Mailpit http://localhost:8025
5. Jalankan Artisan Command

```bash
docker compose exec app php artisan migrate
docker compose exec app php artisan key:generate
```

6. Konfigurasi .env Laravel

```bash
APP_NAME=CMMS
APP_ENV=local
APP_KEY=base64:...
APP_DEBUG=true
APP_URL=http://localhost:8081

DB_CONNECTION=mysql
DB_HOST=db
DB_PORT=3306
DB_DATABASE=cmms
DB_USERNAME=root
DB_PASSWORD=cmmsapp

REDIS_HOST=redis

QUEUE_CONNECTION=redis
CACHE_DRIVER=redis
SESSION_DRIVER=redis

MAIL_MAILER=smtp
MAIL_HOST=mailpit
MAIL_PORT=1025
MAIL_FROM_ADDRESS=no-reply@cmms.local
```

👷 Service Supervisor

Supervisor akan menjalankan 3 service utama secara paralel:

-   php-fpm
-   php artisan queue:work
-   php artisan horizon

Log Output:

/storage/logs/queue.log
/storage/logs/horizon.log

📌 Tips Tambahan

Rebuild semua container:

```bash
docker compose down -v
docker compose up -d --build
```

Bersihkan cache konfigurasi Laravel:

```bash
docker compose exec app php artisan optimize:clear
```

🧾 License

MIT License – bebas digunakan dan dimodifikasi untuk kebutuhan proyek pribadi maupun komersial.
✨ Credits

Dibuat dengan ❤️ oleh Ali Musthofa Baharudin
Program Studi Teknologi Rekayasa Informatika Industri
Politeknik Manufaktur Bandung – 2025
