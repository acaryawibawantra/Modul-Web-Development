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

**CSS (Cascading Style Sheets)** adalah bahasa yang digunakan untuk mengatur tampilan dokumen yang ditulis dalam HTML. Jika HTML adalah kerangkanya, maka CSS adalah **pakaian, cat, dan dekorasinya**. CSS memungkinkan kita mengubah warna, font, ukuran, hingga posisi elemen di layar.

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

# 3. Cara Menambahkan CSS ke HTML

Ada tiga cara utama untuk menghubungkan CSS dengan file HTML:

### 1. Inline CSS
Menulis kode langsung di dalam tag HTML menggunakan atribut `style`. (Tidak disarankan untuk proyek besar).
```html
<p style="color: red; font-weight: bold;">Ini adalah Inline CSS.</p>
```

### 2. Internal CSS
Menulis kode di dalam tag `<style>` di bagian `<head>` file HTML.
```html
<style>
  body { background-color: #f4f4f4; }
  p { color: green; }
</style>
```

### 3. External CSS
Menghubungkan file `.css` terpisah menggunakan tag `<link>`. **Ini adalah cara terbaik.**
```html
<link rel="stylesheet" href="style.css">
```

# 4. CSS Selectors (Pemilih)

-   **Element Selector**: Memilih elemen berdasarkan nama tag (misal: `p`, `h1`, `div`).
-   **Class Selector**: Memilih elemen berdasarkan atribut `class`. Gunakan tanda titik (`.`).
    ```css
    .tombol-biru { background-color: blue; }
    ```
-   **ID Selector**: Memilih elemen berdasarkan atribut `id` yang unik. Gunakan tanda pagar (`#`).
    ```css
    #header-utama { font-size: 32px; }
    ```

# 5. Box Model

Konsep terpenting dalam CSS adalah **Box Model**. Setiap elemen HTML dianggap sebagai sebuah kotak.

Box Model terdiri dari (dari dalam ke luar):
1.  **Content**: Isi elemen (teks/gambar).
2.  **Padding**: Ruang antara konten dan border (di dalam elemen).
3.  **Border**: Garis tepi elemen.
4.  **Margin**: Ruang kosong di luar border (jarak antar elemen).

![Diagram Box Model](https://developer.mozilla.org/en-US/docs/Learn/CSS/Introduction_to_CSS/The_box_model/box-model.png)

# 6. Layout Modern: Flexbox

**Flexbox** adalah cara termudah untuk mengatur posisi elemen (seperti membuat menu navigasi atau menyeimbangkan kolom) dalam satu dimensi (baris atau kolom).

Cukup gunakan `display: flex;` pada container induk:

```css
.container {
  display: flex;
  justify-content: space-around; /* Jarak antar elemen */
  align-items: center;           /* Rata tengah secara vertikal */
  gap: 20px;                     /* Jarak antar item */
}
```

# 7. Desain Responsif (Media Queries)

Agar website terlihat bagus di HP maupun Desktop, kita menggunakan **Media Queries**.

```css
/* Style untuk layar lebar (Desktop) */
.content { display: flex; }

/* Jika layar kurang dari 768px (HP/Tablet) */
@media (max-width: 768px) {
  .content { display: block; } /* Elemen akan menumpuk ke bawah */
}
```

---

### Pelajari Lebih Lanjut:
-   [MDN Web Docs - CSS Basics](https://developer.mozilla.org/en-US/docs/Learn_web_development/Core/Styling_basics)
-   [CSS-Tricks - Guide to Flexbox](https://css-tricks.com/snippets/css/a-guide-to-flexbox/)
-   [W3Schools CSS Tutorial](https://www.w3schools.com/css/)