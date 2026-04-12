# Modul 2.4 – Tailwind CSS Foundations

Pada modul ini, kamu akan belajar:
- Apa itu **Tailwind CSS** dan kenapa disebut *utility-first CSS framework*.
- Masalah umum ketika styling dengan CSS biasa.
- Cara berpikir utility class di Tailwind.
- Contoh sederhana penggunaan Tailwind di komponen UI.
- Gambaran singkat cara setup Tailwind di project Next.js.

- https://tailwindcss.com/

---

## 1. Masalah Styling dengan CSS Biasa

Di modul sebelumnya kamu sudah menulis CSS secara manual:

- Membuat class sendiri (`.card`, `.btn-primary`, `.navbar`, dll).
- Menyimpan semua aturan di file `.css`.

Pendekatan ini bagus untuk belajar dasar, tapi ketika project makin besar, biasanya muncul masalah:

- **Penamaan class membingungkan**  
  Misalnya: `.card`, `.card-1`, `.card-primary`, `.main-card`, dst.
- **Tidak konsisten**  
  Margin/padding/warna/font kadang beda-beda di tiap halaman.
- **File CSS membengkak**  
  Sulit tahu class mana yang masih dipakai dan mana yang sudah tidak terpakai.
- **Refactor styling** jadi sulit karena banyak saling ketergantungan.

Kita butuh pendekatan styling yang:

- Konsisten (spacing, warna, font),
- Cepat dibuat,
- Enak dipakai bersama komponen (misalnya di React/Next.js).

Salah satu solusi populer: **Tailwind CSS**.

---

## 2. Apa Itu Tailwind CSS?

> **Tailwind CSS adalah framework CSS dengan pendekatan *utility-first*.**

Artinya:

- Alih-alih membuat class besar seperti `.card` atau `.btn-primary`,
- Kita menggunakan **class kecil-kecil** yang masing-masing punya satu tugas jelas, misalnya:
  - `p-4` → padding 1rem,
  - `mt-2` → margin-top kecil,
  - `bg-blue-500` → background biru,
  - `text-white` → teks putih,
  - `rounded-lg` → sudut membulat.

Kita menyusun tampilan dengan **menggabungkan utility class** langsung di atribut `class`.

Tailwind tidak menggantikan CSS, tapi:

- Memberikan sekumpulan utility class yang **sudah terkonfigurasi** dengan skala spacing, warna, dan typography yang konsisten.

---

## 3. Contoh: HTML Biasa vs Tailwind

Misalkan sebelumnya kamu punya card sederhana dengan CSS biasa:

```html
<div class="card">
  <h3>GDGoC Web Dev Workshop</h3>
  <p>Sabtu, 20 April 2026</p>
  <p>Online - Google Meet</p>
</div>
```
Menggunakan CSS manual
```css
.card {
  padding: 16px;
  background-color: #2563eb;
  color: white;
  border-radius: 12px;
  box-shadow: 0 10px 15px -3px rgba(0,0,0,0.1);
}

 ```

Dan ini html yang menggunakan Tailwind
```html
<div class="p-4 bg-blue-600 text-white rounded-xl shadow-lg">
  <h3 class="text-lg font-semibold">
    GDGoC Web Dev Workshop
  </h3>
  <p>Sabtu, 20 April 2026</p>
  <p>Online - Google Meet</p>
</div>
```

Perbedaannya:

- **CSS biasa** → definisikan class di file `.css`, lalu pakai di HTML.
- **Tailwind** → langsung gunakan utility class yang sudah disediakan.

---

## 4. Kenapa Banyak Developer Suka Tailwind?

Beberapa alasan Tailwind populer:

- **Cepat untuk prototyping**  
  Kamu bisa membangun tampilan dengan sangat cepat tanpa berpindah-pindah file (semua di satu tempat: HTML/JSX + class Tailwind).

- **Konsisten**  
  Tailwind menggunakan skala spacing, warna, dan font yang sudah ditentukan:  
  Contoh: `p-2`, `p-4`, `p-6` → punya makna yang konsisten di seluruh project.

- **Mudah diintegrasikan dengan React/Next.js**  
  Tailwind sangat umum dipakai di project Next.js modern.

- **Banyak komponen siap pakai**  
  Ada banyak resource seperti Tailwind UI, Flowbite, DaisyUI, dll yang menyediakan komponen siap pakai.

---

## 5. Gambaran Setup Tailwind di Next.js (Ringkas)

Di workshop ini, detail setup bisa ditunjukkan di sesi live coding.

Namun secara umum, alurnya seperti ini (gambaran tinggi saja):

1. Buat project Next.js (JavaScript) dengan `create-next-app`.
2. Pasang Tailwind CSS dan inisialisasi konfigurasi.
3. Tambahkan direktori `app` atau `pages` ke konfigurasi `content` Tailwind.
4. Gunakan utility class Tailwind di `className` pada komponen React/Next.js.

Contoh sangat ringkas (bukan langkah lengkap):

```bash
# Setelah membuat project Next.js
npm install -D tailwindcss postcss autoprefixer
npx tailwindcss init -p
```

Lalu di file global CSS (misalnya ‎`globals.css`):

```css
@tailwind base;
@tailwind components;
@tailwind utilities;
```

Setelah itu, kamu sudah bisa menulis:
```jsx
export default function HomePage() {
  return (
    <main className="min-h-screen flex items-center justify-center bg-slate-900">
      <div className="p-6 bg-white rounded-xl shadow-lg">
        <h1 className="text-xl font-semibold text-slate-900">
          Selamat datang di GDGoC Web Dev Workshop!
        </h1>
      </div>
    </main>
  );
}
```

## 6. Tailwind dalam Konteks Web Modern ￼

Dalam rangkaian materi ini:

- HTML, CSS, JS (Modul 1) → fondasi.

- React → cara modern membangun UI dengan komponen.

- Next.js → framework untuk mengatur struktur dan fitur aplikasi React.

- Tailwind CSS → cara modern styling UI dengan cepat dan konsisten.

Saat kamu menggabungkan semuanya di project nyata:

- Komponen dibuat dengan React,

- Aplikasi diatur dengan Next.js,

- Styling ditangani oleh Tailwind CSS.

Ini adalah kombinasi yang sangat umum dipakai di banyak project web modern dan juga sering muncul di lowongan kerja web developer saat ini.




