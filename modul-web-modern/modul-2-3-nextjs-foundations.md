# Modul 2.3 – Pengenalan Next.js

Pada modul ini, kamu akan belajar:
- Apa itu **Next.js** dan bagaimana hubungannya dengan React.
- Perbedaan **React saja** vs **React + Next.js**.
- Gambaran fitur utama Next.js (routing, struktur folder, rendering).
- Kenapa Next.js banyak dipakai di project web modern.

---

## 1. React Saja vs React + Next.js

Di modul sebelumnya, kita sudah mengenal **React** sebagai library untuk membangun UI berbasis komponen.

Kalau kita pakai **React saja** (tanpa Next.js), biasanya:

- Kita membuat aplikasi **Single Page Application (SPA)**.
- Kita butuh tambahan tool untuk:
  - Routing (misalnya React Router),
  - Build & bundling (misalnya Vite, Webpack),
  - Optimasi performance dan konfigurasi lainnya.
- Struktur folder proyek lebih bebas, tapi juga lebih banyak keputusan yang harus kita ambil sendiri.

Di sinilah **Next.js** membantu.

> **Next.js adalah framework berbasis React yang memberikan struktur dan fitur tambahan untuk membangun aplikasi web modern.**

Dengan Next.js, kita tetap menulis **komponen React**, tapi:

- Routing sudah disediakan.
- Struktur dasar proyek sudah ditentukan.
- Ada dukungan untuk rendering di server, optimasi SEO, dan lain-lain.

---

## 2. Apa Itu Next.js?

Secara singkat:

> **Next.js adalah framework React untuk membangun aplikasi web fullstack yang cepat, terstruktur, dan siap produksi.**

Beberapa hal yang membuat Next.js menarik:

- Dibangun di atas **React** → jadi semua yang kamu pelajari tentang komponen React tetap berlaku.
- Mendukung **Fullstack**:
  - Halaman frontend,
  - API routes (endpoint backend sederhana) dalam satu project yang sama.
- Dikembangkan oleh **Vercel** dan terintegrasi dengan sangat baik untuk deployment.

---

## 3. Fitur Utama Next.js (Gambaran Tingkat Tinggi)

Tanpa masuk terlalu teknis dulu, berikut beberapa fitur penting Next.js:

### 3.1. File-based Routing

- Di Next.js, kita bisa membuat halaman baru hanya dengan **menambah file** di folder tertentu.
- Contoh:
  - `app/page.tsx` → halaman utama (`/`).
  - `app/about/page.tsx` → halaman `/about`.
- Kita tidak perlu mengatur router manual seperti di React murni.

### 3.2. Rendering (SSR, SSG, CSR)

Next.js mendukung beberapa cara untuk merender halaman:

- **SSR (Server-Side Rendering)**  
  Halaman dirender di server setiap kali ada request, lalu dikirim ke browser.

- **SSG (Static Site Generation)**  
  Halaman dirender sekali saat build, lalu disajikan sebagai file statis.

- **CSR (Client-Side Rendering)**  
  Bagian tertentu tetap bisa dirender di sisi client dengan React biasa.

Untuk modul pengenalan ini, kamu tidak perlu menghafal semua istilahnya, cukup pahami:

> Next.js membantu mengatur **kapan** dan **di mana** sebuah halaman dirender, sehingga kita bisa mengoptimalkan **kecepatan** dan **SEO**.

### 3.3. Struktur Proyek yang Jelas

Next.js sudah memberikan pola struktur folder:

- Folder untuk halaman (misalnya `app/` atau `pages/` tergantung versi Next).
- Folder untuk komponen.
- Folder untuk API routes, dll.

Ini membantu tim agar:

- Kode lebih terorganisir,
- Semua developer “bermain dengan aturan yang sama”.

---

## 4. Hubungan React dan Next.js

Penting:

- Kamu **bisa** memakai React **tanpa** Next.js  
  (misalnya pakai Vite + React, atau Create React App).
- Kamu **tidak bisa** memakai Next.js **tanpa** React, karena:
  - Next.js dibangun di atas React.
  - Di dalam file Next.js, kita tetap menulis komponen React.

Cara melihatnya:

- **React** → alat untuk membangun UI (komponen).
- **Next.js** → kerangka kerja aplikasi berbasis React.

Di banyak project modern, orang langsung bilang:
- “Kita pakai Next.js” → maksudnya: React **+** fitur-fitur tambahan dari Next.

---

## 5. Kenapa Banyak Project Memilih Next.js?

Beberapa alasan Next.js populer di industri:

- **SEO lebih baik**  
  Karena bisa merender halaman di server (SSR / SSG), konten halaman lebih mudah dibaca mesin pencari.

- **Developer experience yang bagus**  
  Hot reload, error overlay, dokumentasi rapi, banyak contoh starter.

- **Ekosistem kuat**  
  Banyak tutorial, template, dan integrasi dengan Tailwind CSS, Prisma, dll.

- **Mudah di-deploy**  
  Terutama ke platform seperti Vercel.

---

## 6. Next.js dalam Konteks Workshop Ini

Dalam konteks workshop Web Modern ini:

- **React** akan dikenalkan sebagai cara baru membangun UI.
- **Next.js** akan dikenalkan sebagai framework yang:
  - Menggunakan React di dalamnya,
  - Menyediakan struktur dan fitur tambahan untuk aplikasi web yang lebih besar.

Di sesi live coding, kamu mungkin akan melihat:

- Bagaimana membuat project Next.js baru.
- Di mana kita menulis komponen React.
- Bagaimana Next.js mengatur halaman (routing) berdasarkan struktur folder.

Untuk saat ini, cukup pahami dulu konsep besarnya:

> “Next.js membantu kita membawa React ke level **aplikasi web produksi** dengan struktur dan fitur bawaan yang jelas.”
