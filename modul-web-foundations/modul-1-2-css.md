---
title: "Modul 1.2: Cascading Style Sheets (CSS)"
date: 2026-03-11
weight: 2
description: "Mempelajari bagaimana memberikan gaya dan tata letak pada halaman web menggunakan CSS."
categories: ["Web Development", "GDGOC ITS"]
tags: ["html", "css", "javascript", "gdgoc"]
showToc: true
TocOpen: false
---

# 1. Apa itu CSS?

**CSS (Cascading Style Sheets)** adalah bahasa yang digunakan untuk mengatur tampilan dokumen yang ditulis dalam HTML.  
Jika HTML adalah kerangkanya, maka CSS adalah **pakaian, cat, dan dekorasinya**.  
CSS memungkinkan kita mengubah warna, font, ukuran, hingga posisi elemen di layar.

---

# 2. Sintaks Dasar CSS

CSS bekerja dengan cara memilih elemen (selector) lalu memberikan nilai pada propertinya (declaration).

**Struktur Sintaks:**

```css
selector {
  property: value;
}
```

- **Selector**: Target elemen HTML yang ingin diubah gayanya.
- **Property**: Aspek gaya yang ingin diubah (misal: warna, ukuran font).
- **Value**: Nilai dari properti tersebut.

**Contoh:**

```css
h1 {
  color: blue;
  font-size: 24px;
  text-align: center;
}
```

---

# 3. Cara Menambahkan CSS ke HTML

Ada tiga cara utama untuk menghubungkan CSS dengan file HTML:

### 1. Inline CSS

Menulis kode langsung di dalam tag HTML menggunakan atribut `style`.  
Biasanya hanya untuk contoh cepat, **tidak disarankan** untuk proyek besar.

```html
<p style="color: red; font-weight: bold;">Ini adalah Inline CSS.</p>
```

### 2. Internal CSS

Menulis kode di dalam tag `<style>` di bagian `<head>` file HTML.

```html
<head>
  <style>
    body {
      background-color: #f4f4f4;
    }

    p {
      color: green;
    }
  </style>
</head>
```

### 3. External CSS

Menghubungkan file `.css` terpisah menggunakan tag `<link>`.  
**Ini adalah cara terbaik** untuk proyek nyata, karena rapi dan mudah dirawat.

```html
<head>
  <link rel="stylesheet" href="style.css" />
</head>
```

---

# 4. CSS Selectors (Pemilih)

Selector digunakan untuk memilih elemen yang akan diberi gaya.

## 4.1 Element Selector

Memilih elemen berdasarkan nama tag (misal: `p`, `h1`, `div`).

```css
p {
  color: #333;
}

h1 {
  text-transform: uppercase;
}
```

## 4.2 Class Selector

Memilih elemen berdasarkan atribut `class`.  
Gunakan tanda titik (`.`) di depan nama class.

```html
<p class="highlight">Teks ini punya class "highlight".</p>
```

```css
.highlight {
  background-color: yellow;
  font-weight: bold;
}
```

## 4.3 ID Selector

Memilih **satu** elemen dengan atribut `id` tertentu.  
Gunakan tanda pagar (`#`).

```html
<h1 id="main-title">Judul Utama</h1>
```

```css
#main-title {
  color: #0f766e;
  font-size: 32px;
}
```

> Catatan: `id` sebaiknya unik di satu halaman, sedangkan `class` bisa dipakai di banyak elemen.

## 4.4 Grouping Selector

Beberapa selector bisa digabung jika punya gaya yang sama.

```css
h1,
h2,
h3 {
  font-family: system-ui, sans-serif;
  color: #111827;
}
```

---

# 5. Properti CSS Dasar

## 5.1 Warna dan Background

```css
body {
  background-color: #f9fafb; /* warna latar belakang */
}

p {
  color: #374151; /* warna teks */
}

.highlight {
  background-color: #fef3c7;
}
```

CSS mendukung nilai warna seperti:

- Nama warna: `red`, `blue`, `green`
- Hex: `#1f2937`
- RGB: `rgb(31, 41, 55)`
- HSL: `hsl(210, 20%, 20%)`

## 5.2 Font dan Teks

```css
body {
  font-family: system-ui, -apple-system, BlinkMacSystemFont, "Segoe UI", sans-serif;
  line-height: 1.5;
}

h1 {
  font-size: 2rem;
  font-weight: 700;
}

p {
  font-size: 1rem;
  text-align: justify;
}
```

Properti penting:

- `font-family`
- `font-size`
- `font-weight`
- `line-height`
- `text-align`
- `text-decoration`

---

# 6. Box Model: Margin, Border, Padding

Setiap elemen di HTML dianggap sebagai **kotak (box)**.

Box Model terdiri dari:

- **Content**: isi elemen (teks/gambar).
- **Padding**: jarak antara konten dan border.
- **Border**: garis di sekitar elemen.
- **Margin**: jarak antara elemen dan elemen lain.

```css
.card {
  background-color: #ffffff;
  padding: 16px;         /* jarak isi ke border */
  border: 1px solid #e5e7eb;
  margin-bottom: 16px;   /* jarak antar card */
  border-radius: 8px;    /* sudut membulat */
}
```

Contoh di HTML:

```html
<div class="card">
  <h2>About the Event</h2>
  <p>Ini adalah contoh card sederhana.</p>
</div>
```

---

# 7. Layout Dasar: Display dan Flexbox

## 7.1 Display

Properti `display` menentukan cara elemen ditampilkan.

```css
.block-element {
  display: block; /* Mengisi lebar penuh, mulai di baris baru */
}

.inline-element {
  display: inline; /* Mengisi sesuai konten, tidak mulai baris baru */
}

.inline-block-element {
  display: inline-block; /* Bisa diatur width/height, tetap satu baris */
}
```

## 7.2 Flexbox (Dasar)

Flexbox memudahkan mengatur layout satu dimensi (horizontal/vertical).

```css
.navbar {
  display: flex;
  justify-content: space-between; /* sebar elemen secara horizontal */
  align-items: center;            /* rata tengah secara vertikal */
}
```

```html
<header class="navbar">
  <h1>GDGoC ITS</h1>
  <nav>
    <a href="#about">About</a>
    <a href="#topics">Topics</a>
    <a href="#register">Register</a>
  </nav>
</header>
```

---

# 8. Responsive Design (Media Query)

Agar tampilan website tetap nyaman di layar kecil (HP) dan besar (laptop), gunakan **media query**.

```css
.container {
  max-width: 960px;
  margin: 0 auto;
  padding: 16px;
}

/* Jika lebar layar kurang dari atau sama dengan 640px (mobile) */
@media (max-width: 640px) {
  .container {
    padding: 8px;
  }

  h1 {
    font-size: 1.5rem;
  }
}
```

---

# 9. Contoh Koneksi ke Study Case (Event Registration)

Berikut contoh sederhana gaya yang mirip dengan study case **Event Registration Mini Site**:

```css
body {
  font-family: system-ui, sans-serif;
  background-color: #0f172a;
  color: #e5e7eb;
  margin: 0;
}

.site-header {
  text-align: center;
  padding: 24px 16px;
}

.container {
  max-width: 960px;
  margin: 0 auto;
  padding: 16px;
}

.card {
  background-color: #020617;
  border-radius: 12px;
  padding: 16px 20px;
  margin-bottom: 16px;
  border: 1px solid #1f2937;
}

.form-group {
  display: flex;
  flex-direction: column;
  margin-bottom: 12px;
}

.form-group label {
  margin-bottom: 4px;
  font-weight: 500;
}

input,
select {
  padding: 8px 10px;
  border-radius: 8px;
  border: 1px solid #4b5563;
  background-color: #020617;
  color: #e5e7eb;
}

.btn-primary {
  background-color: #22c55e;
  border: none;
  color: #022c22;
  font-weight: 600;
  padding: 10px 16px;
  border-radius: 999px;
  cursor: pointer;
}

.btn-primary:hover {
  background-color: #16a34a;
}
```

CSS di atas sudah memperlihatkan:

- Penggunaan class untuk layout (`container`, `card`, `form-group`).
- Styling form input dan button.
- Warna dan radius yang konsisten.

---

# 10. Latihan Singkat

Coba praktikkan:

1. Ambil file `index.html` dari modul HTML (atau dari study case yang sederhana).
2. Buat file baru `style.css`.
3. Tambahkan:
   - Warna background berbeda untuk `body`.
   - Warna teks khusus untuk heading (`h1`, `h2`).
   - `card` dengan background putih dan sudut melengkung.
   - Margin dan padding yang rapi.
4. Hubungkan file CSS ke HTML dengan:

```html
<link rel="stylesheet" href="style.css" />
```

Lalu buka halaman di browser dan perhatikan bagaimana tampilan berubah setelah CSS diterapkan.

---

# 11. Ringkasan Modul

Di Modul 1.2 ini kamu sudah belajar:

- Apa itu CSS dan perannya terhadap HTML.
- Cara menulis sintaks dasar CSS (selector, property, value).
- Cara menghubungkan CSS ke HTML (inline, internal, external).
- Jenis-jenis selector: element, class, id, dan grouping.
- Properti dasar: warna, background, font, dan teks.
- Konsep **box model**: margin, padding, border.
- Dasar layout dengan `display` dan Flexbox.
- Pengantar responsive design dengan media query.
- Contoh penerapan CSS di konteks study case Event Registration.

Modul berikutnya (1.3) akan fokus pada **JavaScript**, yaitu bagaimana menambahkan **logika dan interaktivitas** ke halaman yang sudah kamu bangun dengan HTML dan CSS.
