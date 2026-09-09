# Rekap E-GOTO — Firebase Firestore

Rekap bulanan anggota E-GOTO yang di-host gratis di GitHub Pages dan disinkronkan realtime melalui Firebase Firestore.

## Fitur
- Ernest, Arief, Dilla, Fauzan, Fikri
- Tabel berbeda untuk setiap anggota
- Pilihan bulan
- Nomor otomatis
- Status: Belum, Proses, Tertunda, Selesai
- Tambah / hapus baris
- Sinkron realtime antar HP/laptop
- Login Firebase Authentication
- Export PDF
- Responsive mobile, tablet, laptop, desktop

## 1. Buat Firebase Project
1. Buka Firebase Console.
2. Buat project baru.
3. Tambahkan **Web App**.
4. Salin `firebaseConfig`.
5. Edit `firebase-config.js` dan ganti seluruh nilai `GANTI_...`.

## 2. Aktifkan Firestore
1. Firebase Console -> Build -> Firestore Database.
2. Create database.
3. Pilih lokasi yang paling dekat / sesuai kebutuhan.
4. Setelah database jadi, buka tab **Rules**.
5. Salin isi `firestore.rules`.
6. Ganti lima email contoh dengan email asli anggota tim.
7. Publish rules.

Jangan gunakan rule `allow read, write: if true` pada website publik.

## 3. Aktifkan Login
1. Firebase Console -> Build -> Authentication.
2. Klik **Get started**.
3. Sign-in method -> aktifkan **Email/Password**.
4. Authentication -> Users -> buat 5 user tim secara manual.
5. Gunakan email yang sama dengan yang dimasukkan ke `firestore.rules`.

Website ini tidak menyediakan registrasi user publik.

## 4. Authorized Domain
Di Authentication -> Settings -> Authorized domains, tambahkan:

`fikrialv.github.io`

## 5. GitHub Pages
Settings -> Pages -> Deploy from a branch -> `main` -> `/(root)`.

URL:
`https://fikrialv.github.io/Rekap-e-goto/`

## Struktur Firestore

Collection: `rekap`

Document ID:
`YYYY-MM__anggota`

Contoh:
- `2026-09__ernest`
- `2026-09__arief`
- `2026-09__dilla`

Isi dokumen:
```json
{
  "member": "Ernest",
  "month": "2026-09",
  "rows": [
    {
      "kegiatan": "Desain konten",
      "status": "Proses",
      "catatan": "Revisi"
    }
  ]
}
```

Listener realtime dipasang langsung pada lima dokumen bulan aktif, sehingga tidak membutuhkan query kompleks atau composite index.
