# Rekap E-GOTO — Firebase Firestore

Website rekap bulanan anggota E-GOTO yang di-host gratis melalui GitHub Pages dan disinkronkan realtime menggunakan Firebase Firestore.

## Anggota
- Ernest
- Arief
- Dilla
- Fauzan
- Fikri

## Fitur
- Tabel berbeda untuk setiap anggota
- Pilihan bulan
- Nomor otomatis
- Status: Belum, Proses, Tertunda, Selesai
- Tambah / hapus baris
- Sinkron realtime antar HP/laptop
- Firebase Authentication
- Export PDF
- Responsive mobile, tablet, laptop, desktop
- Warna identitas berbeda untuk setiap anggota

## Firebase yang digunakan
Project Firebase sudah dikonfigurasi di `firebase-config.js`.

Akses aplikasi dibatasi ke satu akun tim Firebase Authentication:

`egotosecond@gmail.com`

Password **tidak disimpan di repository**. Masukkan password hanya pada halaman login aplikasi.

## 1. Aktifkan Firebase Authentication
1. Buka Firebase Console.
2. Masuk ke project `rekap-e-goto`.
3. Build -> Authentication -> Get started.
4. Sign-in method -> aktifkan **Email/Password**.
5. Authentication -> Users -> Add user.
6. Buat user dengan email `egotosecond@gmail.com` dan password khusus aplikasi.

## 2. Buat Firestore Database
1. Firebase Console -> Build -> Firestore Database.
2. Klik **Create database**.
3. Pilih lokasi yang sesuai.
4. Setelah database aktif, buka tab **Rules**.
5. Salin isi file `firestore.rules` dari repository.
6. Klik **Publish**.

Rules hanya mengizinkan akun Firebase Authentication `egotosecond@gmail.com` untuk membaca dan menulis collection `rekap`.

Jangan gunakan rule publik seperti:

```text
allow read, write: if true;
```

## 3. Authorized Domain
Firebase Console -> Authentication -> Settings -> Authorized domains.

Pastikan domain berikut tersedia:

`fikrialv.github.io`

## 4. GitHub Pages
Repository:

`Fikrialv/Rekap-e-goto`

Buka:

Settings -> Pages -> Build and deployment -> Deploy from a branch

Pilih:
- Branch: `main`
- Folder: `/(root)`

Kemudian klik **Save**.

Alamat website:

`https://fikrialv.github.io/Rekap-e-goto/`

## Struktur Firestore

Collection:

`rekap`

Document ID menggunakan format:

`YYYY-MM__anggota`

Contoh:
- `2026-09__ernest`
- `2026-09__arief`
- `2026-09__dilla`
- `2026-09__fauzan`
- `2026-09__fikri`

Contoh isi dokumen:

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

Website memasang listener realtime pada dokumen bulan aktif sehingga perubahan dari satu perangkat dapat muncul pada perangkat lain yang sedang membuka rekap bulan yang sama.

## Keamanan
- Jangan commit password Firebase Authentication ke GitHub.
- Jangan menaruh service account/private key di frontend.
- Firebase Web config di `firebase-config.js` memang digunakan oleh browser; akses database tetap dibatasi oleh Authentication + Firestore Rules.
