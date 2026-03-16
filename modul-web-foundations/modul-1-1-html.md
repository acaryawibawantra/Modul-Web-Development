---
title: "Modul 1.1: Web Foundations & HTML"
date: 2026-03-11
weight: 1
description: "Pengenalan cara kerja website, tools yang dibutuhkan, serta dasar HTML."
categories: ["Web Development", "GDGOC ITS"]
tags: ["html", "css", "javascript", "gdgoc"]
showToc: true
TocOpen: false
---

# 1. Pendahuluan

## Bagaimana Cara Kerja Website?

Komputer yang terhubung ke internet disebut sebagai **client** (klien) dan **server**. Diagram sederhana interaksi keduanya terlihat seperti ini:

![Interaksi Client dan Server](/modul-web-foundations/image-1.png)

*   **Client**: Perangkat pengguna yang terhubung ke internet (seperti laptop atau ponsel) dan perangkat lunak pengakses web (seperti browser Chrome atau Firefox).
*   **Server**: Komputer yang menyimpan halaman web, aplikasi, atau data. Ketika client meminta akses, server akan mengirimkan salinan data tersebut untuk ditampilkan di browser pengguna.

![Alur Request dan Response](/images/modul-web-foundations/image.png)

### Alur Singkat:
1. Setiap client dan server memiliki alamat unik di internet yang disebut **IP Address**.
2. Saat kamu mengunjungi `www.example.com`, browser akan melakukan pencarian ke **DNS** untuk mengetahui IP server tersebut.
3. Client mengirimkan **Request** (permintaan) ke server berdasarkan IP tersebut.
4. Server mengirimkan **Response** (jawaban) kembali ke client dalam bentuk file (HTML, CSS, JS) yang kemudian dirender oleh browser.

# 2. Tools Pengembangan Web

Untuk mulai membangun website, kita membutuhkan beberapa peralatan dasar:

-   **Text Editors / IDE**: Tempat menulis kode. Pilihan populer: [Visual Studio Code](https://code.visualstudio.com/), [Cursor](https://www.cursor.com/), [WebStorm](https://www.jetbrains.com/webstorm/).
-   **Browsers**: Untuk melihat hasil kode (Chrome, Firefox, Edge).
-   **Version Control System**: [Git](https://git-scm.com/) untuk mengelola riwayat perubahan kode.
-   **Hosting Providers**: Tempat meletakkan website agar bisa diakses orang lain (GitHub Pages, Netlify, Vercel, AWS, dll).

# 3. HTML (HyperText Markup Language)

## Apa itu HTML?

HTML adalah bahasa markup standar yang digunakan untuk menentukan struktur sebuah halaman web. Bayangkan HTML sebagai **kerangka tulang** dari sebuah bangunan. HTML terdiri dari serangkaian **elemen** yang memberitahu browser bagaimana konten harus ditampilkan (misalnya: ini adalah judul, ini adalah paragraf, ini adalah link).

## Anatomi Elemen HTML

![Anatomi Elemen HTML](/images/modul-web-foundations/image-2.png)

1.  **Opening Tag (Tag Pembuka)**: Nama elemen yang dibungkus kurung sudut (misal: `<p>`). Ini menandakan awal elemen.
2.  **Content (Konten)**: Isi dari elemen tersebut.
3.  **Closing Tag (Tag Penutup)**: Sama seperti tag pembuka, tapi diawali dengan garis miring (misal: `</p>`). Ini menandakan akhir elemen.
4.  **Element (Elemen)**: Gabungan dari tag pembuka, konten, dan tag penutup.

## Nesting Elemen (Elemen Bersarang)

Kamu bisa memasukkan elemen di dalam elemen lain:

```html
<p>Kucing saya <strong>sangat</strong> galak.</p>
```
*Pastikan urutan penutupannya benar: elemen yang terakhir dibuka harus pertama ditutup.*

## Void Elements

Beberapa elemen tidak memiliki konten atau tag penutup. Elemen ini biasanya digunakan untuk memasukkan sesuatu ke halaman, seperti Gambar:

```html
<img src="https://raw.githubusercontent.com/mdn/beginner-html-site/gh-pages/images/firefox-icon.png" alt="Logo Firefox" />
```

## Elemen Fundamental

### 1. Format Teks
-   `<h1>` sampai `<h6>`: Judul (Heading). `<h1>` adalah yang terbesar.
-   `<p>`: Paragraf.
-   `<strong>` / `<b>`: Teks tebal.
-   `<em>` / `<i>`: Teks miring.

### 2. Link & Gambar
-   `<a>` (Anchor): Membuat link. Gunakan atribut `href` untuk alamat tujuan.
-   `<img>`: Menampilkan gambar. Gunakan `src` untuk sumber file dan `alt` untuk teks deskripsi.

### 3. Daftar (Lists)
-   **Unordered List (`<ul>`)**: Daftar poin (bullets).
-   **Ordered List (`<ol>`)**: Daftar urutan angka.
-   **List Item (`<li>`)**: Item di dalam daftar.

```html
<ul>
  <li>Belajar HTML</li>
  <li>Belajar CSS</li>
</ul>
```

# 4. Formulir (Forms)

Formulir digunakan untuk berinteraksi dengan pengguna (login, daftar, kontak).

```html
<form action="/submit" method="POST">
  <label for="nama">Nama Lengkap:</label>
  <input type="text" id="nama" name="nama" placeholder="Masukkan nama...">

  <label for="email">Email:</label>
  <input type="email" id="email" name="email">

  <button type="submit">Kirim</button>
</form>
```
*Tipe input umum: `text`, `email`, `password`, `number`, `checkbox`, `radio`.*

# 5. Semantic HTML

**Semantic HTML** berarti menggunakan tag sesuai dengan makna dan tujuannya. Ini sangat penting untuk **Aksesibilitas** (pengguna dengan alat bantu baca) dan **SEO** (agar website mudah ditemukan di Google).

Pilihan tag semantic yang disarankan:
-   `<header>`: Bagian atas (logo & navigasi).
-   `<nav>`: Menu navigasi.
-   `<main>`: Konten utama halaman.
-   `<article>`: Konten mandiri (seperti post blog).
-   `<section>`: Bagian-bagian dalam dokumen.
-   `<footer>`: Bagian bawah (copyright & info tambahan).

---

### Pelajari Lebih Lanjut:
-   [MDN Web Docs - HTML Basics](https://developer.mozilla.org/en-US/docs/Learn_web_development/Core/Structuring_content)
-   [W3Schools HTML Tutorial](https://www.w3schools.com/html/)
