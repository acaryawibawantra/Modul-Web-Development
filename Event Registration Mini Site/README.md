# GDGoC ITS – Event Registration Mini Site

Mini project for the **Web Foundations: HTML, CSS, JavaScript** session at GDGoC ITS by (https://www.acaryawibawantra.xyz/gdgoc/).

## What we practice

- HTML
  - Basic structure (`<!DOCTYPE html>`, `<head>`, `<body>`)
  - Semantic elements (`<header>`, `<main>`, `<section>`, `<footer>`)# GDGoC ITS – Web Foundations Workshop & Modul Web Development

Mini project dan modul pendukung untuk sesi **Web Foundations: HTML, CSS, JavaScript** di GDGoC ITS.  
Repository ini berisi kode studi kasus *Event Registration* sekaligus pengantar materi dasar Web Development.

## 📚 Modul Pembelajaran

Materi lengkap dan terstruktur bisa kamu baca di website:

- Modul Web Development GDGoC ITS: [acaryawibawantra.xyz – Modul Web Development GDGOC ITS](https://www.acaryawibawantra.xyz/gdgoc)

Modul dibagi per topik agar mudah diikuti:

### Modul 1.1: Web Foundations & HTML

Di modul ini kamu belajar fondasi cara kerja web dan dasar HTML:

- Konsep **client** dan **server** (bagaimana browser berkomunikasi dengan server).
- Apa itu HTML dan perannya dalam membangun halaman web.
- Struktur dasar dokumen HTML: `<!DOCTYPE html>`, elemen `<html>`, `<head>`, dan `<body>`.
- Pengenalan elemen semantik seperti `<header>`, `<main>`, `<section>`, `<footer>`.

Detail penjelasan dan contoh kode ada di modul HTML di website.

### Modul 1.2: Cascading Style Sheets (CSS)

Modul ini membahas cara mengatur tampilan halaman:

- Apa itu CSS dan bagaimana ia mengatur presentasi dokumen HTML.
- Cara menghubungkan file CSS ke HTML dengan `<link rel="stylesheet" href="style.css">`.
- Dasar selector (element, class, id) dan properti styling (warna, font, spacing).
- Gambaran awal layout dan responsivitas.

Penjelasan lengkap ada di modul CSS di website.

### Modul 1.3: Dasar-dasar JavaScript

Di modul ini kamu masuk ke logika dan interaktivitas:

- Apa itu JavaScript dan perannya untuk membuat halaman interaktif.
- Contoh penggunaan JS di browser (event, animasi sederhana, dsb).
- Dasar-dasar: variabel, array, loop, conditional, fungsi.
- Pengantar DOM: memilih elemen, menangani event, dan memanipulasi konten.

Detail dan contoh lebih lengkap ada di modul JavaScript di website.

---

## 🧪 Modul 1.4: Web Foundations Workshop (Study Case)

Sebagai penutup Web Foundations, kita mempraktikkan semua materi dengan membangun halaman **Event Registration** sederhana.

Live versi web study case ada di:

- Web Study Case: [GDGoC ITS – Web Foundations Workshop](https://www.acaryawibawantra.xyz/web-foundations-workshop/)

### Struktur Proyek

Proyek ini adalah static site sederhana tanpa build tools.

- `index.html` – Struktur dan konten halaman:
  - Bagian **About the Event**: menjelaskan tujuan sesi.
  - Bagian **Topics Covered**: ringkasan materi HTML, CSS, dan JavaScript yang dipelajari.
  - Bagian **Event Registration**: form pendaftaran peserta (nama, email, level pengalaman, opsi join grup WhatsApp).
  - Bagian **Registered Participants**: daftar peserta yang sudah mendaftar (diisi via JavaScript).
  - Header dan footer dengan informasi workshop.

- `style.css` – Styling tampilan:
  - Mengatur layout card, container, dan tipografi.
  - Styling form (label, input, button).
  - Warna, spacing, dan tampilan yang konsisten dengan materi di modul CSS.
  - Responsif dasar untuk tampilan yang nyaman di berbagai ukuran layar.

- `script.js` – Logika interaktif:
  - Mengambil nilai input dari form (nama, email, experience level, checkbox WA).
  - Validasi sederhana dan menampilkan pesan error/sukses.
  - Menyimpan data peserta ke array dan menampilkannya ke dalam elemen daftar peserta.
  - Contoh penggunaan DOM selection, event listener, fungsi, dan array.

---

## 🚀 Cara Menjalankan

Tidak perlu instalasi atau build step.

1. Clone atau download repository ini.
2. Buka file `index.html` langsung di browser (Chrome, Firefox, dll).
3. Form pendaftaran sudah bisa digunakan dan daftar peserta akan muncul di bagian **Registered Participants**.

---

## 🎯 Tujuan Pembelajaran

Dengan modul dan study case ini, diharapkan peserta:

- Memahami alur dasar cara kerja web (client–server).
- Mampu menulis struktur HTML yang rapi dan semantik.
- Mampu memberi style dasar halaman dengan CSS.
- Mampu menambahkan interaktivitas sederhana menggunakan JavaScript dan DOM.
- Melihat gambaran utuh bagaimana HTML, CSS, dan JS bekerja bersama dalam satu mini project.

Untuk penjelasan teori yang lebih detail, silakan lihat modul lengkap di website, sementara repository ini fokus pada contoh implementasi kodenya.
  - Forms and inputs
- CSS
  - External stylesheet
  - Element, class, and ID selectors
  - Basic layout and colors
- JavaScript
  - DOM selection and event listeners
  - Variables, arrays, loops, and conditionals
  - Functions, parameters, and return values
  - Simple DOM manipulation (create and append elements)
  - Basic async behavior with `setTimeout`

## How to run

Just open `index.html` in your browser (no build tools needed).
