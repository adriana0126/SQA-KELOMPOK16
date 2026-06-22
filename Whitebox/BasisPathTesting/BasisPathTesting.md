# Basis Path Testing Login

## Pendahuluan

Basis Path Testing merupakan teknik White Box Testing yang digunakan untuk menguji seluruh jalur independen yang diperoleh dari hasil perhitungan Cyclomatic Complexity. Pengujian ini bertujuan untuk memastikan bahwa setiap kemungkinan jalur eksekusi program dapat berjalan sesuai dengan yang diharapkan.

Berdasarkan hasil Cyclomatic Complexity diperoleh empat jalur independen yang harus diuji.

## Jalur Pengujian

### Path 1 - Input Tidak Valid

Jalur:

```text
1 → 2 → 3 → 4 → 10
```

Skenario:

Pengguna memasukkan karakter yang tidak valid atau berpotensi menyebabkan gangguan keamanan sistem.

Expected Result:

Sistem menolak input dan menampilkan pesan kesalahan.

Status:

PASS

---

### Path 2 - Login Gagal

Jalur:

```text
1 → 2 → 3 → 5 → 6 → 9 → 10
```

Skenario:

Pengguna memasukkan username atau password yang tidak terdaftar pada database.

Expected Result:

Sistem menampilkan informasi bahwa login gagal.

Status:

PASS

---

### Path 3 - Login Sebagai Administrator

Jalur:

```text
1 → 2 → 3 → 5 → 6 → 7 → 8 → 10
```

Skenario:

Pengguna memasukkan username dan password yang valid dengan hak akses administrator.

Expected Result:

Sistem mengarahkan pengguna ke halaman admin.

Status:

PASS

---

### Path 4 - Login Sebagai Pengguna

Jalur:

```text
1 → 2 → 3 → 5 → 6 → 7 → 11 → 10
```

Skenario:

Pengguna memasukkan username dan password yang valid dengan hak akses pengguna biasa.

Expected Result:

Sistem mengarahkan pengguna ke halaman dashboard pengguna.

Status:

PASS

---

## Ringkasan Hasil Pengujian

| Path | Jalur Pengujian | Hasil Yang Diharapkan | Status |
|--------|----------------|----------------------|---------|
| P1 | 1-2-3-4-10 | Input ditolak | PASS |
| P2 | 1-2-3-5-6-9-10 | Login gagal | PASS |
| P3 | 1-2-3-5-6-7-8-10 | Masuk halaman admin | PASS |
| P4 | 1-2-3-5-6-7-11-10 | Masuk dashboard user | PASS |

## Kesimpulan

Seluruh jalur independen yang diperoleh dari hasil Cyclomatic Complexity telah berhasil diuji dan menghasilkan status PASS. Berdasarkan hasil pengujian tersebut dapat disimpulkan bahwa logika program pada modul login Sistem Informasi Perpustakaan berjalan sesuai dengan kebutuhan sistem dan tidak ditemukan kesalahan pada jalur eksekusi yang diuji.
