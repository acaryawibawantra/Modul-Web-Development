# Modul 4.1 – Pengenalan Database & Prisma ORM

Di modul ini kamu akan belajar **apa itu database**, kenapa data perlu disimpan secara permanen, dan bagaimana cara menggunakan **Prisma ORM** untuk berinteraksi dengan database dari Node.js.

Fokusnya:

- Memahami konsep database dan perbedaan SQL vs NoSQL.
- Setup database **SQLite** (tanpa install apapun).
- Mengenal **Prisma** sebagai ORM modern untuk Node.js.
- Membuat schema, menjalankan migration, dan melakukan operasi CRUD lewat Prisma.

Target akhirnya: kamu siap mengintegrasikan Prisma ke REST API Express di Modul 4.2.

---

## 1. Kenapa Butuh Database?

Di Modul 3.3, data `tasks` disimpan di **array JavaScript**:

```js
let tasks = [
  { id: 1, title: "Belajar Node.js", completed: false },
  { id: 2, title: "Membangun REST API", completed: false }
];
```

Masalahnya:

- **Data hilang** setiap kali server di-restart.
- **Tidak bisa di-share** antar proses atau server.
- **Tidak bisa di-query** secara efisien kalau datanya besar.

Database menyelesaikan semua masalah ini. Data disimpan di **disk**, bertahan selamanya (persisten), dan bisa di-query dengan cepat.

---

## 2. SQL vs NoSQL (Singkat)

Ada dua jenis database utama:

| | SQL (Relational) | NoSQL (Non-Relational) |
|---|---|---|
| **Struktur** | Tabel dengan baris & kolom (seperti spreadsheet) | Dokumen JSON, key-value, graph, dll |
| **Contoh** | PostgreSQL, MySQL, SQLite | MongoDB, Redis, Firebase |
| **Schema** | Ketat — harus didefinisikan dulu | Fleksibel — bisa berubah-ubah |
| **Relasi** | Kuat — JOIN antar tabel | Terbatas — biasanya embed di dokumen |
| **Kapan pakai** | Data terstruktur, relasi jelas | Data fleksibel, skala horizontal |

Di modul ini kita pakai **SQLite** (SQL) karena:

- **Zero config** — tidak perlu install database server, cukup satu file.
- **Cocok untuk belajar** — syntax SQL standar.
- **Mudah migrasi** — kalau nanti mau pindah ke PostgreSQL, tinggal ganti connection string.

---

## 3. Apa Itu ORM dan Kenapa Pakai Prisma?

**ORM (Object-Relational Mapping)** adalah tool yang memungkinkan kamu berinteraksi dengan database **lewat kode JavaScript/TypeScript**, tanpa harus menulis SQL mentah.

Tanpa ORM (SQL mentah):

```sql
SELECT * FROM tasks WHERE completed = false;
```

Dengan Prisma:

```js
const tasks = await prisma.task.findMany({
  where: { completed: false }
});
```

Kenapa Prisma?

- **Type-safe** — auto-complete dan error checking saat coding.
- **Migration otomatis** — schema berubah → database ikut berubah.
- **Prisma Studio** — GUI untuk melihat dan mengedit data langsung.
- **Populer di ekosistem Next.js** — banyak dipakai di proyek modern.

---

## 4. Setup Project

Kita buat project baru untuk belajar Prisma.

1. Buat folder baru:

```bash
mkdir belajar-prisma
cd belajar-prisma
```

2. Inisialisasi project Node.js:

```bash
npm init -y
```

3. Install Prisma sebagai dev dependency dan Prisma Client:

```bash
npm install prisma@5 --save-dev
npm install @prisma/client@5
```

4. Inisialisasi Prisma dengan SQLite:

```bash
npx prisma init --datasource-provider sqlite
```

Perintah ini akan membuat:

- Folder `prisma/` berisi file `schema.prisma`
- File `.env` berisi connection string

Cek isi `.env`:

```
DATABASE_URL="file:./dev.db"
```

Artinya database SQLite akan disimpan sebagai file `dev.db` di folder `prisma/`.

---

## 5. Membuat Schema Prisma

Buka file `prisma/schema.prisma`. Kamu akan melihat:

```prisma
generator client {
  provider = "prisma-client-js"
}

datasource db {
  provider = "sqlite"
  url      = env("DATABASE_URL")
}
```

Sekarang kita tambahkan model untuk **Event** dan **Participant** (sesuai tema Event Registration):

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

Penjelasan:

- `@id` — primary key.
- `@default(autoincrement())` — ID otomatis bertambah.
- `String?` — field opsional (boleh kosong).
- `@default(now())` — otomatis terisi waktu saat ini.
- `Participant[]` dan `@relation(...)` — relasi **one-to-many**: satu Event bisa punya banyak Participant.

---

## 6. Menjalankan Migration

Migration adalah proses membuat/mengubah tabel di database berdasarkan schema yang sudah kita tulis.

Jalankan:

```bash
npx prisma migrate dev --name init
```

Prisma akan:

1. Membuat file migration di `prisma/migrations/`.
2. Membuat database `dev.db`.
3. Membuat tabel `Event` dan `Participant` di database.
4. Generate Prisma Client (kode yang kamu pakai untuk query).

Kalau berhasil, kamu akan melihat pesan:

```
Your database is now in sync with your schema.
✔ Generated Prisma Client
```

---

## 7. Prisma Studio — Lihat Database Lewat Browser

Prisma punya GUI bawaan untuk melihat dan mengedit data.

Jalankan:

```bash
npx prisma studio
```

Browser akan terbuka di `http://localhost:5555`. Kamu bisa:

- Melihat tabel `Event` dan `Participant`.
- Menambah data langsung dari sini.
- Mengedit dan menghapus data.

Coba tambahkan satu Event lewat Prisma Studio untuk latihan. Klik tabel `Event` → `Add record` → isi data → `Save`.

---

## 8. Operasi CRUD dengan Prisma Client

Sekarang kita coba akses database lewat kode JavaScript.

Buat file `seed.js`:

```bash
touch seed.js
```

Isi dengan:

```js
// seed.js
const { PrismaClient } = require("@prisma/client");
const prisma = new PrismaClient();

async function main() {
  // CREATE — Buat event baru
  const event = await prisma.event.create({
    data: {
      title: "GDGoC Web Dev Workshop",
      description: "Workshop web development untuk pemula",
      date: new Date("2026-07-15T09:00:00"),
      location: "ITS Surabaya"
    }
  });
  console.log("Event dibuat:", event);

  // CREATE — Tambah participant ke event
  const participant = await prisma.participant.create({
    data: {
      name: "Budi Santoso",
      email: "budi@example.com",
      eventId: event.id
    }
  });
  console.log("Participant ditambahkan:", participant);

  // READ — Ambil semua event beserta participants
  const events = await prisma.event.findMany({
    include: { participants: true }
  });
  console.log("Semua event:", JSON.stringify(events, null, 2));

  // UPDATE — Ubah lokasi event
  const updated = await prisma.event.update({
    where: { id: event.id },
    data: { location: "Gedung Robotika ITS" }
  });
  console.log("Event diupdate:", updated);

  // DELETE — Hapus participant
  const deleted = await prisma.participant.delete({
    where: { id: participant.id }
  });
  console.log("Participant dihapus:", deleted);
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

Jalankan:

```bash
node seed.js
```

Kamu akan melihat output setiap operasi CRUD di terminal. Cek juga hasilnya lewat Prisma Studio (`npx prisma studio`).

---

## 9. Cheat Sheet Prisma Client

Berikut operasi-operasi yang paling sering dipakai:

| Operasi | Kode |
|---------|------|
| Buat satu | `prisma.event.create({ data: { ... } })` |
| Ambil semua | `prisma.event.findMany()` |
| Ambil satu (by ID) | `prisma.event.findUnique({ where: { id: 1 } })` |
| Ambil dengan relasi | `prisma.event.findMany({ include: { participants: true } })` |
| Update | `prisma.event.update({ where: { id: 1 }, data: { ... } })` |
| Hapus | `prisma.event.delete({ where: { id: 1 } })` |
| Filter | `prisma.event.findMany({ where: { location: "ITS" } })` |

---

## 10. Struktur Folder Akhir

Setelah menyelesaikan modul ini, folder project kamu akan terlihat seperti ini:

```
belajar-prisma/
├── node_modules/
├── prisma/
│   ├── migrations/
│   │   └── 20260715_init/
│   │       └── migration.sql
│   ├── dev.db
│   └── schema.prisma
├── .env
├── package.json
├── package-lock.json
└── seed.js
```

---

## 11. Ringkasan Modul 4.1

Setelah menyelesaikan modul ini, kamu diharapkan:

- Paham kenapa data perlu disimpan di database (bukan di array).
- Mengerti perbedaan SQL vs NoSQL secara garis besar.
- Bisa setup Prisma dengan SQLite di project Node.js.
- Bisa membuat schema dengan model dan relasi.
- Bisa menjalankan migration untuk membuat tabel.
- Bisa melakukan operasi CRUD lewat Prisma Client.
- Bisa menggunakan Prisma Studio untuk melihat data.

Pada **Modul 4.2**, kita akan:

- Mengintegrasikan Prisma ke REST API Express dari Modul 3.3.
- Mengganti data in-memory (array) menjadi data dari database.
- Membangun API Event Registration yang datanya **persisten**.
