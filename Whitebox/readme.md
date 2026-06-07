# 📋 White Box Testing — Aplikasi Perpustakaan Digital

> **Metode:** Basis Path Testing & Control Flow Analysis  
> **Teknik:** Cyclomatic Complexity, Flow Graph Analysis  
> **Total Test Case:** 20 | **Hasil:** 20 PASS ✅

---

## 📌 Daftar Isi

1. [Pendahuluan](#1-pendahuluan)
2. [Analisis Flow Graph Per Modul](#2-analisis-flow-graph-per-modul)
3. [Tabel Test Case](#3-tabel-test-case)
4. [Cyclomatic Complexity](#4-ringkasan-cyclomatic-complexity)
5. [Temuan & Rekomendasi](#5-temuan--rekomendasi)
6. [Kesimpulan](#6-kesimpulan)

---

## 1. Pendahuluan

**White Box Testing** adalah teknik pengujian perangkat lunak yang berfokus pada struktur internal kode program. Berbeda dengan Black Box Testing yang menguji dari sisi pengguna, White Box Testing memeriksa alur logika, kondisi percabangan (branch), dan jalur eksekusi (path) di dalam source code.

### Modul yang Diuji

| No | File | Fungsi |
|----|------|--------|
| 1 | `index.php` | Halaman login dengan toggle password |
| 2 | `koneksi.php` | Koneksi ke database MySQL |
| 3 | `dashboard.php` | Halaman utama user dan peminjaman buku |
| 4 | `admin.php` | Panel admin dengan search & pagination |
| 5 | `kembali.php` | Proses pengembalian buku dan kalkulasi denda |
| 6 | `kirim_email.php` | Pengiriman kode OTP via email (PHPMailer) |
| 7 | `logout.php` | Penghancuran sesi user |

### Tujuan Pengujian

- Memverifikasi seluruh jalur eksekusi (execution path) pada setiap modul
- Memastikan kondisi percabangan `if/else` ditangani dengan benar
- Mengidentifikasi potensi bug, SQL Injection, dan celah keamanan
- Menghitung Cyclomatic Complexity untuk mengukur kompleksitas kode

### Teknik yang Digunakan

- **Basis Path Testing** — menentukan jalur independen dari flow graph
- **Control Flow Analysis** — menganalisis struktur percabangan
- **Cyclomatic Complexity** — `V(G) = E - N + 2P`

---

## 2. Analisis Flow Graph Per Modul

### 2.1 `koneksi.php` — Koneksi Database

```
N1 → mysqli_connect(localhost, root, '', perpustakaan)
N2 → if (!$conn)
       ├── TRUE  → N3: die('Koneksi gagal')
       └── FALSE → N4: lanjut eksekusi
```

| Node | Pernyataan | Kondisi |
|------|-----------|---------|
| N1 | `mysqli_connect(...)` | — |
| N2 | `if (!$conn)` | Koneksi gagal → TRUE / berhasil → FALSE |
| N3 | `die('Koneksi gagal')` | Jalur gagal |
| N4 | Lanjut eksekusi | Jalur sukses |

> **Cyclomatic Complexity: V(G) = 2** (2 jalur: sukses dan gagal)

---

### 2.2 `index.php` — Halaman Login

```
N1 → Tampilkan form HTML
N2 → User klik tombol 👁️ (togglePassword())
N3 → if (pass.type === 'password')
       ├── TRUE  → ubah ke 'text', ikon 🙈
       └── FALSE → ubah ke 'password', ikon 👁️
N5 → Form submit ke proses_login.php (POST)
```

| Node | Pernyataan | Kondisi |
|------|-----------|---------|
| N1 | Tampilkan form HTML | — |
| N2 | User klik tombol toggle | Event onClick |
| N3 | `if (pass.type === 'password')` | TRUE: show / FALSE: hide |
| N4 | else | Ubah kembali ke password |
| N5 | Submit form ke `proses_login.php` | POST action |

> **Cyclomatic Complexity: V(G) = 2** (toggle show/hide password)

---

### 2.3 `dashboard.php` — Dashboard User

```
N1 → session_start()
N2 → if (!isset($_SESSION['user']))
       ├── TRUE  → redirect index.php
       └── FALSE → N3: tampilkan halaman
N4 → User klik Pinjam
N5 → if (window.sudahKlik)
       ├── TRUE  → return (abaikan klik ganda)
       └── FALSE → N6: fetch POST ke pinjam.php
N7 → alert berhasil + location.reload()
```

| Node | Pernyataan | Kondisi |
|------|-----------|---------|
| N1 | `session_start()` | — |
| N2 | `if (!isset($_SESSION['user']))` | TRUE → redirect |
| N3 | Tampilkan dashboard | Sesi valid |
| N4 | Klik tombol Pinjam | Event onClick |
| N5 | `if (window.sudahKlik) return` | TRUE → abaikan klik ganda |
| N6 | `fetch('pinjam.php', POST)` | Kirim request |
| N7 | Alert sukses + reload | After fetch resolve |

> **Cyclomatic Complexity: V(G) = 3** (sesi invalid, klik ganda, klik valid)

---

### 2.4 `admin.php` — Panel Admin

```
N1  → session_start() + include koneksi.php
N2  → if (!isset($_SESSION['user']) || role != 'admin')
        ├── TRUE  → redirect index.php
        └── FALSE → N3
N3  → Ambil $keyword dari GET['cari']
N4  → if ($keyword != '')
        ├── TRUE  → tambah WHERE LIKE ke query
        └── FALSE → N5: query tanpa filter
N6  → while (mysqli_fetch_assoc) — loop setiap baris
N7  → if ($d['status'] == 'dipinjam')  → badge warning
N8  → elseif ($d['status'] == 'menunggu') → badge info + form konfirmasi
N9  → else (dikembalikan) → badge success
N10 → for ($i=1; $i<=$total_page; $i++) — loop pagination
N11 → if ($i == $page) → active class
```

| Node | Pernyataan | Kondisi |
|------|-----------|---------|
| N1 | `session_start()` + include | — |
| N2 | Cek sesi & role admin | TRUE → redirect |
| N3 | Ambil `$keyword` dari GET | — |
| N4 | `if ($keyword != '')` | TRUE: tambah WHERE LIKE |
| N5 | Query tanpa WHERE | Tidak ada keyword |
| N6 | `while (mysqli_fetch_assoc)` | Iterasi data |
| N7 | `if (status == 'dipinjam')` | Badge warning kuning |
| N8 | `elseif (status == 'menunggu')` | Badge info + konfirmasi |
| N9 | `else` (dikembalikan) | Badge success hijau |
| N10 | `for ($i=1; ...)` | Loop halaman |
| N11 | `if ($i == $page)` | Active class |

> **Cyclomatic Complexity: V(G) = 7** (auth, search, loop data, 3 status, pagination)

---

### 2.5 `kembali.php` — Pengembalian & Kalkulasi Denda

```
N1 → Terima $_POST['id']
N2 → SELECT * FROM peminjaman WHERE id='$id'
N3 → Hitung $hari = (sekarang - tanggal_pinjam) / 86400
N4 → $denda = 0
N5 → if ($hari > 3)
       ├── TRUE  → $denda = ($hari - 3) * 1000
       └── FALSE → denda tetap 0
N6 → UPDATE status, tanggal_kembali, denda
N7 → redirect admin.php
```

| Node | Pernyataan | Kondisi |
|------|-----------|---------|
| N1 | Terima `$_POST['id']` | — |
| N2 | Query SELECT data peminjaman | — |
| N3 | Hitung selisih hari | — |
| N4 | `$denda = 0` | Inisialisasi |
| N5 | `if ($hari > 3)` | TRUE: kena denda Rp1.000/hari |
| N6 | UPDATE ke database | — |
| N7 | `header('Location: admin.php')` | Redirect |

> **Cyclomatic Complexity: V(G) = 2** (denda atau tidak)

---

### 2.6 `kirim_email.php` — Kirim Kode OTP

```
N1 → Terima POST: nama, email, username, password
N2 → $kode = rand(1000, 9999)
N3 → Simpan ke $_SESSION['user_temp']
N4 → new PHPMailer(true) + config SMTP Gmail
N5 → $mail->send()
       ├── TRUE  → N7: redirect verifikasi.php
       └── FALSE → N6: throw Exception
```

| Node | Pernyataan | Kondisi |
|------|-----------|---------|
| N1 | Terima data registrasi via POST | — |
| N2 | `rand(1000, 9999)` | Generate OTP |
| N3 | Simpan ke `$_SESSION['user_temp']` | — |
| N4 | Inisialisasi PHPMailer + SMTP config | — |
| N5 | `$mail->send()` | Kirim email |
| N6 | Exception handler | Jika SMTP gagal |
| N7 | Redirect ke `verifikasi.php` | Jika sukses |

> **Cyclomatic Complexity: V(G) = 2** (email berhasil / gagal exception)

---

### 2.7 `logout.php` — Hapus Sesi

```
N1 → session_start()
N2 → session_destroy()
N3 → header('Location: index.php')
```

| Node | Pernyataan | Kondisi |
|------|-----------|---------|
| N1 | `session_start()` | — |
| N2 | `session_destroy()` | Hapus semua sesi |
| N3 | Redirect ke `index.php` | — |

> **Cyclomatic Complexity: V(G) = 1** (jalur tunggal, tidak ada percabangan)

---

## 3. Tabel Test Case

| No | Fungsi / File | Jalur Eksekusi | Kondisi Input | Expected Output | Actual Output | Status |
|----|--------------|----------------|---------------|-----------------|---------------|--------|
| 1 | `koneksi.php` | N1→N2→N4 (sukses) | DB tersedia: localhost, root | `$conn` valid, eksekusi lanjut | Koneksi berhasil | ✅ PASS |
| 2 | `koneksi.php` | N1→N2→N3 (gagal) | DB tidak tersedia / password salah | `die('Koneksi gagal')` dipanggil | Eksekusi berhenti | ✅ PASS |
| 3 | `index.php` (toggle) | N2→N3 TRUE (show) | `pass.type = 'password'`, klik toggle | Type berubah ke `text`, ikon 🙈 | Password terlihat | ✅ PASS |
| 4 | `index.php` (toggle) | N2→N4 FALSE (hide) | `pass.type = 'text'`, klik toggle | Type berubah ke `password`, ikon 👁️ | Password tersembunyi | ✅ PASS |
| 5 | `dashboard.php` | N1→N2→redirect | `$_SESSION['user']` tidak ada | Redirect ke `index.php` | Redirect berhasil | ✅ PASS |
| 6 | `dashboard.php` | N1→N2→N3 (valid) | `$_SESSION['user'] = 'budi'` | Halaman dashboard tampil | Dashboard muncul | ✅ PASS |
| 7 | `dashboard.php` (pinjam) | N4→N5 TRUE→return | `window.sudahKlik = true` | Fungsi return, fetch tidak dipanggil | Request tidak ganda | ✅ PASS |
| 8 | `dashboard.php` (pinjam) | N4→N5 FALSE→N6→N7 | `window.sudahKlik = false`, pilih buku | Fetch POST ke `pinjam.php`, alert sukses | Peminjaman tercatat | ✅ PASS |
| 9 | `admin.php` | N1→N2 TRUE→redirect | `role = 'user'` | Redirect ke `index.php` | Akses ditolak | ✅ PASS |
| 10 | `admin.php` | N1→N2 FALSE→N3 | `role = 'admin'` | Panel admin tampil | Data peminjaman muncul | ✅ PASS |
| 11 | `admin.php` (search) | N3→N4 TRUE | `$_GET['cari'] = 'Budi'` | WHERE LIKE `'%Budi%'` ditambahkan | Data terfilter | ✅ PASS |
| 12 | `admin.php` (search) | N3→N5 FALSE | `$_GET['cari'] = ''` | Semua data tampil tanpa filter | Semua data tampil | ✅ PASS |
| 13 | `admin.php` (status) | N7 TRUE | `status = 'dipinjam'` | Badge warning kuning | Badge tampil sesuai | ✅ PASS |
| 14 | `admin.php` (status) | N8 TRUE | `status = 'menunggu'` | Badge info biru + tombol Konfirmasi | Konfirmasi muncul | ✅ PASS |
| 15 | `admin.php` (status) | N9 (else) | `status = 'dikembalikan'` | Badge success hijau | Badge tampil sesuai | ✅ PASS |
| 16 | `kembali.php` | N1→N5 TRUE (denda) | Pinjam 7 hari lalu | denda = (7-3)×1000 = Rp 4.000 | Denda tersimpan, redirect | ✅ PASS |
| 17 | `kembali.php` | N1→N5 FALSE (tidak denda) | Pinjam 2 hari lalu | denda = 0, status dikembalikan | denda 0 tersimpan | ✅ PASS |
| 18 | `kembali.php` | N1→N5 FALSE (batas tepat) | Pinjam tepat 3 hari | denda = 0 (batas tidak dikenakan denda) | denda = 0 | ✅ PASS |
| 19 | `kirim_email.php` | N1→N7 (sukses) | Email valid, SMTP aktif | Email OTP terkirim, redirect `verifikasi.php` | Email diterima | ✅ PASS |
| 20 | `kirim_email.php` | N1→N6 (gagal) | SMTP mati / password salah | Exception PHPMailer terlempar | Error, tidak redirect | ✅ PASS |
| 21 | `logout.php` | N1→N2→N3 | Sesi aktif manapun | Sesi hancur, redirect `index.php` | Logout berhasil | ✅ PASS |

---

## 4. Ringkasan Cyclomatic Complexity

> **Rumus:** `V(G) = E - N + 2P`  
> E = jumlah edge, N = jumlah node, P = jumlah komponen terhubung (biasanya 1)

| Modul / File | Jumlah Node | V(G) | Interpretasi |
|-------------|-------------|------|--------------|
| `koneksi.php` | 4 | 2 | Sederhana |
| `index.php` | 5 | 2 | Sederhana |
| `dashboard.php` | 7 | 3 | Sederhana–Menengah |
| `admin.php` | 11 | 7 | Menengah |
| `kembali.php` | 7 | 2 | Sederhana |
| `kirim_email.php` | 7 | 2 | Sederhana |
| `logout.php` | 3 | 1 | Sangat Sederhana |
| **TOTAL** | **44** | **19** | **Kompleksitas Keseluruhan: Sedang** |

---

## 5. Temuan & Rekomendasi

### ⚠️ 5.1 Kerentanan SQL Injection

| File | Kode Bermasalah | Risiko | Rekomendasi |
|------|----------------|--------|-------------|
| `admin.php` | `WHERE users.nama LIKE '%$keyword%'` | SQL Injection via `GET['cari']` | Gunakan `mysqli_prepare()` |
| `kembali.php` | `WHERE id='$id'` | SQL Injection via `POST['id']` | Cast ke integer: `$id = (int)$_POST['id']` |
| `koneksi.php` | Password root kosong `('')` | Akses DB tanpa autentikasi | Set password untuk user root MySQL |

**Contoh perbaikan `kembali.php`:**
```php
// ❌ Rentan SQL Injection
$data = mysqli_query($conn, "SELECT * FROM peminjaman WHERE id='$id'");

// ✅ Aman dengan prepared statement
$stmt = mysqli_prepare($conn, "SELECT * FROM peminjaman WHERE id = ?");
mysqli_stmt_bind_param($stmt, "i", $id);
mysqli_stmt_execute($stmt);
$data = mysqli_stmt_get_result($stmt);
```

---

### 🔐 5.2 Kerentanan Keamanan Lainnya

| Prioritas | Masalah | File | Solusi |
|-----------|---------|------|--------|
| 🔴 KRITIS | Kredensial SMTP hardcoded | `kirim_email.php` | Pindahkan ke `.env` + gunakan `getenv()` |
| 🔴 KRITIS | SQL Injection | `admin.php`, `kembali.php` | Gunakan prepared statement |
| 🟠 TINGGI | `kembali.php` tanpa cek autentikasi | `kembali.php` | Tambah `session_start()` + cek role admin |
| 🟠 TINGGI | Output tanpa escape (XSS) | `admin.php` | Wrap dengan `htmlspecialchars()` |
| 🟡 SEDANG | Tidak ada CSRF token | `dashboard.php`, `admin.php` | Tambah token tersembunyi di setiap form POST |
| 🟢 RENDAH | Password DB kosong | `koneksi.php` | Set password MySQL untuk root |

**Contoh perbaikan XSS di `admin.php`:**
```php
// ❌ Rentan XSS
<td><?= $d['nama'] ?></td>

// ✅ Aman
<td><?= htmlspecialchars($d['nama'], ENT_QUOTES, 'UTF-8') ?></td>
```

**Contoh perbaikan kredensial `kirim_email.php`:**
```php
// ❌ Hardcoded
$mail->Username = 'rianaldika0126@gmail.com';
$mail->Password = 'imxj dkkk iadf ceyy';

// ✅ Gunakan environment variable
$mail->Username = getenv('SMTP_USER');
$mail->Password = getenv('SMTP_PASS');
```

---

## 6. Kesimpulan

White Box Testing terhadap aplikasi Perpustakaan Digital telah berhasil dilakukan terhadap **7 modul PHP** dengan total **21 test case**. Seluruh test case menunjukkan hasil **PASS** dari sisi fungsionalitas alur logika program.

| Aspek | Hasil |
|-------|-------|
| Total modul diuji | 7 file PHP |
| Total test case | 21 test case |
| Test PASS | 21 (100%) ✅ |
| Test FAIL | 0 (0%) |
| Kerentanan ditemukan | 6 isu (2 kritis, 2 tinggi, 1 sedang, 1 rendah) |
| Cyclomatic Complexity | Total 19 — Sedang (dapat dikelola) |

> **Rekomendasi utama:** Lakukan perbaikan keamanan sebelum deployment, terutama penerapan **prepared statement** untuk mencegah SQL Injection dan pemindahan **kredensial SMTP** ke environment variable agar tidak terekspos di source code.
