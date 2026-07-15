# Modul 5.3 (Opsional) – Sekilas Deploy Full-Stack

> **Modul ini opsional dan bersifat pengenalan.** Kalau portofolio kamu hanya halaman statis (HTML/CSS/JS, React, atau Next.js tanpa backend), **Modul 5.2 sudah cukup** — website kamu sudah live. Modul ini hanya untuk kamu yang portofolionya punya **backend + database** dan penasaran cara deploy-nya.

Tujuan modul ini bukan tutorial lengkap, tapi memberi **gambaran** cara kerja deploy full-stack supaya kamu tahu arahnya. Detail teknisnya bisa kamu dalami sendiri lewat dokumentasi resmi.

---

## 1. Konsep: Tiga Bagian, Tempat Berbeda

Website statis cukup deploy di **satu** tempat (Vercel). Aplikasi full-stack punya **tiga bagian**, dan biasanya deploy ke tempat berbeda:

| Bagian | Deploy ke |
| --- | --- |
| **Frontend** (tampilan) | Vercel (seperti Modul 5.2) |
| **Backend** (Express API) | Railway |
| **Database** | Railway (PostgreSQL) |

Cara mereka terhubung:
```
Frontend (Vercel) → Backend API (Railway) → Database (Railway)
```

Frontend memanggil backend lewat **URL API**-nya. Backend membaca/menulis ke database.

---

## 2. Satu Hal Penting: SQLite → PostgreSQL

Di Modul 4 kita pakai **SQLite** (file `dev.db`). SQLite bagus untuk belajar, tapi **tidak bisa dipakai di server cloud** — file-nya bisa hilang setiap kali aplikasi restart, artinya data user bisa lenyap.

Solusinya: ganti ke **PostgreSQL** (database gratis dari Railway). Karena kita pakai **Prisma**, perubahannya cuma di satu tempat:
```
datasource db {

provider = “postgresql”   // sebelumnya “sqlite”

url      = env(“DATABASE_URL”)

}
```

Model Prisma kamu tidak perlu diubah. Inilah kelebihan pakai ORM.

---

## 3. Langkah Garis Besar

Kalau kamu mau deploy full-stack, ini alurnya secara umum:

1. **Ganti database ke PostgreSQL** di `schema.prisma` (lihat Bagian 2).
2. **Siapkan backend**: pakai `process.env.PORT`, aktifkan CORS (`npm install cors`), pastikan ada script `start` di `package.json`.
3. **Deploy backend ke Railway**: login dengan GitHub → New Project → deploy dari repo → tambahkan database PostgreSQL → jalankan migration.
4. **Ambil URL backend** dari Railway (misal `https://api-ku.up.railway.app`).
5. **Sambungkan frontend**: ganti alamat API di frontend dari `localhost` ke URL Railway, lalu `git push` (Vercel auto-deploy).

Setelah itu, frontend (Vercel), backend, dan database (Railway) sudah terhubung dan live.

---

## 4. Mau Mendalami? Ini Sumbernya

Deploy full-stack punya banyak detail. Kalau kamu serius mencobanya, ini referensi terbaik:

- **Dokumentasi Railway** — [docs.railway.app](https://docs.railway.app) (cara deploy Node.js & setup PostgreSQL).
- **Dokumentasi Prisma** — [prisma.io/docs](https://www.prisma.io/docs) (migrasi database & deploy).
- **Tanya mentor** saat sesi — bagian ini paling enak dibahas langsung.

---

## 5. Ringkasan Modul 5.3

- Full-stack punya **tiga bagian**: frontend (Vercel), backend & database (Railway).
- **SQLite harus diganti PostgreSQL** saat deploy — cukup ubah satu baris di Prisma.
- Alurnya: siapkan backend → deploy ke Railway → sambungkan frontend lewat URL API.
- Detail lengkapnya ada di dokumentasi resmi Railway & Prisma.

Untuk Final Project berupa portofolio, **Modul 5.2 sudah lebih dari cukup**. Modul ini hanya bekal kalau suatu saat kamu membangun aplikasi dengan backend sendiri. 🚀

---


