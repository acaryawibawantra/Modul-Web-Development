# Modul 3.2 – Pengenalan Node.js & npm + Script CLI Sederhana

Di modul ini kamu akan mulai **praktek langsung** dengan backend menggunakan **Node.js**.  
Fokusnya:

- Mengenal apa itu Node.js dari sisi praktis.
- Memahami peran **npm** sebagai package manager.
- Membuat **project Node.js pertama**.
- Menulis **script CLI sederhana** di terminal.

Target akhirnya: kamu nyaman menjalankan JavaScript di **luar browser** dan siap lanjut ke pembuatan REST API di Modul 3.3.

---

## 1. Apa itu Node.js (Secara Praktis)

Secara sederhana:

- **Node.js** adalah _runtime_ yang memungkinkan kamu menjalankan **JavaScript di luar browser**, biasanya di server atau di terminal.
- Dengan Node.js, kamu bisa:
  - Bikin **web server**.
  - Bikin **tool CLI** (command line interface).
  - Menjalankan **script otomatisasi** (misal: generate file, deploy, dsb).

Perbedaan utama:

- Di browser, JavaScript berinteraksi dengan:
  - DOM (`document`, `window`, dll).
- Di Node.js, JavaScript berinteraksi dengan:
  - Sistem file (baca/tulis file).
  - Jaringan (buka port, kirim request).
  - Environment (variabel environment, process, dll).

---

## 2. Install & Cek Node.js + npm

Sebelum mulai, pastikan Node.js sudah terpasang.

1. Buka terminal (macOS: Terminal / iTerm).
2. Jalankan:

   ```bash
   node -v
   npm -v
   ```
Jika muncul versi (misal ‎`v20.x.x` dan ‎`10.x.x`), berarti Node.js dan npm sudah terinstall.

- npm (Node Package Manager) adalah tool untuk mengelola package/library JavaScript yang dipakai di project Node.js-mu.

---

## 3. Membuat Project Node.js Pertama

Sekarang kita buat project backend kecil.

1. Buat folder baru, misalnya:
```bash
mkdir belajar-node-cli
cd belajar-node-cli
```

2. Inisialisasi project Node.js:
```bash
npm init -y
```

Perintah ini akan membuat file ‎`package.json` yang menyimpan informasi project (nama, versi, script, dependencies, dll).

3. Buat file ‎`index.js`:
```bash
touch index.js
```

4. Isi ‎`index.js` dengan kode sederhana:
```bash
// index.js
console.log("Hello dari Node.js!");
```

5. Jalankan:
```bash
node index.js
```
Jika di terminal muncul tulisan ‎`Hello dari Node.js! 🚀⁠, artinya kamu sudah berhasil menjalankan JavaScript via Node.js.

---

## 4. Mengenal npm & External Packages ￼

Salah satu kekuatan Node.js ada di ekosistem npm (ribuan package siap pakai).

Contoh: kita pakai package ‎`chalk` untuk memberi warna di output terminal.

Salah satu kekuatan Node.js ada di ekosistem npm (ribuan package siap pakai).

Contoh: kita pakai package ‎`chalk` untuk memberi warna di output terminal.

1. Install package:
```bash
npm install chalk
```

2. Untuk mempermudah, kita pakai format CommonJS (tanpa ‎`type: "module"`).

Update ‎`index.js`:
```js
// index.js
const chalk = require("chalk");

console.log(chalk.green("Hello dari Node.js dengan warna hijau!"));
console.log(chalk.blue.bold("Welcome to backend world 🌐"));
```

3. Jalankan lagi:
```bash
node index.js
```
Kamu akan melihat teks berwarna di terminal.

- Intinya: npm memudahkan kamu menambahkan fitur lewat library buatan orang lain, tanpa harus menulis semuanya dari nol.

---

## 5. Membaca Input di Command Line (Script CLI Sederhana) ￼

Sekarang kita bikin script CLI sederhana: misalnya kalkulator penjumlahan dua angka dari argumen terminal.

```js
// index.js
const args = process.argv.slice(2); // ambil argumen setelah `node index.js`

if (args.length < 2) {
  console.log("Usage: node index.js <angka1> <angka2>");
  process.exit(1);
}

const a = Number(args[0]);
const b = Number(args[1]);

if (Number.isNaN(a) || Number.isNaN(b)) {
  console.log("Harap masukkan dua angka yang valid.");
  process.exit(1);
}

const hasil = a + b;

console.log(`Hasil penjumlahan ${a} + ${b} = ${hasil}`);
```

2. Jalankan dari terminal
```bash
node index.js 5 7
```

output
```
Hasil penjumlahan 5 + 7 = 12
```

---

## 6. Menambahkan Script di package.json 

Agar lebih rapi, kamu bisa menambahkan script di ‎`package.json`:
```json
{
  "name": "belajar-node-cli",
  "version": "1.0.0",
  "main": "index.js",
  "scripts": {
    "start": "node index.js"
  }
}
```

Sekarang kamu bisa menjalankan:
```bash
npm run start -- 3 4
```
npm akan menjalankan ‎`node index.js 3 4`.

link youtube belajar : https://youtu.be/LuY3f978a-A?si=y7zPR6YvTqJj4-Zu

---

## 7. Menghubungkan ke Learning Path
Di learning path, kamu sudah melewati:

- HTML → CSS → JavaScript → React → Frontend Apps

- npm → Tailwind CSS → React → Frontend Apps

Di Modul 3.2 ini, kamu mulai menyentuh bagian:

- Node.js → CLI APIs

Artinya:

- Kamu sudah bisa menjalankan JavaScript di server/terminal.

- Kamu sudah bisa menggunakan external packages via npm.

- Kamu sudah membuat script CLI yang bisa berkembang jadi tool internal.

Di modul berikutnya (Modul 3.3), kamu akan:

- Menggunakan Node.js untuk membuat web server.

- Membangun REST API dasar dengan Express (tanpa database dulu).

- Menyiapkan fondasi untuk CRUD + database di modul selanjutnya.

8. Ringkasan Modul 3.2 ￼

Setelah menyelesaikan Modul 3.2, kamu diharapkan:

- Paham apa itu Node.js secara praktis.

- Bisa menginisialisasi project Node.js dengan ‎`npm init`.

- Mengerti fungsi dasar npm dan cara menginstall package.

- Bisa menulis dan menjalankan script CLI sederhana dengan Node.js.

- Siap melangkah ke pembuatan REST API di Modul 3.3.








