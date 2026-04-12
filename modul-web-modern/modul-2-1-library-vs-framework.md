# Modul 2.1 – Library vs Framework

Pada modul ini, kamu akan belajar:
- Apa itu *library* di dunia pemrograman (terutama web).
- Apa itu *framework* dan apa bedanya dengan library.
- Contoh-contoh library dan framework yang sering dipakai web developer.
- Kenapa penting memahami konsep ini sebelum belajar React dan Next.js.

---

## 1. Permasalahan di Pengembangan Web Manual

Di modul sebelumnya, kita sudah belajar membuat halaman web dengan:

- **HTML** untuk struktur.
- **CSS** untuk styling.
- **JavaScript** untuk interaktivitas.

Semua kita tulis **secara manual**. Cara ini bagus untuk belajar dasar, tapi saat proyek mulai membesar, akan muncul beberapa masalah:

- Banyak kode yang **berulang** (misalnya card, button, navbar, footer).
- File HTML bisa jadi **sangat panjang** dan sulit dibaca.
- Styling CSS bisa **berantakan** kalau tidak terstruktur.
- Menambah fitur baru sering membuat kode lama makin sulit di-maintain.

Di sinilah kita mulai butuh **alat bantu**: *library* dan *framework*.

---

## 2. Apa Itu Library?

Secara sederhana:

> **Library adalah kumpulan fungsi/kode yang bisa kita pakai untuk membantu menyelesaikan masalah tertentu.**

Ciri-ciri utama library:

- Kita yang **memanggil** library ketika butuh.
- Library biasanya fokus pada satu area tertentu, misalnya:
  - manipulasi tampilan,
  - HTTP request,
  - grafik/chart, dan lain-lain.

Beberapa contoh library di web development:

- **React** → library untuk membangun UI.
- **Axios** → library untuk melakukan HTTP request (GET, POST, dll).
- **Chart.js** → library untuk membuat grafik.

Analogi:

- Library seperti **kotak peralatan** di rumah.  
  Kalau butuh, kita ambil obeng/palu dari kotaknya, lalu kita yang pakai untuk memperbaiki sesuatu.

---

## 3. Apa Itu Framework?

Secara sederhana:

> **Framework adalah kerangka kerja yang sudah menentukan struktur dan pola sebuah aplikasi.**

Ciri-ciri utama framework:

- Framework biasanya sudah menentukan **cara kita menyusun kode** (struktur folder, nama file, pola umum).
- Framework sering memakai konsep *Inversion of Control*:
  - Bukan kita yang memanggil framework,
  - tapi **framework yang akan memanggil kode kita** di waktu yang tepat.

Beberapa contoh framework:

- **Next.js** (JavaScript/TypeScript, di atas React).
- **Laravel** (PHP).
- **Django** (Python).
- **Spring** (Java).

Analogi:

- Framework seperti **kerangka bangunan** yang sudah jadi.  
  Tiang, dinding utama, dan pondasi sudah ditentukan.  
  Tugas kita adalah mengisi ruangan-ruangan di dalam kerangka itu (misalnya: isi ruang tamu, kamar, dapur).

---

## 4. Perbedaan Library vs Framework

Secara ringkas:

**Library:**

- Kita yang mengontrol alur program.
- Kita memanggil fungsi/fitur dari library sesuai kebutuhan.
- Contoh:
  - Memanggil fungsi dari React untuk merender komponen.
  - Memanggil Axios untuk melakukan `axios.get('/api/users')`.

**Framework:**

- Framework mengontrol alur utama aplikasi.
- Framework memanggil kode kita pada titik-titik tertentu (misalnya saat ada request masuk).
- Contoh:
  - Next.js yang mengatur routing dan memanggil halaman kita.
  - Laravel yang memanggil controller kita ketika ada URL tertentu diakses.

Cara mudah mengingatnya:

- Library → *“Saya punya aplikasi, dan saya memakai library ini di dalamnya.”*
- Framework → *“Saya memakai framework ini, dan saya membangun aplikasi saya di dalamnya.”*

---

## 5. Kenapa Konsep Ini Penting untuk Web Developer?

Di dunia kerja, hampir semua aplikasi web modern memakai:

- Satu atau lebih **library** untuk membantu tugas tertentu (UI, HTTP, chart, dll).
- Satu **framework utama** untuk mengatur struktur aplikasi.

Dengan memahami perbedaan library vs framework:

- Kamu tidak hanya “ikut-ikutan pakai React/Next.js”.
- Kamu mengerti **peran** masing-masing alat di dalam sebuah project.
- Kamu bisa lebih mudah mempelajari teknologi lain yang konsepnya mirip  
  (misalnya: Angular, Vue, SvelteKit, Laravel, Django, dan sebagainya).

---

## 6. Menghubungkan ke Materi Berikutnya

Di modul-modul berikutnya, kita akan melihat contoh nyata:

- **React** sebagai sebuah **library** untuk membangun UI berbasis komponen.
- **Next.js** sebagai sebuah **framework** yang dibangun di atas React.

Saat membaca modul selanjutnya, coba ingat:

- “Bagian mana yang terasa seperti **library** (kita yang memanggil)?“
- “Bagian mana yang terasa seperti **framework** (kita mengikuti aturan dan struktur yang sudah disiapkan)?“
