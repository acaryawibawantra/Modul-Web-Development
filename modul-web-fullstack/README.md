# Modul 4 – Full-Stack Web App: Database & Integrasi

Modul ini adalah lanjutan dari Modul 3 (Web Backend). Di sini kamu akan belajar menyimpan data ke **database**, mengintegrasikan database ke **REST API**, dan menghubungkan semuanya dengan **frontend Next.js** menjadi aplikasi full-stack.

Study case: **Event Registration App** — aplikasi pendaftaran event GDGoC ITS.

## Daftar Materi

| Modul | Topik | Deskripsi |
| --- | --- | --- |
| 4.1 | **[Pengenalan Database & Prisma ORM](modul-4-1-database-prisma.md)** | Konsep database, SQL vs NoSQL, setup SQLite + Prisma, operasi CRUD lewat kode |
| 4.2 | **[REST API + Database (Express + Prisma)](modul-4-2-rest-api-database.md)** | Upgrade REST API Modul 3.3 agar baca/tulis ke database, endpoint Event & Participant |
| 4.3 | **[Full-Stack Integration (Next.js + API)](modul-4-3-fullstack-integration.md)** | Frontend Next.js yang fetch data dari API, form registrasi, loading & error handling |

## Prasyarat

Sebelum memulai Modul 4, pastikan kamu sudah menyelesaikan:

- **Modul 2** — Pengenalan React & Next.js
- **Modul 3** — Node.js, npm, dan REST API Express

## Hasil Akhir

Setelah menyelesaikan Modul 4, kamu akan punya:

- Database SQLite dengan tabel `Event` dan `Participant`
- REST API Express yang CRUD ke database (data persisten)
- Frontend Next.js dengan halaman daftar event, detail event, dan form registrasi
- Kedua bagian terhubung dan berjalan sebagai satu aplikasi full-stack
