# Modul 3.3 – REST API Dasar dengan Node.js (Express, tanpa Database)

Di modul ini kamu akan membangun **REST API sederhana** menggunakan **Node.js + Express**, dengan data yang masih disimpan di **memory (array)**.

Fokusnya:

- Memahami struktur dasar REST API.
- Membuat server HTTP dengan Express.
- Membuat endpoint CRUD sederhana (`GET`, `POST`, `PUT`, `DELETE`).
- Mencoba memanggil API menggunakan tool seperti Postman / Bruno / curl.

Ini adalah jembatan penting sebelum nanti kamu menambahkan **database** di modul berikutnya.

---

## 1. Apa itu REST API (Recap Singkat)

Di modul 3.1 kamu sudah kenalan dengan **API** dan **HTTP request–response**.  
Di sini kita fokus ke **REST API**, yaitu gaya desain API yang:

- Menggunakan **HTTP method** sebagai cara operasi:
  - `GET` → baca data
  - `POST` → buat data baru
  - `PUT/PATCH` → update data
  - `DELETE` → hapus data
- Menggunakan **URL** untuk merepresentasikan resource:
  - `/api/tasks`, `/api/users`, `/api/posts`, dll.

Contoh desain endpoint untuk resource `tasks`:

- `GET /api/tasks` → ambil semua task
- `GET /api/tasks/:id` → ambil satu task
- `POST /api/tasks` → buat task baru
- `PUT /api/tasks/:id` → update task
- `DELETE /api/tasks/:id` → hapus task

Di modul ini kita akan mengimplementasikan pola seperti itu.

---

## 2. Setup Project Express

Kita mulai dari project baru khusus untuk API ini.

1. Buat folder baru:

```bash
mkdir belajar-express-api
cd belajar-express-api
```
2. Inisialisasi project Node.js:
```bash
npm init -y
```

3. Install Express (framework web untuk Node.js):
```bash
npm install express
```
4. Buat file ‎`index.js`:
```bash
touch index.js
```

5. Isi ‎`index.js` dengan kode server dasar:
```js
// index.js
const express = require("express");
const app = express();
const PORT = 3000;

// Middleware agar Express bisa membaca JSON di body request
app.use(express.json());

// Route dasar untuk cek server
app.get("/", (req, res) => {
  res.json({ message: "API is running 🚀" });
});

app.listen(PORT, () => {
  console.log(`Server berjalan di http://localhost:${PORT}`);
});
```
6. Tambahkan script di ‎`package.json` supaya gampang dijalankan:
```js
{
  "name": "belajar-express-api",
  "version": "1.0.0",
  "main": "index.js",
  "scripts": {
    "start": "node index.js"
  },
  "dependencies": {
    "express": "^4.19.0"
  }
}
```

7. Jalankan server:
```bash
npm run start
```

Buka ‎`http://localhost:3000` di browser, kamu harus melihat respons JSON:
```
{ "message": "API is running 🚀" }
```

---

## 3. Menyimpan Data di Memory (Tanpa Database) ￼

Sebelum pakai database beneran, kita akan simpan data di array.

Tambahkan kode di atas route ‎`/`:
```js
// Data dummy in-memory (hilang kalau server di-restart)
let tasks = [
  { id: 1, title: "Belajar Node.js", completed: false },
  { id: 2, title: "Membangun REST API", completed: false }
];

let nextId = 3;
```
Kita akan membuat endpoint untuk mengelola ‎`tasks` ini.

---

## 4. Endpoint: GET /api/tasks (Read All) ￼

Tambahkan route berikut setelah route ‎`/`:
```js
// GET /api/tasks - ambil semua task
app.get("/api/tasks", (req, res) => {
  res.json(tasks);
});
```

Coba akses:

- Browser: ‎`http://localhost:3000/api/tasks`

- Atau Postman/Bruno/curl:
```
curl http://localhost:3000/api/tasks
```
Kamu akan dapat list task dalam bentuk JSON.

---

## 5. Endpoint: GET /api/tasks/:id (Read One) 

Tambahkan 
```js
// GET /api/tasks/:id - ambil satu task berdasarkan id
app.get("/api/tasks/:id", (req, res) => {
  const id = Number(req.params.id);
  const task = tasks.find((t) => t.id === id);

  if (!task) {
    return res.status(404).json({ error: "Task tidak ditemukan" });
  }

  res.json(task);
});
```

coba 
```
curl http://localhost:3000/api/tasks/1
curl http://localhost:3000/api/tasks/999
```
Kalau ‎`id` tidak ada, API akan mengembalikan status ‎`404`.

---

## 6. Endpoint: POST /api/tasks (Create) ￼

Sekarang kita tambahkan endpoint untuk menambah task baru.
```
// POST /api/tasks - buat task baru
app.post("/api/tasks", (req, res) => {
  const { title } = req.body;

  if (!title) {
    return res.status(400).json({ error: "Field 'title' wajib diisi" });
  }

  const newTask = {
    id: nextId++,
    title,
    completed: false
  };

  tasks.push(newTask);

  res.status(201).json(newTask);
});
```

Coba kirim request dengan Postman / Bruno:

- Method: ‎`POST`

- URL: ‎`http://localhost:3000/api/tasks`

- Body (JSON):
```
{
  "title": "Belajar Express"
}
```

Atau dengan curl:
```bash
curl -X POST http://localhost:3000/api/tasks \
  -H "Content-Type: application/json" \
  -d '{"title": "Belajar Express"}'
```
Respons:
```bash
{
  "id": 3,
  "title": "Belajar Express",
  "completed": false
}
```

---

## 7. Endpoint: PUT /api/tasks/:id (Update) ￼

Sekarang kita buat endpoint untuk mengubah task, misalnya mengubah judul atau status ‎`completed`.
```js
// PUT /api/tasks/:id - update task
app.put("/api/tasks/:id", (req, res) => {
  const id = Number(req.params.id);
  const { title, completed } = req.body;

  const taskIndex = tasks.findIndex((t) => t.id === id);

  if (taskIndex === -1) {
    return res.status(404).json({ error: "Task tidak ditemukan" });
  }

  // Update hanya field yang dikirim
  if (title !== undefined) {
    tasks[taskIndex].title = title;
  }

  if (completed !== undefined) {
    tasks[taskIndex].completed = Boolean(completed);
  }

  res.json(tasks[taskIndex]);
});
```

Contoh request (Postman / Bruno):

- Method: ‎`PUT`

- URL: ‎`http://localhost:3000/api/tasks/1`

- Body (JSON):

```bash
{
  "completed": true
}
```



## 8. Endpoint: DELETE /api/tasks/:id (Delete)

Terakhir, kita tambahkan endpoint untuk menghapus task.
```js
// DELETE /api/tasks/:id - hapus task
app.delete("/api/tasks/:id", (req, res) => {
  const id = Number(req.params.id);

  const taskIndex = tasks.findIndex((t) => t.id === id);

  if (taskIndex === -1) {
    return res.status(404).json({ error: "Task tidak ditemukan" });
  }

  const deletedTask = tasks[taskIndex];

  tasks.splice(taskIndex, 1);

  res.json({ message: "Task berhasil dihapus", task: deletedTask });
});
```

Contoh request:
```
curl -X DELETE http://localhost:3000/api/tasks/1
```

### 9. Struktur Akhir index.js ￼

Untuk memudahkan, berikut isi lengkap ‎`index.js` yang sudah berisi semua endpoint:
```js
// index.js
const express = require("express");
const app = express();
const PORT = 3000;

// Middleware untuk parsing JSON
app.use(express.json());

// Data dummy in-memory
let tasks = [
  { id: 1, title: "Belajar Node.js", completed: false },
  { id: 2, title: "Membangun REST API", completed: false }
];

let nextId = 3;

// Route dasar
app.get("/", (req, res) => {
  res.json({ message: "API is running 🚀" });
});

// GET /api/tasks - ambil semua task
app.get("/api/tasks", (req, res) => {
  res.json(tasks);
});

// GET /api/tasks/:id - ambil satu task
app.get("/api/tasks/:id", (req, res) => {
  const id = Number(req.params.id);
  const task = tasks.find((t) => t.id === id);

  if (!task) {
    return res.status(404).json({ error: "Task tidak ditemukan" });
  }

  res.json(task);
});

// POST /api/tasks - buat task baru
app.post("/api/tasks", (req, res) => {
  const { title } = req.body;

  if (!title) {
    return res.status(400).json({ error: "Field 'title' wajib diisi" });
  }

  const newTask = {
    id: nextId++,
    title,
    completed: false
  };

  tasks.push(newTask);

  res.status(201).json(newTask);
});

// PUT /api/tasks/:id - update task
app.put("/api/tasks/:id", (req, res) => {
  const id = Number(req.params.id);
  const { title, completed } = req.body;

  const taskIndex = tasks.findIndex((t) => t.id === id);

  if (taskIndex === -1) {
    return res.status(404).json({ error: "Task tidak ditemukan" });
  }

  if (title !== undefined) {
    tasks[taskIndex].title = title;
  }

  if (completed !== undefined) {
    tasks[taskIndex].completed = Boolean(completed);
  }

  res.json(tasks[taskIndex]);
});

// DELETE /api/tasks/:id - hapus task
app.delete("/api/tasks/:id", (req, res) => {
  const id = Number(req.params.id);

  const taskIndex = tasks.findIndex((t) => t.id === id);

  if (taskIndex === -1) {
    return res.status(404).json({ error: "Task tidak ditemukan" });
  }

  const deletedTask = tasks[taskIndex];

  tasks.splice(taskIndex, 1);

  res.json({ message: "Task berhasil dihapus", task: deletedTask });
});

app.listen(PORT, () => {
  console.log(`Server berjalan di http://localhost:${PORT}`);
});
```

## 10. Menghubungkan ke Modul Berikutnya ￼

Dengan modul 3.3 ini, kamu sudah:

- Membuat server HTTP dengan Express.

- Membuat endpoint REST API dasar (CRUD) untuk resource ‎`tasks`.

- Mencoba mengakses API dengan browser / Postman / curl.

Di modul berikutnya (Modul 4 – Database & CRUD), kamu akan:

- Memindahkan data dari array in-memory ke database beneran (misalnya PostgreSQL / Supabase).

- Tetap menggunakan pola endpoint yang sama, tapi sekarang datanya persisten (tidak hilang saat server restart).





