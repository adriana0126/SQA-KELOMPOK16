# White Box Testing - Modul Login (login.php)

## Software Quality Assurance (SQA)

### Kelompok 16

## Deskripsi Modul

Modul yang diuji pada White Box Testing ini adalah modul autentikasi login (`login.php`). Modul ini berfungsi untuk memverifikasi identitas pengguna yang melakukan login ke sistem berbasis web menggunakan PHP dan MySQL.

Alur kerja modul meliputi:

1. Menerima input username dan password dari form login.
2. Melakukan pengecekan data ke database.
3. Membuat session apabila data valid.
4. Mengarahkan pengguna ke halaman sesuai role.
5. Menampilkan pesan gagal apabila data tidak ditemukan.

---

## Flow Graph

### Node

| Node | Keterangan                          |
| ---- | ----------------------------------- |
| 1    | Mulai Program                       |
| 2    | Membaca Input Username dan Password |
| 3    | Query Database                      |
| 4    | Kondisi Login Berhasil              |
| 5    | Menyimpan Data Session              |
| 6    | Kondisi Role Admin                  |
| 7    | Redirect ke admin.php               |
| 8    | Redirect ke dashboard.php           |
| 9    | Login Gagal dan Redirect            |
| 10   | Selesai                             |

### Edge

1 → 2

2 → 3

3 → 4

4 → 5

4 → 9

5 → 6

6 → 7

6 → 8

7 → 10

8 → 10

9 → 10

Jumlah Node = 10

Jumlah Edge = 11

---

## Cyclomatic Complexity

Menggunakan rumus:

V(G) = E - N + 2P

Keterangan:

* E = 11 (Edge)
* N = 10 (Node)
* P = 1 (Connected Component)

Perhitungan:

V(G) = 11 - 10 + 2(1)

V(G) = 3

### Hasil

Cyclomatic Complexity = **3**

Kategori: **Low Complexity**

---

## Independent Path

### Path 1 - Login Berhasil Sebagai Admin

1 → 2 → 3 → 4 → 5 → 6 → 7 → 10

Kondisi:

* Username dan password valid.
* Role pengguna adalah admin.

Output:

* Session tersimpan.
* Redirect ke `admin.php`.

### Path 2 - Login Berhasil Sebagai User

1 → 2 → 3 → 4 → 5 → 6 → 8 → 10

Kondisi:

* Username dan password valid.
* Role bukan admin.

Output:

* Session tersimpan.
* Redirect ke `dashboard.php`.

### Path 3 - Login Gagal

1 → 2 → 3 → 4 → 9 → 10

Kondisi:

* Username atau password tidak valid.

Output:

* Menampilkan pesan "Login gagal".
* Redirect ke `index.php`.

---

## Test Case White Box

| TC-ID | Path   | Input                 | Expected Output           | Status |
| ----- | ------ | --------------------- | ------------------------- | ------ |
| TC-01 | Path 1 | admin / admin123      | Redirect ke admin.php     | PASS   |
| TC-02 | Path 2 | user01 / user123      | Redirect ke dashboard.php | PASS   |
| TC-03 | Path 3 | wronguser / wrongpass | Alert Login Gagal         | PASS   |
| TC-04 | Path 3 | admin / salahpass     | Alert Login Gagal         | PASS   |
| TC-05 | Path 3 | kosong / kosong       | Alert Login Gagal         | PASS   |

---

## Hasil Pengujian

### Ringkasan

* Jumlah Test Case : 5
* Test Case PASS : 5
* Test Case FAIL : 0
* Persentase Keberhasilan : 100%
* Path Coverage : 3/3 (100%)
* Statement Coverage : 100%
* Branch Coverage : 100%

---

## Temuan Keamanan

Selama proses analisis ditemukan beberapa potensi kerentanan:

### SQL Injection

Query masih menggunakan input pengguna secara langsung tanpa prepared statement sehingga berpotensi dimanipulasi.

### Password Plaintext

Password masih disimpan dalam bentuk teks biasa (plaintext) sehingga berisiko apabila database bocor.

### Brute Force Attack

Belum terdapat mekanisme pembatasan percobaan login (rate limiting).

---

## Rekomendasi

1. Menggunakan Prepared Statement (PDO atau MySQLi Prepare).
2. Menggunakan `password_hash()` dan `password_verify()`.
3. Menambahkan CAPTCHA atau Rate Limiting.
4. Melakukan validasi dan sanitasi input pengguna.

---

## Kesimpulan

Berdasarkan hasil White Box Testing pada modul `login.php`, seluruh jalur independen berhasil diuji dengan tingkat keberhasilan 100%. Nilai Cyclomatic Complexity sebesar 3 menunjukkan bahwa modul memiliki kompleksitas rendah dan mudah dipelihara. Meskipun fungsi login berjalan dengan baik, ditemukan beberapa kerentanan keamanan seperti SQL Injection, penyimpanan password plaintext, dan tidak adanya mekanisme pencegahan brute force yang perlu diperbaiki sebelum sistem digunakan pada lingkungan produksi.
