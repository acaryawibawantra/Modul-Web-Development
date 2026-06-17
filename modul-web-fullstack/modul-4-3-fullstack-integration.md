# Modul 4.3 – Full-Stack Integration (Next.js + Express API)

Di modul ini kamu akan **menghubungkan frontend Next.js dengan backend Express API** yang sudah dibuat di Modul 4.2.

Fokusnya:

- Membuat project Next.js baru dengan Tailwind CSS.
- Fetch data event dari API dan tampilkan di halaman.
- Membuat form registrasi yang POST data ke API.
- Menangani loading state dan error di frontend.

Target akhirnya: kamu punya **aplikasi full-stack Event Registration** — frontend Next.js yang berkomunikasi dengan backend Express + database.

---

## 1. Arsitektur Full-Stack

Sebelum mulai, pahami bagaimana kedua bagian bekerja bersama:

```
┌─────────────────────┐         ┌─────────────────────┐
│     FRONTEND        │  HTTP   │      BACKEND        │
│     (Next.js)       │ ──────> │    (Express API)    │
│                     │ <────── │                     │
│  localhost:3001     │  JSON   │  localhost:3000      │
│                     │         │        │             │
│  - Halaman event    │         │        ▼             │
│  - Form registrasi  │         │  ┌──────────┐       │
│  - Daftar peserta   │         │  │  SQLite   │       │
└─────────────────────┘         │  │  Database │       │
                                │  └──────────┘       │
                                └─────────────────────┘
```

- **Frontend** (Next.js) berjalan di port 3001.
- **Backend** (Express) berjalan di port 3000.
- Frontend mengirim HTTP request ke backend, backend membalas dengan JSON.
- Keduanya berjalan **terpisah** — ini pola yang umum di industri.

---

## 2. Setup Project Next.js

Pastikan backend dari Modul 4.2 sudah berjalan di terminal terpisah:

```bash
# Terminal 1: jalankan backend
cd event-registration-api
node index.js
```

Sekarang buat project Next.js di terminal baru:

```bash
# Terminal 2: buat frontend
npx create-next-app@latest event-registration-frontend
```

Saat ditanya opsi, pilih:

```
✔ Would you like to use TypeScript? → No
✔ Would you like to use ESLint? → Yes
✔ Would you like to use Tailwind CSS? → Yes
✔ Would you like your code inside a `src/` directory? → No
✔ Would you like to use App Router? → Yes
✔ Would you like to use Turbopack? → Yes
✔ Would you like to customize the import alias? → No
```

Masuk ke folder project:

```bash
cd event-registration-frontend
```

Ubah port supaya tidak bentrok dengan backend. Edit `package.json`:

```json
{
  "scripts": {
    "dev": "next dev -p 3001"
  }
}
```

Jalankan:

```bash
npm run dev
```

Buka `http://localhost:3001` — halaman default Next.js muncul.

---

## 3. Halaman Utama: Daftar Event

Ganti isi `app/page.js` dengan:

```javascript
// app/page.js
"use client";

import { useState, useEffect } from "react";
import Link from "next/link";

export default function Home() {
  const [events, setEvents] = useState([]);
  const [loading, setLoading] = useState(true);
  const [error, setError] = useState(null);

  useEffect(() => {
    fetch("http://localhost:3000/api/events")
      .then((res) => {
        if (!res.ok) throw new Error("Gagal mengambil data events");
        return res.json();
      })
      .then((data) => {
        setEvents(data);
        setLoading(false);
      })
      .catch((err) => {
        setError(err.message);
        setLoading(false);
      });
  }, []);

  if (loading) {
    return (
      <div className="min-h-screen flex items-center justify-center">
        <p className="text-lg text-gray-500">Memuat data events...</p>
      </div>
    );
  }

  if (error) {
    return (
      <div className="min-h-screen flex items-center justify-center">
        <div className="text-center">
          <p className="text-lg text-red-500">{error}</p>
          <p className="text-sm text-gray-400 mt-2">
            Pastikan backend berjalan di http://localhost:3000
          </p>
        </div>
      </div>
    );
  }

  return (
    <div className="min-h-screen bg-gray-50 py-12 px-4">
      <div className="max-w-3xl mx-auto">
        <h1 className="text-3xl font-bold text-gray-900 mb-8">
          Event Registration
        </h1>

        {events.length === 0 ? (
          <p className="text-gray-500">Belum ada event.</p>
        ) : (
          <div className="space-y-4">
            {events.map((event) => (
              <div
                key={event.id}
                className="bg-white rounded-lg shadow p-6 border border-gray-200"
              >
                <h2 className="text-xl font-semibold text-gray-800">
                  {event.title}
                </h2>
                {event.description && (
                  <p className="text-gray-600 mt-1">{event.description}</p>
                )}
                <div className="flex gap-4 mt-3 text-sm text-gray-500">
                  <span>
                    {new Date(event.date).toLocaleDateString("id-ID", {
                      weekday: "long",
                      year: "numeric",
                      month: "long",
                      day: "numeric"
                    })}
                  </span>
                  <span>{event.location}</span>
                </div>
                <div className="flex items-center justify-between mt-4">
                  <span className="text-sm text-gray-400">
                    {event.participants.length} peserta terdaftar
                  </span>
                  <Link
                    href={`/events/${event.id}`}
                    className="text-sm font-medium text-blue-600 hover:text-blue-800"
                  >
                    Lihat Detail & Daftar →
                  </Link>
                </div>
              </div>
            ))}
          </div>
        )}
      </div>
    </div>
  );
}
```

Buka `http://localhost:3001` — kamu akan melihat... **error CORS!** Ini normal. Lanjut ke langkah berikutnya.

---

## 4. Mengatasi CORS di Backend

Browser memblokir request dari `localhost:3001` (frontend) ke `localhost:3000` (backend) karena **CORS (Cross-Origin Resource Sharing)**.

Kalau kamu mengikuti Modul 4.2, CORS sudah diinstall dan diaktifkan di `index.js` backend. Pastikan di project backend (`event-registration-api`) sudah ada:

```javascript
const cors = require("cors");
app.use(cors());
```

Kalau belum, kembali ke project backend dan jalankan:

```bash
npm install cors
```

Tambahkan dua baris di atas ke `index.js`, lalu restart backend. Sekarang refresh `http://localhost:3001` — daftar event akan muncul.

---

## 5. Halaman Detail Event + Form Registrasi

Buat folder dan file untuk halaman detail:

```bash
mkdir -p app/events/[id]
```

Buat `app/events/[id]/page.js`:

```javascript
// app/events/[id]/page.js
"use client";

import { useState, useEffect } from "react";
import { useParams } from "next/navigation";
import Link from "next/link";

export default function EventDetail() {
  const params = useParams();
  const [event, setEvent] = useState(null);
  const [loading, setLoading] = useState(true);
  const [error, setError] = useState(null);

  // Form state
  const [name, setName] = useState("");
  const [email, setEmail] = useState("");
  const [submitting, setSubmitting] = useState(false);
  const [submitMessage, setSubmitMessage] = useState(null);

  // Fetch event data
  function fetchEvent() {
    fetch(`http://localhost:3000/api/events/${params.id}`)
      .then((res) => {
        if (!res.ok) throw new Error("Event tidak ditemukan");
        return res.json();
      })
      .then((data) => {
        setEvent(data);
        setLoading(false);
      })
      .catch((err) => {
        setError(err.message);
        setLoading(false);
      });
  }

  useEffect(() => {
    fetchEvent();
  }, [params.id]);

  // Handle form submit
  async function handleSubmit(e) {
    e.preventDefault();
    setSubmitting(true);
    setSubmitMessage(null);

    try {
      const res = await fetch("http://localhost:3000/api/participants", {
        method: "POST",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify({
          name,
          email,
          eventId: Number(params.id)
        })
      });

      const data = await res.json();

      if (!res.ok) {
        setSubmitMessage({ type: "error", text: data.error });
      } else {
        setSubmitMessage({ type: "success", text: "Registrasi berhasil!" });
        setName("");
        setEmail("");
        // Refresh data event untuk update daftar peserta
        fetchEvent();
      }
    } catch (err) {
      setSubmitMessage({ type: "error", text: "Gagal mengirim data" });
    }

    setSubmitting(false);
  }

  if (loading) {
    return (
      <div className="min-h-screen flex items-center justify-center">
        <p className="text-lg text-gray-500">Memuat data event...</p>
      </div>
    );
  }

  if (error) {
    return (
      <div className="min-h-screen flex items-center justify-center">
        <p className="text-lg text-red-500">{error}</p>
      </div>
    );
  }

  return (
    <div className="min-h-screen bg-gray-50 py-12 px-4">
      <div className="max-w-3xl mx-auto">
        <Link
          href="/"
          className="text-sm text-blue-600 hover:text-blue-800 mb-6 inline-block"
        >
          ← Kembali ke daftar event
        </Link>

        {/* Detail Event */}
        <div className="bg-white rounded-lg shadow p-6 border border-gray-200">
          <h1 className="text-2xl font-bold text-gray-900">{event.title}</h1>
          {event.description && (
            <p className="text-gray-600 mt-2">{event.description}</p>
          )}
          <div className="flex gap-4 mt-3 text-sm text-gray-500">
            <span>
              {new Date(event.date).toLocaleDateString("id-ID", {
                weekday: "long",
                year: "numeric",
                month: "long",
                day: "numeric"
              })}
            </span>
            <span>{event.location}</span>
          </div>
        </div>

        {/* Form Registrasi */}
        <div className="bg-white rounded-lg shadow p-6 border border-gray-200 mt-6">
          <h2 className="text-lg font-semibold text-gray-800 mb-4">
            Daftar sebagai Peserta
          </h2>

          <form onSubmit={handleSubmit} className="space-y-4">
            <div>
              <label className="block text-sm font-medium text-gray-700 mb-1">
                Nama Lengkap
              </label>
              <input
                type="text"
                value={name}
                onChange={(e) => setName(e.target.value)}
                required
                className="w-full px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-blue-500 text-gray-900"
                placeholder="Masukkan nama lengkap"
              />
            </div>
            <div>
              <label className="block text-sm font-medium text-gray-700 mb-1">
                Email
              </label>
              <input
                type="email"
                value={email}
                onChange={(e) => setEmail(e.target.value)}
                required
                className="w-full px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-blue-500 text-gray-900"
                placeholder="Masukkan email"
              />
            </div>
            <button
              type="submit"
              disabled={submitting}
              className="w-full bg-blue-600 text-white py-2 px-4 rounded-md hover:bg-blue-700 disabled:bg-blue-300 font-medium"
            >
              {submitting ? "Mendaftarkan..." : "Daftar Sekarang"}
            </button>
          </form>

          {submitMessage && (
            <div
              className={`mt-4 p-3 rounded-md text-sm ${
                submitMessage.type === "success"
                  ? "bg-green-50 text-green-700 border border-green-200"
                  : "bg-red-50 text-red-700 border border-red-200"
              }`}
            >
              {submitMessage.text}
            </div>
          )}
        </div>

        {/* Daftar Peserta */}
        <div className="bg-white rounded-lg shadow p-6 border border-gray-200 mt-6">
          <h2 className="text-lg font-semibold text-gray-800 mb-4">
            Peserta Terdaftar ({event.participants.length})
          </h2>

          {event.participants.length === 0 ? (
            <p className="text-gray-500 text-sm">
              Belum ada peserta. Jadilah yang pertama!
            </p>
          ) : (
            <ul className="divide-y divide-gray-100">
              {event.participants.map((p) => (
                <li key={p.id} className="py-3 flex justify-between">
                  <div>
                    <p className="text-sm font-medium text-gray-800">
                      {p.name}
                    </p>
                    <p className="text-xs text-gray-400">{p.email}</p>
                  </div>
                  <span className="text-xs text-gray-400">
                    {new Date(p.createdAt).toLocaleDateString("id-ID")}
                  </span>
                </li>
              ))}
            </ul>
          )}
        </div>
      </div>
    </div>
  );
}
```

---

## 6. Mencoba Aplikasi Full-Stack

Pastikan kedua server berjalan:

```bash
# Terminal 1: Backend
cd event-registration-api
node index.js

# Terminal 2: Frontend
cd event-registration-frontend
npm run dev
```

Sekarang buka `http://localhost:3001` dan coba:

1. **Lihat daftar event** — data diambil dari API → database.
2. **Klik "Lihat Detail & Daftar"** — masuk ke halaman detail event.
3. **Isi form dan klik "Daftar Sekarang"** — data dikirim ke API → disimpan di database.
4. **Daftar peserta langsung terupdate** — tanpa perlu refresh manual.
5. **Coba daftar dengan email yang sama** — muncul pesan error "Email sudah terdaftar di event ini".
6. **Restart backend** (`Ctrl+C` lalu `node index.js`) → refresh frontend → **data tetap ada**.

---

## 7. Alur Data yang Terjadi

Saat user membuka halaman utama:

```
Browser (localhost:3001)
  → Next.js render page
  → useEffect: fetch("http://localhost:3000/api/events")
  → Express menerima GET /api/events
  → Prisma: prisma.event.findMany({ include: { participants: true } })
  → SQLite mengembalikan data
  → Express kirim JSON response
  → React setState → UI terupdate
```

Saat user submit form registrasi:

```
Browser: user klik "Daftar Sekarang"
  → handleSubmit: fetch POST /api/participants
  → Express menerima POST
  → Prisma: prisma.participant.create({ data: { ... } })
  → Data tersimpan di SQLite
  → Express kirim 201 Created
  → React: tampilkan "Registrasi berhasil!"
  → fetchEvent() dipanggil ulang → daftar peserta terupdate
```

---

## 8. Struktur Folder Akhir

```
event-registration-api/           ← Backend (Modul 4.2)
├── prisma/
│   ├── migrations/
│   ├── dev.db
│   └── schema.prisma
├── routes/
│   ├── events.js
│   └── participants.js
├── index.js
├── seed.js
├── package.json
└── .env

event-registration-frontend/      ← Frontend (Modul 4.3)
├── app/
│   ├── events/
│   │   └── [id]/
│   │       └── page.js
│   ├── layout.js
│   ├── page.js
│   └── globals.css
├── package.json
└── ...
```

---

## 9. Ringkasan Modul 4.3

Setelah menyelesaikan modul ini, kamu diharapkan:

- Bisa membuat project Next.js dan menghubungkannya ke backend API.
- Paham cara `fetch` data dari API di React (`useEffect` + `useState`).
- Bisa mengirim data dari form ke API menggunakan `POST`.
- Paham konsep CORS dan cara mengatasinya.
- Bisa menangani loading state, error state, dan success feedback.
- Memiliki **aplikasi full-stack** yang berjalan: frontend + backend + database.

Selamat! Dari Modul 1 sampai Modul 4, kamu sudah membangun:

| Modul | Output |
| --- | --- |
| Modul 1 | Halaman web statis (HTML + CSS + JS) |
| Modul 2 | Aplikasi React/Next.js dengan Tailwind |
| Modul 3 | REST API Express dengan data in-memory |
| Modul 4 | Full-stack app: Next.js + Express + SQLite |

Di **Modul 5**, kamu akan belajar:

- Menambahkan **authentication** (login/register).
- Mempersiapkan project untuk **production**.
- **Deploy** aplikasi ke internet agar bisa diakses siapa saja.
