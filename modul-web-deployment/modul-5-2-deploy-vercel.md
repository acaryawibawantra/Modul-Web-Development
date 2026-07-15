# Modul 5.2 – Deploy ke Vercel

Di modul ini kamu akan **men-deploy website portofolio kamu ke Vercel** sampai benar-benar **live** dan punya URL publik yang bisa dibagikan ke siapa saja.

Fokusnya:

- Menghubungkan akun **GitHub** ke **Vercel**.
- Meng-import dan men-deploy project (baik statis maupun Next.js).
- Mendapatkan **URL publik** website kamu.
- Memahami **auto-deploy** — update otomatis tiap kali `git push`.

Target akhirnya: website portofolio kamu **live di internet**. 🎉

> **Prasyarat:** project sudah di-push ke GitHub (lihat Modul 5.1).

---

## 1. Banyak Pilihan Tempat Deploy

Sebelum masuk ke praktik, penting untuk tahu: **Vercel bukan satu-satunya tempat deploy.** Ada banyak platform, dan masing-masing punya kelebihan. Umumnya dibagi berdasarkan apa yang mau di-deploy.

**Platform untuk Frontend (website & tampilan):**

| Platform | Cocok untuk | Catatan |
| --- | --- | --- |
| **Vercel** | Statis, React, Next.js | Paling mulus untuk Next.js. Kita pakai ini. |
| **Netlify** | Statis, React | Mirip Vercel, sama-sama mudah. |
| **Cloudflare Pages** | Statis, React | Cepat, jaringan global besar. |
| **GitHub Pages** | Statis (HTML/CSS/JS) | Gratis, langsung dari repo GitHub. |

**Platform untuk Backend (server & API):**

| Platform | Cocok untuk | Catatan |
| --- | --- | --- |
| **Railway** | Node.js/Express + database | Backend & database jadi satu. |
| **Render** | Node.js/Express + database | Punya tier gratis. |
| **Fly.io** | Aplikasi server | Fleksibel, sedikit lebih teknis. |

### Frontend dan Backend bisa terpisah

Pada aplikasi **full-stack**, frontend dan backend sering **di-deploy di platform berbeda** — misal frontend di Vercel, backend di Railway. Keduanya lalu **disambungkan**: frontend memanggil backend lewat **URL API**-nya.
```
Frontend (Vercel)  ──── memanggil ────▶  Backend API (Railway)

https://situsku.vercel.app              https://api-ku.up.railway.app
```

Selama URL backend-nya benar dan backend mengizinkan akses (CORS), keduanya terhubung mulus meski berada di server yang berbeda.

### Kenapa workshop ini pakai Vercel?

- **Gratis** untuk personal project.
- **Mudah** — connect GitHub, pilih repo, deploy. Tanpa setting server.
- **Cepat** — website disebar ke banyak server dunia (CDN).
- **Support Next.js terbaik** (Vercel yang membuat Next.js).

Karena Final Project kita adalah **web portofolio** (umumnya frontend saja), Vercel adalah pilihan paling praktis. Mulai sekarang kita fokus deploy ke Vercel.

> **Catatan:** Kalau portofolio kamu punya **backend + database**, cara deploy full-stack lengkap (backend + PostgreSQL di Railway, lalu disambungkan ke frontend) dibahas terpisah di **Modul 5.3**.

---

## 2. Buat Akun Vercel

1. Buka [vercel.com](https://vercel.com).
2. Klik **Sign Up**.
3. Pilih **Continue with GitHub** — ini penting supaya Vercel langsung terhubung ke repo kamu.
4. Izinkan (authorize) Vercel mengakses akun GitHub kamu.

Selesai. Sekarang Vercel sudah bisa "melihat" repository di GitHub kamu.

---

## 3. Import Project dari GitHub

1. Di dashboard Vercel, klik **Add New...** → **Project**.
2. Vercel menampilkan daftar repository GitHub kamu.
3. Cari repo portofolio kamu (misal `portofolio`) → klik **Import**.

> Kalau repo tidak muncul, klik **Adjust GitHub App Permissions** dan beri akses Vercel ke repo tersebut.

---

## 4. Konfigurasi & Deploy

Setelah import, Vercel menampilkan halaman konfigurasi. Yang perlu kamu lakukan tergantung jenis project:

### 4.1. Kalau project statis (HTML/CSS/JS biasa)

- **Framework Preset**: pilih **Other** (atau biarkan Vercel deteksi otomatis).
- Biarkan setting lain default.
- Klik **Deploy**.

### 4.2. Kalau project React (Vite)

- **Framework Preset**: Vercel biasanya auto-detect **Vite**.
- **Build Command**: `npm run build`
- **Output Directory**: `dist`
- Klik **Deploy**.

### 4.3. Kalau project Next.js

- **Framework Preset**: Vercel auto-detect **Next.js** (tidak perlu diubah apa-apa).
- Semua setting sudah otomatis benar.
- Klik **Deploy**.

Sekarang tunggu beberapa saat — Vercel sedang **build** website kamu. Kamu bisa lihat prosesnya berjalan (install dependencies → build → deploy).

---

## 5. Website Kamu Live! 🎉

Kalau berhasil, Vercel menampilkan **halaman selamat** dengan preview website kamu dan sebuah URL, misal:
https://portofolio-budi.vercel.app

Klik URL itu — **website portofolio kamu sekarang online dan bisa diakses siapa saja!**

Coba:
- Buka URL-nya di HP kamu.
- Kirim ke teman dan minta mereka buka.

Itu bukan `localhost` lagi — itu **website beneran di internet**. Selamat! 🚀

---

## 6. Auto-Deploy: Update Otomatis Tiap Push

Ini fitur paling keren dari Vercel.

Website kamu sekarang **terhubung ke repo GitHub**. Setiap kali kamu update kode dan push:
```
git add .

git commit -m “update bagian about”

git push
```

Vercel akan **otomatis mendeteksi perubahan** dan **men-deploy ulang** website dengan versi terbaru — tanpa kamu klik apa-apa. Dalam beberapa detik, URL yang sama sudah menampilkan versi baru.

Alurnya:
```
Edit kode → git push → Vercel auto-deploy → URL update otomatis
```

Jadi setelah deploy pertama, kamu tidak perlu buka Vercel lagi untuk update — cukup `git push` seperti biasa.

---

## 7. (Opsional) Custom Domain

URL default `namaku.vercel.app` sudah cukup untuk portofolio. Tapi kalau mau lebih profesional (misal `budisantoso.com`), kamu bisa:

1. Beli domain (di Niagahoster, Namecheap, dll).
2. Di Vercel: **Settings** → **Domains** → **Add** → masukkan domain kamu.
3. Ikuti instruksi mengatur DNS.

Ini opsional dan bisa dilakukan kapan saja nanti.

---

## 8. Troubleshooting Umum

| Masalah | Kemungkinan Penyebab | Solusi |
| --- | --- | --- |
| Build gagal / error | Ada error di kode yang tidak ketahuan saat lokal | Cek log build di Vercel, perbaiki error, push ulang |
| Halaman putih/blank | Output directory salah | Cek Build Command & Output Directory (Bagian 4) |
| CSS/gambar tidak muncul | Path file salah (pakai path absolut) | Gunakan path relatif, cek nama file (case-sensitive!) |
| Repo tidak muncul di Vercel | Vercel belum diberi akses | Adjust GitHub App Permissions |
| Update tidak muncul | Belum di-push ke GitHub | Pastikan sudah `git push` ke branch `main` |

> **Tips:** Kalau build gagal, jangan panik. Vercel selalu menampilkan **log** yang memberi tahu error-nya di baris mana. Baca log-nya — biasanya errornya sama dengan yang muncul saat `npm run build` di lokal. Coba jalankan `npm run build` di laptop dulu untuk memastikan tidak ada error sebelum push.

---

## 9. Ringkasan Modul 5.2

Setelah menyelesaikan modul ini, kamu diharapkan:

- Memahami bahwa ada **banyak pilihan platform deploy**, dan kenapa kita pakai Vercel.
- Paham bahwa **frontend & backend bisa deploy terpisah** lalu disambungkan lewat URL API.
- Bisa membuat akun **Vercel** dan menghubungkannya ke **GitHub**.
- Bisa **meng-import dan men-deploy** project (statis, React, atau Next.js).
- Punya website portofolio yang **live dengan URL publik**.
- Paham konsep **auto-deploy**: cukup `git push` untuk update website.

Pada **Modul 5.3 (Opsional)**, kita akan bahas cara deploy website **full-stack** (yang punya backend + database) menggunakan Railway — buat kamu yang portofolionya lebih dari sekadar halaman statis.

---




