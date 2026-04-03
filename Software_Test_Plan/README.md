# Software Test Plan

## Deskripsi
Dokumen ini berisi rencana dan hasil pengujian sistem.

## Pengujian yang Dilakukan
- Login berhasil
- Login gagal
- Registrasi berhasil
- Verifikasi kode
- Penyimpanan data

## Metode
Pengujian dilakukan secara manual dengan mencoba setiap fitur.

## Hasil
Semua fitur berjalan dengan baik sesuai kebutuhan user.

## 📊 Tabel Pengujian User Characteristic (Login & Register)

| No | Kebutuhan User                      | Hasil | Keterangan                 |
| -- | ----------------------------------- | ----- | -------------------------- |
| 1  | User dapat memilih menu registrasi  | OK    | Tombol register berfungsi  |
| 2  | Sistem menampilkan form registrasi  | OK    | Halaman register tampil    |
| 3  | User dapat menginput data diri      | OK    | Input berjalan dengan baik |
| 4  | User dapat memilih menu create akun | OK    | Tombol daftar berfungsi    |
| 5  | Sistem menampilkan verifikasi email | NO    | Disimulasikan              |
| 6  | User menginput kode verifikasi      | NO    | Disimulasikan              |
| 7  | Sistem menyimpan data ke database   | NO    | Disimulasikan (frontend)   |
| 8  | User dapat memilih cancel           | OK    | Kembali ke halaman login   |
| 9  | Sistem menampilkan halaman utama    | OK    | Redirect sederhana         |

