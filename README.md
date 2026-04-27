# 📚 Sistem Perpustakaan Berbasis Web

Project ini merupakan aplikasi perpustakaan berbasis web yang dibuat menggunakan PHP, MySQL, dan Bootstrap sebagai bagian dari tugas mata kuliah Software Quality. Sistem ini bertujuan untuk membantu proses pengelolaan peminjaman buku secara digital sehingga lebih efisien dibandingkan dengan sistem manual.

## 🎯 Deskripsi Sistem

Sistem perpustakaan ini memungkinkan pengguna untuk melakukan registrasi akun, login, meminjam buku, serta mengajukan pengembalian. Proses pengembalian tidak dilakukan secara langsung oleh user, melainkan harus melalui konfirmasi dari admin untuk mencegah manipulasi data. Sistem ini juga dilengkapi dengan fitur verifikasi email untuk memastikan validitas pengguna.

## 🚀 Fitur Utama

Sistem ini memiliki beberapa fitur utama, antara lain:
- Login & Register
- Verifikasi Email
- Dashboard User
- Peminjaman Buku
- Pengembalian Buku (Request → Admin)
- Riwayat Peminjaman
- Admin Panel
- Search & Pagination
- Lihat password

## 👥 Role User

Dalam sistem ini terdapat dua jenis pengguna, yaitu:

User:
- Melakukan registrasi dan login
- Meminjam buku
- Mengajukan pengembalian
- Melihat riwayat peminjaman

Admin:
- Melihat seluruh data peminjaman
- Mengkonfirmasi pengembalian buku
- Monitoring sistem

## 🗄️ Database

Sistem menggunakan database MySQL dengan dua tabel utama, yaitu:
- users
- peminjaman

Relasi antara tabel:
- users.id → peminjaman.user_id

## 🔄 Alur Sistem

Alur sistem dimulai dari proses registrasi akun oleh user, kemudian dilakukan verifikasi email. Setelah itu user dapat login ke dalam sistem dan melakukan peminjaman buku. Jika user ingin mengembalikan buku, maka user harus mengajukan permintaan pengembalian terlebih dahulu. Admin kemudian akan melakukan konfirmasi pengembalian tersebut. Sistem juga dapat menghitung denda apabila terjadi keterlambatan pengembalian.

## 🧪 Pengujian Sistem

Pengujian dilakukan terhadap seluruh fitur utama seperti login, register, verifikasi email, peminjaman buku, pengembalian buku, admin panel, search, pagination, dan show password. Berdasarkan hasil pengujian, seluruh fitur berjalan dengan baik sesuai dengan kebutuhan sistem.

## 🛠️ Teknologi yang Digunakan

- PHP Native
- MySQL Database
- Bootstrap 5
- XAMPP
## 📁 Struktur Repository

- Software_Design_Dokumen
- Software_Requirements_Specification
- Software_Test_Plan
- Software_User_Documentations

## ▶️ Cara Menjalankan Project

1. Install XAMPP
2. Simpan project ke folder htdocs
3. Import database ke phpMyAdmin
4. Jalankan project melalui browser:
   http://localhost/SQA-KELOMPOK16/perpustakaan

## 👥 Tim Penyusun 

1. Adriana Putra Pratama Kusunmah
2. Marwan Setyadi
3. Muhammad Teguh Pawana
4. Ryan Restu Julianto
