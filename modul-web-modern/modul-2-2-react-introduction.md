# Modul 2.2 – Pengenalan React

Pada modul ini, kamu akan belajar:
- Apa itu **React** dan kenapa React sangat populer di dunia web development.
- Konsep dasar **komponen** (component) dalam membangun UI.
- Gambaran tentang **props** dan **state** secara konsep (tanpa masuk terlalu dalam ke detail teknis).
- Bagaimana React dipakai di project nyata dan hubungannya dengan Next.js.

---

## 1. Kenapa Butuh React?

Di modul sebelumnya, kita sudah melihat bahwa:

- HTML dipakai untuk menyusun struktur halaman.
- CSS untuk styling.
- JavaScript untuk menambahkan interaktivitas.

Kalau aplikasi web yang kita buat masih **kecil dan sederhana**, cara ini sudah cukup.

Tapi ketika aplikasi mulai tumbuh:

- Banyak bagian UI yang **berulang** (card, button, navbar, footer, form, dll).
- Kita mulai ingin **mengubah tampilan berdasarkan data** (misalnya: jumlah item di keranjang, status login, daftar produk, dll).
- Mengelola **DOM secara manual** dengan JavaScript (pakai `document.querySelector`, `innerHTML`, dll) menjadi:
  - Mudah salah,
  - Sulit di-maintain,
  - Sulit di-scale.

Kita butuh cara:

- Mengorganisir UI dalam **bagian-bagian kecil yang bisa digunakan ulang**.
- Menghubungkan tampilan dengan **data** secara lebih rapi.

Di sinilah **React** masuk.

---

## 2. Apa Itu React?

> **React adalah library JavaScript untuk membangun user interface (UI).**

Beberapa poin penting:

- React fokus pada **UI** (tampilan).
- React membantu kita membangun UI menggunakan **komponen**.
- React tidak menggantikan HTML/CSS/JS, tetapi memberikan **cara baru untuk mengorganisir** ketiganya.

React dibuat oleh Facebook (sekarang Meta) dan digunakan di banyak produk besar, misalnya:

- Facebook
- Instagram
- WhatsApp Web
- Dan banyak aplikasi web modern lainnya

---

## 3. Cara Berpikir Komponen (Component-Based)

Konsep paling penting di React adalah **component**.

> **Komponen adalah “potongan UI” yang berdiri sendiri dan bisa digunakan ulang.**

Contoh komponen di sebuah website:

- Navbar
- Footer
- Card produk
- Tombol (Button)
- Input form

Di HTML biasa, kita mungkin akan:

- Menyalin blok `<div class="card">...</div>` berkali-kali.
- Kalau ada perubahan, kita harus mengubah di banyak tempat.

Di React, kita bisa:

- Membuat **satu komponen `Card`**, lalu memakainya berkali-kali dengan data yang berbeda.

Secara konsep, bedanya:

- HTML biasa → copy-paste struktur yang sama berkali-kali.
- React → definisikan satu komponen, lalu **re-use**.

---

## 4. Props dan State (Gambaran Konseptual)

Untuk mengatur data dalam komponen, React punya dua konsep penting: **props** dan **state**.

### 4.1. Props

> **Props adalah data yang dikirim ke komponen dari luar.**

Bayangkan kamu punya komponen `CardEvent`, lalu kamu kirim:

- `title`
- `date`
- `location`

Setiap kali kamu memanggil `CardEvent` dengan props berbeda, tampilan card-nya bisa berbeda, walau komponen dasarnya sama.

Analoginya:

- Props seperti **parameter** ketika kamu memanggil fungsi.

### 4.2. State

> **State adalah data internal di dalam sebuah komponen yang bisa berubah.**

Contoh:

- Jumlah item di keranjang belanja.
- Status “sudah diklik” atau “belum” pada sebuah tombol.
- Nilai input form yang sedang diketik user.

Ketika **state berubah**, React akan **merender ulang** bagian UI yang perlu diperbarui, sehingga tampilan selalu sesuai dengan data terbaru.

---

## 5. React di Project Nyata

Di dunia industri, React:

- Dipakai untuk membangun aplikasi web yang **interaktif** dan **kompleks**.
- Memiliki **ekosistem besar**:
  - Router (misalnya React Router),
  - State management (Redux, Zustand, dsb),
  - UI library (MUI, Chakra UI, dll).

Banyak framework modern dibangun di atas React, salah satunya yang akan kita bahas adalah **Next.js**.

---

## 6. Hubungan React dengan Materi Berikutnya

Di modul selanjutnya (Modul 2.3), kita akan melihat:

- Bagaimana **Next.js** menggunakan React di dalamnya.
- Bagaimana Next.js menambahkan:
  - Routing otomatis,
  - Struktur folder yang jelas,
  - Fitur tambahan seperti server-side rendering dan lainnya.

Kesimpulan:
- **React** = library untuk membangun UI dengan komponen.
- **Next.js** = framework yang menggunakan React di dalamnya dan menambahkan banyak fitur untuk membangun aplikasi web modern.

---

## Lampiran: Setup Project React Sederhana (Tanpa Next.js)

Bagian ini opsional, tapi bisa kamu ikuti kalau ingin langsung mencoba React di laptopmu.

Kita akan membuat project React sederhana menggunakan **Vite** dan **JavaScript (tanpa TypeScript dulu)**.

### 1. Persiapan Awal

Pastikan:

- Node.js sudah terpasang di komputer.
- Kamu bisa membuka **terminal** (Command Prompt / PowerShell / Terminal / VS Code terminal).

Untuk mengecek Node.js, jalankan:

```bash
node -v
```

Kalau muncul versi (misalnya ‎`v20.x.x`), berarti sudah siap.

2. Membuat Project React Baru dengan Vite ￼

Di terminal, jalankan perintah berikut:

```bash
npm create vite@latest my-react-app -- --template react
```

Penjelasan singkat:

- ‎`my-react-app` → nama folder project (boleh kamu ganti).

- ‎`--template react` → kita pilih template React + JavaScript.

Setelah perintah jalan, kamu akan diminta beberapa pilihan:

- Project name → tekan Enter saja kalau sudah sesuai.

- Template → pilih ‎`React` (bukan TypeScript).


Lalu masuk ke folder project:
```bash
cd my-react-app
npm install
```

3. Menjalankan Project React
```bash
npm run dev
```

Terminal akan menampilkan alamat, misalnya:
```bash
http://localhost:5173/
```


