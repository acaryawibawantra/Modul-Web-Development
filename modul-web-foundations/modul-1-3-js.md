---
title: "Modul 1.3: Dasar-dasar JavaScript"
date: 2026-03-11
weight: 3
description: "Menambahkan interaktivitas dan logika pemrograman ke dalam website dengan JavaScript."
categories: ["Web Development", "GDGOC ITS"]
tags: ["html", "css", "javascript", "gdgoc"]
showToc: true
TocOpen: false
---

# 1. Apa itu JavaScript?

**JavaScript** adalah bahasa pemrograman lintas platform yang berorientasi objek yang digunakan untuk membuat halaman web menjadi interaktif (misalnya: animasi yang kompleks, tombol yang bisa diklik, menu popup, dll.). 

Selain di browser (Client-side), JavaScript juga bisa berjalan di sisi server (**Server-side**) menggunakan runtime seperti **Node.js**, yang memungkinkan penambahan fungsi yang lebih canggih seperti kolaborasi real-time antar pengguna. Di dalam browser, JavaScript terhubung dengan objek-objek di lingkungannya untuk memberikan kontrol programatik atas mereka.

# 2. Lingkungan (Environment) JavaScript

JavaScript adalah bahasa yang serbaguna karena bisa berjalan di sisi klien (browser) maupun sisi server. Setiap lingkungan menyediakan alat dan API yang berbeda sesuai tugasnya.

### Client-Side JavaScript (Browser)

Lingkungan ini merujuk pada JavaScript yang berjalan langsung di browser pengguna. Fokus utamanya adalah membuat halaman web yang interaktif dan dinamis.

**Fitur Utama:**
1.  **Global Object: `window`**: Memberikan akses ke API browser (seperti `window.alert()`).
2.  **Manipulasi DOM**: JavaScript dapat mengakses dan mengubah HTML serta CSS halaman web melalui *Document Object Model* (DOM).
    ```js
    document.getElementById("contoh").textContent = "Halo dari Client!";
    ```
3.  **Browser APIs**: `fetch` (permintaan HTTP), `localStorage` (penyimpanan data), `Canvas` (grafik), dll.
4.  **Event Handling**: Mendengarkan aksi pengguna seperti klik atau ketik.
    ```js
    document.querySelector("button").addEventListener("click", () => {
      alert("Tombol diklik!");
    });
    ```

### Server-Side JavaScript (Runtime)

Merujuk pada JavaScript yang berjalan di luar browser, biasanya di server menggunakan **Node.js**, **Deno**, atau **Bun**.

**Fitur Utama:**
1.  **Global Object: `global`**: Tidak memiliki objek `window` atau `document`.
2.  **Server APIs**: `fs` (File System untuk baca/tulis file), `http` (untuk membuat server), `process` (info runtime).
    ```js
    const fs = require("fs");
    fs.writeFileSync("pesan.txt", "Halo dari Server!");
    ```
3.  **Package Management**: Menggunakan `npm` atau `yarn` untuk mengelola library eksternal.

### Perbandingan Client-Side vs Server-Side

| **Aspek**                 | **Client-Side**                          | **Server-Side**                         |
| ------------------------- | ---------------------------------------- | --------------------------------------- |
| **Objek Global**          | `window`, `globalThis`                   | `global`, `globalThis`                  |
| **Kegunaan Utama**        | Interaksi UI, Manipulasi DOM             | Logika Backend, Interaksi Database      |
| **API Utama**             | DOM, Canvas, `fetch`, Web Storage        | `fs`, `http`, `process`, `os`           |
| **Tempat Eksekusi**       | Browser                                  | Node.js, Deno, Bun                      |
| **Akses File System**     | Tidak Bisa (Keamanan)                    | Bisa                                    |

---

# 3. Manipulasi DOM (Document Object Model)

Kemampuan paling kuat dari JavaScript di browser adalah berinteraksi dengan elemen HTML secara langsung melalui objek `document`.

### A. Memilih Elemen
Gunakan fungsi-fungsi ini untuk "menangkap" elemen HTML:
```js
const judul = document.getElementById("judul-utama");
const tombol = document.querySelector(".btn-submit");
const daftarItem = document.querySelectorAll("li"); // Menghasilkan daftar elemen
```

### B. Mengubah Konten dan Gaya
```js
const pesan = document.getElementById("pesan");
pesan.textContent = "Halo, GDGOC ITS!"; // Mengubah teks
pesan.style.color = "blue";             // Mengubah warna via CSS
```

### C. Event Listener (Interaksi)
Mendengarkan kejadian seperti klik.
```js
const tombol = document.getElementById("tombolGantiWarna");
tombol.addEventListener("click", function() {
    document.body.style.backgroundColor = "lightblue";
});
```

### D. Menambahkan Elemen Baru
```js
const btnTambah = document.getElementById("tambahNama");
const daftar = document.getElementById("daftarNama");

btnTambah.addEventListener("click", () => {
    const liBaru = document.createElement("li"); // Buat tag <li>
    liBaru.textContent = "Peserta Baru";         // Isi teks
    daftar.appendChild(liBaru);                  // Masukkan ke dalam <ul>
});
```

---

# 4. Dasar Pemrograman JavaScript

### Variabel dan Deklarasi

Ada tiga cara mendeklarasikan variabel:
-   **`const`**: Untuk nilai tetap (konstanta). Tidak bisa diubah setelah diisi. (**Disarankan**).
-   **`let`**: Untuk nilai yang bisa berubah. Memiliki cakupan blok (*block scope*).
-   **`var`**: Cara lama (sebelum ES6). Tidak disarankan karena cakupannya tidak terbatas pada blok.

### Tipe Data
JavaScript memiliki beberapa tipe data dasar:
1.  **String**: Teks (contoh: `"Halo"`).
2.  **Number**: Angka (contoh: `42`, `3.14`).
3.  **Boolean**: `true` atau `false`.
4.  **Object**: Kumpulan data (contoh: `{ nama: "Acarya", usia: 20 }`).
5.  **Array**: Daftar data berurutan.
6.  **null** & **undefined**: Nilai kosong atau belum terdefinisi.

### Struktur Kontrol (Logic)

**1. Pengkondisian (If-Else)**
```js
if (usia >= 18) {
  console.log("Sudah Dewasa");
} else {
  console.log("Belum Dewasa");
}
```

**2. Perulangan (Loops)**
```js
// For Loop
for (let i = 0; i < 5; i++) {
  console.log("Perulangan ke-" + i);
}

// For-of (Untuk Array)
const buah = ["Apel", "Mangga"];
for (let b of buah) {
  console.log(b);
}
```

### Functions (Fungsi)

Fungsi adalah blok kode yang dirancang untuk melakukan tugas tertentu. Fungsi memungkinkan kita menulis kode yang modular dan bisa digunakan kembali.

**1. Deklarasi Fungsi**
```javascript
function sapa(nama) {
  return "Halo, " + nama;
}
```

**2. Arrow Function (ES6)**
Sintaks yang lebih singkat dan modern.
```javascript
const tambah = (a, b) => a + b;
```

---

### Struktur Data Dasar (Object & Array)

**1. Object**
Digunakan untuk menyimpan kumpulan data dalam bentuk pasangan `key: value`.
```javascript
const user = {
  nama: "Acarya",
  peran: "Instruktur",
  aktif: true
};

console.log(user.nama); // Output: Acarya
```

**2. Array**
Digunakan untuk menyimpan daftar data berurutan.
```javascript
const materi = ["HTML", "CSS", "JS"];

console.log(materi[0]); // Output: HTML
console.log(materi.length); // Output: 3

// Menambah data
materi.push("React");
```

---

# 5. Penanganan Error dan Alur Kontrol

### Exception Handling (`try...catch`)

Digunakan untuk menangani error agar aplikasi tidak langsung berhenti (crash).

```javascript
try {
  // Kode yang mungkin error
  let hasil = variabelYangBelumAda + 10;
} catch (error) {
  // Apa yang harus dilakukan jika terjadi error
  console.log("Terjadi error: " + error.message);
} finally {
  // Kode yang akan SELALU berjalan
  console.log("Proses selesai.");
}
```

---

# 6. Pemrograman Asinkron (Asynchronous)

Asynchronous memungkinkan JavaScript melakukan tugas berat (seperti mengambil data dari internet) tanpa membekukan tampilan website.

**1. Promises**
Janji bahwa suatu data akan tersedia di masa depan.
```javascript
fetch("https://api.github.com/users/gdgoc-its")
  .then(response => response.json())
  .then(data => console.log(data))
  .catch(err => console.error(err));
```

**2. Async / Await**
Cara paling modern dan mudah dibaca untuk menangani proses asinkron.
```javascript
async function ambilData() {
  try {
    const response = await fetch("https://api.example.com/data");
    const data = await response.json();
    console.log(data);
  } catch (error) {
    console.error("Gagal mengambil data:", error);
  }
}
```

---

### Pelajari Lebih Lanjut:
-   [MDN Web Docs - JavaScript Guide](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide)
-   [JavaScript.info](https://javascript.info/)
-   [W3Schools JS Tutorial](https://www.w3schools.com/js/)

---

#### **Anonymous Functions**

Functions without a name, often used as arguments in other functions.

```javascript
setTimeout(function () {
  console.log("This runs after 2 seconds.");
}, 2000);
```

---

#### **Immediately Invoked Function Expression (IIFE)**

A function executed immediately after it's defined.

```javascript
(function () {
  console.log("IIFE is executed!");
})();
```

---

#### **Arrow Functions**

1. **Single Expression (Implicit Return)**

   ```javascript
   const square = (x) => x * x;
   console.log(square(4)); // Output: 16
   ```

2. **Multiple Parameters**

   ```javascript
   const multiply = (a, b) => a * b;
   console.log(multiply(3, 4)); // Output: 12
   ```

3. **No Parameters**
   ```javascript
   const greet = () => console.log("Hello!");
   greet(); // Output: Hello!
   ```

---

#### **Higher-Order Functions**

Functions that take other functions as arguments or return functions.

```javascript
function applyOperation(a, b, operation) {
  return operation(a, b);
}

let result = applyOperation(3, 4, (x, y) => x + y);
console.log(result); // Output: 7
```

---

#### **Function Scope and `this`**

1. **`this` in Regular Functions**
   The value of `this` depends on how the function is called.

   ```javascript
   const obj = {
     name: "Alice",
     greet: function () {
       console.log("Hello, " + this.name);
     },
   };
   obj.greet(); // Output: Hello, Alice
   ```

2. **`this` in Arrow Functions**
   Arrow functions do not bind their own `this`; they inherit it from the surrounding context.
   ```javascript
   const obj = {
     name: "Alice",
     greet: () => {
       console.log("Hello, " + this.name);
     },
   };
   obj.greet(); // Output: Hello, undefined
   ```

---

#### **Best Practices**

1. Use **arrow functions** for concise syntax when `this` is not needed.
2. Use **default parameters** to make functions more robust.
3. Use **IIFE** for code isolation in global scope.
4. Keep functions **small and focused** on a single task.
5. Always **name your functions** for better debugging unless explicitly using anonymous functions.

### Asynchronous Programming

In JavaScript, **asynchronous programming** allows you to perform tasks that take time (like fetching data from a server) without blocking the execution of other code. It ensures the application remains responsive, especially in environments like browsers, where users interact with the UI.

---

#### **Key Concepts in Asynchronous JavaScript**

1. **Synchronous vs Asynchronous**

   - **Synchronous**: Tasks are executed one after another, blocking the execution of subsequent tasks until the current one finishes.

     ```javascript
     console.log("Task 1");
     console.log("Task 2");
     console.log("Task 3");
     // Output: Task 1, Task 2, Task 3 (in order)
     ```

   - **Asynchronous**: Tasks can start, pause, and resume independently without blocking subsequent code.
     ```javascript
     console.log("Task 1");
     setTimeout(() => console.log("Task 2 (async)"), 1000);
     console.log("Task 3");
     // Output: Task 1, Task 3, Task 2 (async) (Task 2 runs after 1 second)
     ```

2. **Event Loop**
   JavaScript uses an **event loop** to manage asynchronous operations. It processes tasks in the call stack, handles asynchronous callbacks in the task queue, and ensures the main thread stays responsive.

---

#### **Ways to Handle Asynchronous Code**

1. **Callbacks**

   A function passed as an argument to another function and executed after an asynchronous task completes.

   **Example**:

   ```javascript
   function fetchData(callback) {
     setTimeout(() => {
       console.log("Data fetched");
       callback();
     }, 1000);
   }

   fetchData(() => {
     console.log("Callback executed");
   });
   ```

   **Drawback**: Can lead to "callback hell" when there are nested callbacks.

---

2. **Promises**

   Promises represent a value that will be available now, later, or never.

   **Example**:

   ```javascript
   const fetchData = new Promise((resolve, reject) => {
     setTimeout(() => {
       resolve("Data fetched");
     }, 1000);
   });

   fetchData
     .then((result) => console.log(result)) // Output: Data fetched
     .catch((error) => console.error(error));
   ```

   - **States of a Promise**:
   - **Pending**: Initial state.
   - **Fulfilled**: The operation completed successfully (`resolve` is called).
   - **Rejected**: The operation failed (`reject` is called).

---

3. **Async/Await**

   Introduced in ES8, `async/await` provides a simpler way to handle asynchronous code.

   **Example**:

   ```javascript
   const fetchData = () => {
     return new Promise((resolve) => {
       setTimeout(() => {
         resolve("Data fetched");
       }, 1000);
     });
   };

   const getData = async () => {
     console.log("Fetching data...");
     const data = await fetchData(); // Pauses here until the promise resolves
     console.log(data);
   };

   getData();
   // Output:
   // Fetching data...
   // Data fetched
   ```

   - **`async`**: Marks a function as asynchronous, which returns a promise.
   - **`await`**: Pauses the execution of the `async` function until the promise resolves or rejects.

---

#### **Common Asynchronous Use Cases**

1. **Fetching Data**

   ```javascript
   fetch("https://jsonplaceholder.typicode.com/posts/1")
     .then((response) => response.json())
     .then((data) => console.log(data))
     .catch((error) => console.error(error));
   ```

2. **Using Async/Await for Fetch**

   ```javascript
   const getPost = async () => {
     try {
       const response = await fetch(
         "https://jsonplaceholder.typicode.com/posts/1"
       );
       const data = await response.json();
       console.log(data);
     } catch (error) {
       console.error("Error fetching data:", error);
     }
   };

   getPost();
   ```

---

#### **Best Practices for Asynchronous Code**

1. **Avoid Callback Hell**: Use Promises or Async/Await instead of deeply nested callbacks.
2. **Handle Errors Gracefully**: Use `.catch` with Promises or `try...catch` with `async/await`.
3. **Keep Async Code Modular**: Break tasks into smaller functions for better readability.
4. **Use Concurrent Operations**: Run multiple asynchronous tasks simultaneously when possible (e.g., `Promise.all`).
```