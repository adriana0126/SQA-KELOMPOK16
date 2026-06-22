# Flow Graph Login

## Pendahuluan

Flow Graph merupakan representasi grafis dari alur logika program yang digunakan untuk menggambarkan hubungan antar proses, keputusan, dan jalur eksekusi dalam sebuah modul. Pada pengujian ini, Flow Graph diterapkan pada modul Login Sistem Informasi Perpustakaan untuk mengidentifikasi seluruh kemungkinan jalur yang dapat dilalui selama proses autentikasi pengguna.

Modul login merupakan salah satu fitur utama dalam sistem karena berfungsi sebagai gerbang akses pengguna. Oleh karena itu, diperlukan analisis terhadap alur program untuk memastikan seluruh proses berjalan sesuai dengan kebutuhan sistem.

## Flow Graph

```text
(1) Start
   |
   v
(2) Input Username & Password
   |
   v
(3) Cek Karakter Berbahaya?
   |Yes
   v
(4) Input Tidak Valid
   |
   v
(10) End

   No
   |
   v
(5) Cek Database
   |
   v
(6) Data Ditemukan?
   |No
   v
(9) Login Gagal
   |
   v
(10) End

   Yes
   |
   v
(7) Role Admin?
   |Yes
   v
(8) Admin Panel
   |
   v
(10) End

   No
   |
   v
(11) Dashboard User
   |
   v
(10) End
```

## Penjelasan Alur

Proses dimulai ketika pengguna memasukkan username dan password pada halaman login. Sistem kemudian melakukan validasi terhadap data yang dimasukkan untuk memastikan tidak terdapat karakter yang berpotensi menimbulkan gangguan keamanan.

Apabila ditemukan input yang tidak valid, proses login akan dihentikan dan sistem menampilkan pesan kesalahan. Jika input valid, sistem akan melakukan pemeriksaan data pengguna pada database.

Selanjutnya sistem akan memeriksa apakah data pengguna ditemukan atau tidak. Jika data tidak ditemukan, maka proses login dinyatakan gagal. Namun apabila data ditemukan, sistem akan memeriksa hak akses pengguna.

Pengguna dengan role administrator akan diarahkan ke halaman admin, sedangkan pengguna biasa akan diarahkan ke halaman dashboard pengguna.

## Kesimpulan

Berdasarkan Flow Graph yang telah dibuat, diperoleh beberapa kemungkinan jalur eksekusi yang menjadi dasar dalam pelaksanaan White Box Testing. Seluruh jalur tersebut akan digunakan pada tahap Basis Path Testing untuk memastikan logika program berjalan dengan baik.
