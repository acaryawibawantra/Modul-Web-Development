# Modul 5.1 – Pengenalan Deploy & Persiapan

Di modul ini kamu akan belajar **apa itu deploy**, kenapa website perlu di-deploy, dan **menyiapkan project** kamu supaya siap dipublikasikan ke internet.

Fokusnya:

- Memahami konsep **deploy** dan perbedaan **development** vs **production**.
- Mengerti kenapa `localhost` tidak cukup dan apa itu **hosting**.
- Mengenal **Vercel** dan **GitHub** sebagai tools untuk deploy.
- Menyiapkan project agar rapi dan sudah ada di GitHub.

Target akhirnya: project kamu siap dan sudah di-push ke GitHub, tinggal di-deploy di Modul 5.2.

---

## 1. Apa Itu Deploy?

Selama workshop ini, website kamu selalu jalan di **`localhost`** — misal `http://localhost:3000`. Coba pikirkan:

- Website itu **cuma bisa dibuka di komputermu sendiri**.
- Kalau laptop dimatikan, website ikut mati.
- Teman kamu **tidak bisa** membuka `localhost:3000` dari HP atau laptop mereka.

**Deploy** adalah proses **memindahkan website dari komputermu ke server yang selalu menyala di internet**, sehingga:

- Punya **alamat/URL publik** (misal `https://portofolio-budi.vercel.app`).
- Bisa diakses **siapa saja, kapan saja, dari mana saja**.
- Tetap hidup walaupun laptop kamu mati.

Analogi sederhana: selama ini website kamu seperti masakan yang cuma bisa dinikmati di dapur sendiri. **Deploy** = membuka warung supaya semua orang bisa datang dan mencicipi.

---

## 2. Development vs Production

Dua istilah yang sering kamu dengar:

| | Development | Production |
| --- | --- | --- |
| **Di mana** | Komputer/laptop kamu (`localhost`) | Server internet (cloud) |
| **Siapa yang akses** | Cuma kamu (developer) | Semua orang (user asli) |
| **Tujuan** | Ngoding & testing | Dipakai beneran |
| **Contoh URL** | `http://localhost:3000` | `https://namaku.vercel.app` |

- **Development** = tahap kamu membangun dan mencoba website.
- **Production** = versi final yang sudah "live" dan dipakai orang.

Deploy = proses membawa website dari **development** ke **production**.

---

## 3. Apa Itu Hosting?

**Hosting** adalah layanan yang menyediakan **server** untuk menyimpan dan menjalankan website kamu 24 jam nonstop.

Dulu, hosting itu ribet — harus sewa server, setting sendiri, bayar mahal. Sekarang ada platform modern yang bikin deploy **gratis dan super mudah**, cukup beberapa klik. Salah satu yang terbaik: **Vercel**.

---

## 4. Kenalan dengan Vercel & GitHub

Untuk deploy, kita pakai dua tools yang saling terhubung:

**GitHub** 🐙
- Tempat menyimpan kode kamu secara online (kamu sudah pakai ini sepanjang workshop).
- Vercel akan mengambil kode dari GitHub untuk di-deploy.

**Vercel** ▲
- Platform hosting gratis, khusus untuk frontend (HTML/CSS/JS, React, Next.js).
- Cara kerjanya: **connect ke GitHub → pilih repo → deploy**. Selesai.
- Bonus: setiap kali kamu `git push` update baru, Vercel **otomatis deploy ulang**. Ini disebut **auto-deploy**.

Kenapa Vercel cocok untuk portofolio?
- **Gratis** untuk personal project.
- **Cepat** — website langsung ngebut karena disebar di banyak server dunia (CDN).
- **Mudah** — tidak perlu setting server sama sekali.
- **Support Next.js** paling bagus (Vercel yang bikin Next.js).

---

## 5. Persiapan Project Sebelum Deploy

Sebelum deploy, pastikan project kamu **rapi dan jalan**. Ikuti checklist ini.

### 5.1. Pastikan project jalan di lokal

Buka project portofolio kamu, jalankan di lokal, dan pastikan **tidak ada error**.

Kalau project statis (HTML/CSS/JS), cukup buka `index.html` di browser.

Kalau pakai React/Next.js:
```
npm install

npm run dev
```

Buka `http://localhost:3000` — pastikan tampil dengan benar.

### 5.2. Buat file `.gitignore`

Jangan sampai folder `node_modules` (yang besar sekali) ikut ter-upload ke GitHub. Buat file `.gitignore`:
```
node_modules

.env

.next

dist
```

### 5.3. Push project ke GitHub

Vercel deploy dari GitHub, jadi project **wajib** ada di GitHub dulu.

1. Buat repository baru di [github.com/new](https://github.com/new). Beri nama, misal `portofolio`.
2. Di folder project kamu, jalankan:
```
git init

git add .

git commit -m “initial commit portofolio”

git branch -M main

git remote add origin https://github.com/USERNAME/portofolio.git

git push -u origin main
```

Ganti `USERNAME` dengan username GitHub kamu.

3. Refresh halaman repo di GitHub — kode kamu harusnya sudah muncul di sana.

---

## 6. Checklist Siap Deploy

Sebelum lanjut ke Modul 5.2, pastikan:

- [ ] Project portofolio **jalan tanpa error** di lokal.
- [ ] Sudah ada file `.gitignore` (folder `node_modules` tidak ikut ke-upload).
- [ ] Project sudah **di-push ke GitHub** dan muncul di repo.
- [ ] Kamu sudah punya akun **GitHub** (dan siap bikin akun Vercel).

---

## 7. Ringkasan Modul 5.1

Setelah menyelesaikan modul ini, kamu diharapkan:

- Paham apa itu **deploy** dan kenapa `localhost` saja tidak cukup.
- Mengerti perbedaan **development** dan **production**.
- Tahu apa itu **hosting** dan kenal **Vercel** + **GitHub**.
- Sudah menyiapkan project portofolio dan **mem-push-nya ke GitHub**.

Pada **Modul 5.2**, kita akan:

- Menghubungkan GitHub ke Vercel.
- Men-deploy website portofolio sampai **live dengan URL publik**.

---

