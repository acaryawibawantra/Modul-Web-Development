# Modul 3.1 – Konsep Backend & Arsitektur Web Modern

Pada modul ini kamu akan belajar **apa itu backend**, bagaimana cara kerjanya, dan di mana posisi backend dalam **arsitektur web modern** yang sudah menggunakan React, Next.js, dan (nantinya) Node.js + database.

Tujuannya bukan langsung ngoding, tapi membangun *mental model* dulu supaya ketika nanti menulis kode backend dengan Node.js kamu sudah paham konteks besarnya.

---

## 1. Frontend vs Backend

Sebelum masuk ke backend, kita recap dulu:

- **Frontend**  
  Bagian aplikasi web yang **berhadapan langsung dengan user** (user interface).  
  Biasanya dijalankan di **browser**:
  - HTML → struktur konten
  - CSS → tampilan & layout
  - JavaScript / React / Next.js → interaksi & logika di sisi client

- **Backend**  
  Bagian aplikasi yang berjalan di **server**, tidak langsung terlihat oleh user.  
  Tugas utamanya:
  - Menerima **request** dari client (browser / aplikasi lain)
  - Memproses data atau logika bisnis
  - Berkomunikasi dengan **database** atau layanan lain
  - Mengirim **response** kembali (biasanya dalam bentuk JSON)

> Singkatnya: **frontend** = “yang dilihat dan di-klik”, **backend** = “otak dan dapur” di balik layar.

---

## 2. Client–Server & HTTP Request–Response

Web modern dibangun di atas model **client–server**.

- **Client**: browser (Chrome, Firefox, Edge, dll) atau aplikasi lain yang mengirim permintaan.
- **Server**: program yang selalu “standby” mendengarkan permintaan, lalu membalas.

Komunikasi antara client dan server terjadi lewat **HTTP**.

Alurnya:

1. Client mengirim **HTTP request** ke server:
   - Method: `GET`, `POST`, `PUT`, `DELETE`, dll.
   - URL: contoh `https://example.com/api/users`
   - Optional: body, header, token, dll.

2. Server menerima request, memproses:
   - Baca parameter/path/body
   - Ambil / simpan data ke database
   - Jalankan logika bisnis

3. Server mengirim kembali **HTTP response**:
   - Status code: `200`, `201`, `400`, `404`, `500`, dll.
   - Body: bisa berupa HTML, JSON, file, dll.

Di modul-modul backend berikutnya, kamu akan **menulis program server** yang:

- Mendengarkan request di port tertentu
- Menentukan apa yang harus dilakukan untuk setiap route
- Mengirim response dalam bentuk JSON (REST API)

---

## 3. Arsitektur Web Modern (Frontend + Backend + Database)

Sekarang kita hubungkan dengan apa yang sudah kamu pelajari:

- **Modul 1 – Web Foundations**
  - HTML, CSS, JavaScript:
    - Bisa bikin website statis dan interaktif
- **Modul 2 – Web Modern**
  - React, Next.js, Tailwind CSS:
    - Bisa bikin **frontend modern** berbasis komponen

Tapi, di aplikasi nyata, frontend saja tidak cukup.

Biasanya kita juga butuh:

- **Backend** (contoh: Node.js)
  - Menyediakan **API** untuk diakses frontend
  - Menyimpan & mengambil data
  - Menjalankan aturan bisnis (business logic)
- **Database** (contoh: PostgreSQL)
  - Tempat menyimpan data secara permanen

Gambaran sederhananya:

- User → buka website React/Next.js (frontend)
- Frontend → kirim request ke backend (Node.js) lewat HTTP
- Backend → baca/ubah data di database
- Backend → kirim response JSON ke frontend
- Frontend → update tampilan berdasarkan data dari backend

Modul 3 ini akan fokus di **bagian backend (Node.js) dan API**, sebelum nanti menyentuh database lebih dalam.

---

## 4. Apa Itu API dan Kenapa Penting?

**API (Application Programming Interface)** di konteks web biasanya berarti **HTTP API**: sebuah interface yang bisa dipanggil lewat HTTP request.

Contoh:

- `GET /api/posts` → ambil semua post
- `POST /api/posts` → buat post baru
- `PUT /api/posts/:id` → edit post
- `DELETE /api/posts/:id` → hapus post

Kenapa API penting?

- Memisahkan **frontend** dan **backend**:
  - Frontend tidak perlu tahu bagaimana data disimpan
  - Frontend hanya perlu tahu:
    - “Kalau aku `GET /api/posts`, aku dapat list post”
- Memudahkan integrasi:
  - Satu API bisa dipakai oleh banyak client:
    - Website, mobile app, service lain, dll.

Di Modul 3.3 nanti, kamu akan membangun **REST API sederhana** dengan Node.js + Express.

---

## 5. Posisi Node.js di Learning Path

Kalau kita lihat kembali learning path yang kamu pakai:

- HTML → CSS → JavaScript → Static Webpages → Interactivity  
- npm → Tailwind CSS → React → Frontend Apps  
- **Node.js → CLI APIs → PostgreSQL → CRUD Apps → RESTful APIs → JWT Auth → Complete App → Deployment**

Kamu sudah menyentuh:

- HTML, CSS, JS (Modul 1)
- React, Next.js, Tailwind (Modul 2)

Sekarang, **Node.js** muncul sebagai langkah berikutnya:

- Dengan Node.js, kamu bisa:
  - Menjalankan JavaScript di **server**
  - Membuat **CLI tools** (program terminal)
  - Membuat **web server** dan **REST API**

Modul 3 akan membawa kamu melewati:

- 3.1 → konsep backend & arsitektur
- 3.2 → Node.js & npm + script CLI
- 3.3 → REST API dasar dengan Express

---

## 6. Ringkasan Modul 3.1

Setelah menyelesaikan Modul 3.1 ini, kamu diharapkan:

- Memahami perbedaan **frontend vs backend**.
- Mengerti konsep **client–server** dan alur **HTTP request–response**.
- Paham gambaran besar arsitektur web modern (frontend React/Next + backend Node.js + database).
- Tahu apa itu **API/REST API** dan kenapa itu penting untuk aplikasi web modern.
- Melihat di mana posisi **Node.js** di learning path yang akan kamu ikuti.

Pada **Modul 3.2**, kita akan mulai **praktek langsung** dengan:

- Install & setup Node.js
- Kenalan dengan `npm`
- Membuat **script CLI sederhana** menggunakan JavaScript di Node.js
