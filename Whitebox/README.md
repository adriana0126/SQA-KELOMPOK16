# White Box Testing

## Deskripsi

White Box Testing merupakan metode pengujian perangkat lunak yang berfokus pada struktur internal program, logika kode, jalur eksekusi, kondisi percabangan, serta alur kontrol yang terdapat pada source code. Pengujian ini dilakukan untuk memastikan bahwa setiap jalur program dapat berjalan sesuai dengan yang diharapkan.

Pada project Sistem Informasi Perpustakaan, White Box Testing diterapkan pada modul Login karena modul tersebut merupakan salah satu fitur utama yang digunakan untuk mengontrol akses pengguna ke dalam sistem.

## Tujuan Pengujian

Adapun tujuan dari White Box Testing yang dilakukan adalah sebagai berikut:

* Menganalisis alur logika program login.
* Mengidentifikasi seluruh jalur eksekusi yang mungkin terjadi.
* Menghitung tingkat kompleksitas program menggunakan Cyclomatic Complexity.
* Menentukan jalur independen yang harus diuji.
* Memastikan seluruh jalur program dapat dieksekusi tanpa menghasilkan error.

## Struktur Pengujian

Folder WhiteBox terdiri dari beberapa dokumen sebagai berikut:

### 1. FlowGraphLogin.md

Berisi representasi alur logika program login dalam bentuk Flow Graph yang digunakan untuk menggambarkan hubungan antar proses, percabangan, dan jalur eksekusi program.

### 2. CyclomaticComplexity.md

Berisi perhitungan Cyclomatic Complexity berdasarkan jumlah node dan edge yang terdapat pada Flow Graph. Hasil perhitungan digunakan untuk menentukan jumlah jalur independen yang harus diuji.

### 3. BasisPathTesting.md

Berisi skenario pengujian terhadap seluruh jalur independen yang diperoleh dari hasil perhitungan Cyclomatic Complexity. Pengujian dilakukan untuk memastikan setiap jalur program berjalan sesuai dengan hasil yang diharapkan.

## Metode Pengujian

Tahapan White Box Testing yang dilakukan pada project ini adalah:

1. Menganalisis source code modul login.
2. Membuat Flow Graph berdasarkan alur program.
3. Menghitung Cyclomatic Complexity.
4. Menentukan Independent Path.
5. Melakukan Basis Path Testing.
6. Mendokumentasikan hasil pengujian.

## Hasil Pengujian

Berdasarkan hasil perhitungan Cyclomatic Complexity diperoleh nilai sebesar 4, yang menunjukkan bahwa terdapat 4 jalur independen yang harus diuji. Seluruh jalur independen berhasil dieksekusi dengan status PASS sehingga modul login dinyatakan berjalan sesuai dengan kebutuhan sistem.

## Kesimpulan

White Box Testing yang dilakukan pada modul Login Sistem Informasi Perpustakaan berhasil menguji seluruh jalur independen yang terdapat pada program. Hasil pengujian menunjukkan bahwa logika program telah berjalan dengan baik dan tidak ditemukan kesalahan pada jalur eksekusi yang diuji.

