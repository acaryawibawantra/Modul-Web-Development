# Modul 4.2 – REST API + Database (Express + Prisma)

Di modul ini kamu akan **mengupgrade REST API dari Modul 3.3** yang datanya masih di array, menjadi API yang datanya tersimpan di **database** menggunakan Prisma.

Fokusnya:

- Mengintegrasikan Prisma ke project Express.
- Mengubah semua endpoint CRUD agar baca/tulis ke database.
- Menambahkan endpoint untuk relasi (Event → Participants).
- Menangani error dengan lebih baik.

Target akhirnya: kamu punya **Event Registration API** yang datanya persisten — tidak hilang walau server di-restart.

---

## 1. Setup Project

Kita mulai dari project baru yang menggabungkan Express (Modul 3.3) dan Prisma (Modul 4.1).

1. Buat folder baru:

```bash
mkdir event-registration-api
cd event-registration-api
```

2. Inisialisasi project:

```bash
npm init -y
```

3. Install dependencies:

```bash
npm install express cors @prisma/client@5
npm install prisma@5 --save-dev
```

4. Inisialisasi Prisma:

```bash
npx prisma init --datasource-provider sqlite
```

---

## 2. Schema Prisma

Buka `prisma/schema.prisma` dan isi dengan schema Event Registration:

```prisma
generator client {
  provider = "prisma-client-js"
}

datasource db {
  provider = "sqlite"
  url      = env("DATABASE_URL")
}

model Event {
  id          Int           @id @default(autoincrement())
  title       String
  description String?
  date        DateTime
  location    String
  createdAt   DateTime      @default(now())
  participants Participant[]
}

model Participant {
  id        Int      @id @default(autoincrement())
  name      String
  email     String
  eventId   Int
  event     Event    @relation(fields: [eventId], references: [id])
  createdAt DateTime @default(now())
}
```

Jalankan migration:

```bash
npx prisma migrate dev --name init
```

---

## 3. Struktur File

Supaya kode lebih rapi, kita pisahkan ke beberapa file:

```
event-registration-api/
├── prisma/
│   └── schema.prisma
├── routes/
│   ├── events.js
│   └── participants.js
├── index.js
├── package.json
└── .env
```

Buat folder `routes/`:

```bash
mkdir routes
```

---

## 4. File Utama: index.js

Buat `index.js`:

```js
// index.js
const express = require("express");
const cors = require("cors");
const { PrismaClient } = require("@prisma/client");

const app = express();
const prisma = new PrismaClient();
const PORT = 3000;

// Middleware
app.use(cors());
app.use(express.json());

// Simpan prisma di app supaya bisa diakses di routes
app.set("prisma", prisma);

// Routes
const eventsRouter = require("./routes/events");
const participantsRouter = require("./routes/participants");

app.use("/api/events", eventsRouter);
app.use("/api/participants", participantsRouter);

// Route dasar
app.get("/", (req, res) => {
  res.json({ message: "Event Registration API is running" });
});

app.listen(PORT, () => {
  console.log(`Server berjalan di http://localhost:${PORT}`);
});
```

Perhatikan perbedaan dengan Modul 3.3:

- Tidak ada lagi array `let tasks = [...]` — data ada di database.
- Routes dipisah ke file sendiri.
- Prisma Client diinisialisasi sekali dan di-share ke semua routes.
- CORS sudah diaktifkan agar frontend bisa mengakses API.

---

## 5. Routes: Events (CRUD Lengkap)

Buat file `routes/events.js`:

```js
// routes/events.js
const express = require("express");
const router = express.Router();

// GET /api/events — ambil semua event
router.get("/", async (req, res) => {
  const prisma = req.app.get("prisma");

  const events = await prisma.event.findMany({
    include: { participants: true },
    orderBy: { date: "asc" }
  });

  res.json(events);
});

// GET /api/events/:id — ambil satu event
router.get("/:id", async (req, res) => {
  const prisma = req.app.get("prisma");
  const id = Number(req.params.id);

  const event = await prisma.event.findUnique({
    where: { id },
    include: { participants: true }
  });

  if (!event) {
    return res.status(404).json({ error: "Event tidak ditemukan" });
  }

  res.json(event);
});

// POST /api/events — buat event baru
router.post("/", async (req, res) => {
  const prisma = req.app.get("prisma");
  const { title, description, date, location } = req.body;

  if (!title || !date || !location) {
    return res.status(400).json({
      error: "Field 'title', 'date', dan 'location' wajib diisi"
    });
  }

  const event = await prisma.event.create({
    data: {
      title,
      description: description || null,
      date: new Date(date),
      location
    }
  });

  res.status(201).json(event);
});

// PUT /api/events/:id — update event
router.put("/:id", async (req, res) => {
  const prisma = req.app.get("prisma");
  const id = Number(req.params.id);
  const { title, description, date, location } = req.body;

  const existing = await prisma.event.findUnique({ where: { id } });

  if (!existing) {
    return res.status(404).json({ error: "Event tidak ditemukan" });
  }

  const updated = await prisma.event.update({
    where: { id },
    data: {
      ...(title !== undefined && { title }),
      ...(description !== undefined && { description }),
      ...(date !== undefined && { date: new Date(date) }),
      ...(location !== undefined && { location })
    }
  });

  res.json(updated);
});

// DELETE /api/events/:id — hapus event (beserta participants)
router.delete("/:id", async (req, res) => {
  const prisma = req.app.get("prisma");
  const id = Number(req.params.id);

  const existing = await prisma.event.findUnique({ where: { id } });

  if (!existing) {
    return res.status(404).json({ error: "Event tidak ditemukan" });
  }

  // Hapus participants dulu (karena ada relasi)
  await prisma.participant.deleteMany({ where: { eventId: id } });

  const deleted = await prisma.event.delete({ where: { id } });

  res.json({ message: "Event berhasil dihapus", event: deleted });
});

module.exports = router;
```

---

## 6. Routes: Participants

Buat file `routes/participants.js`:

```js
// routes/participants.js
const express = require("express");
const router = express.Router();

// GET /api/participants — ambil semua participant
router.get("/", async (req, res) => {
  const prisma = req.app.get("prisma");

  const participants = await prisma.participant.findMany({
    include: { event: true },
    orderBy: { createdAt: "desc" }
  });

  res.json(participants);
});

// POST /api/participants — daftarkan participant ke event
router.post("/", async (req, res) => {
  const prisma = req.app.get("prisma");
  const { name, email, eventId } = req.body;

  if (!name || !email || !eventId) {
    return res.status(400).json({
      error: "Field 'name', 'email', dan 'eventId' wajib diisi"
    });
  }

  // Cek apakah event-nya ada
  const event = await prisma.event.findUnique({
    where: { id: Number(eventId) }
  });

  if (!event) {
    return res.status(404).json({ error: "Event tidak ditemukan" });
  }

  // Cek apakah email sudah terdaftar di event yang sama
  const existing = await prisma.participant.findFirst({
    where: {
      email,
      eventId: Number(eventId)
    }
  });

  if (existing) {
    return res.status(409).json({
      error: "Email sudah terdaftar di event ini"
    });
  }

  const participant = await prisma.participant.create({
    data: {
      name,
      email,
      eventId: Number(eventId)
    }
  });

  res.status(201).json(participant);
});

// DELETE /api/participants/:id — hapus participant
router.delete("/:id", async (req, res) => {
  const prisma = req.app.get("prisma");
  const id = Number(req.params.id);

  const existing = await prisma.participant.findUnique({ where: { id } });

  if (!existing) {
    return res.status(404).json({ error: "Participant tidak ditemukan" });
  }

  const deleted = await prisma.participant.delete({ where: { id } });

  res.json({ message: "Participant berhasil dihapus", participant: deleted });
});

module.exports = router;
```

---

## 7. Seed Data Awal

Supaya API tidak kosong saat pertama kali dijalankan, buat file `seed.js`:

```js
// seed.js
const { PrismaClient } = require("@prisma/client");
const prisma = new PrismaClient();

async function main() {
  // Buat beberapa event
  const workshop = await prisma.event.create({
    data: {
      title: "GDGoC Web Dev Workshop",
      description: "Workshop web development dari dasar sampai full-stack",
      date: new Date("2026-07-15T09:00:00"),
      location: "Gedung Robotika ITS"
    }
  });

  const hackathon = await prisma.event.create({
    data: {
      title: "GDGoC Hackathon 2026",
      description: "Hackathon 24 jam untuk mahasiswa ITS",
      date: new Date("2026-08-20T08:00:00"),
      location: "Graha ITS"
    }
  });

  // Tambah participants
  await prisma.participant.createMany({
    data: [
      { name: "Budi Santoso", email: "budi@example.com", eventId: workshop.id },
      { name: "Ani Wijaya", email: "ani@example.com", eventId: workshop.id },
      { name: "Candra Putra", email: "candra@example.com", eventId: hackathon.id }
    ]
  });

  console.log("Seed data berhasil ditambahkan!");
}

main()
  .catch((e) => {
    console.error(e);
    process.exit(1);
  })
  .finally(async () => {
    await prisma.$disconnect();
  });
```

Jalankan seed:

```bash
node seed.js
```

---

## 8. Testing API

Jalankan server:

```bash
node index.js
```

Coba semua endpoint dengan Postman, Bruno, atau curl:

**Ambil semua event:**

```bash
curl http://localhost:3000/api/events
```

**Buat event baru:**

```bash
curl -X POST http://localhost:3000/api/events \
  -H "Content-Type: application/json" \
  -d '{
    "title": "Info Session",
    "date": "2026-09-01T10:00:00",
    "location": "Online via Zoom"
  }'
```

**Daftarkan participant:**

```bash
curl -X POST http://localhost:3000/api/participants \
  -H "Content-Type: application/json" \
  -d '{
    "name": "Dewi Lestari",
    "email": "dewi@example.com",
    "eventId": 1
  }'
```

**Restart server, lalu GET lagi** — data tetap ada! Ini bedanya dengan Modul 3.3.

```bash
# Ctrl+C untuk stop server
node index.js
curl http://localhost:3000/api/events
# Data masih ada karena tersimpan di database
```

---

## 9. Perbandingan: Sebelum vs Sesudah Database

| Aspek | Modul 3.3 (Array) | Modul 4.2 (Prisma + SQLite) |
|-------|-------|-------|
| Penyimpanan | `let tasks = [...]` di memory | File `dev.db` di disk |
| Restart server | Data hilang | Data tetap ada |
| Relasi antar data | Tidak ada | Event → Participants |
| Validasi duplikat | Manual | Query database |
| Sorting & filtering | Manual dengan `.filter()` | Prisma query (`orderBy`, `where`) |

---

## 10. Ringkasan Modul 4.2

Setelah menyelesaikan modul ini, kamu diharapkan:

- Bisa mengintegrasikan Prisma ke project Express.
- Memahami pola routes terpisah (`routes/events.js`, `routes/participants.js`).
- Bisa membangun endpoint CRUD yang baca/tulis ke database.
- Bisa menangani relasi antar model (Event → Participant).
- Bisa melakukan validasi dasar (field wajib, duplikat email).
- Membuktikan bahwa data **persisten** setelah restart server.

Pada **Modul 4.3**, kita akan:

- Membuat frontend dengan **Next.js** yang mengakses API ini.
- Menampilkan daftar event dari database.
- Membuat form registrasi yang mengirim data ke API.
- Menghubungkan frontend dan backend menjadi satu aplikasi **full-stack**.
