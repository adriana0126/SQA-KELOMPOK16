# Cyclomatic Complexity Login

## Pendahuluan

Cyclomatic Complexity merupakan metode yang digunakan untuk mengukur tingkat kompleksitas logika suatu program berdasarkan jumlah node dan edge yang terdapat pada Flow Graph. Nilai yang diperoleh digunakan untuk menentukan jumlah minimum jalur independen yang harus diuji.

## Data Flow Graph

Jumlah Node (N) = 11

Jumlah Edge (E) = 13

### Daftar Edge

```text
1 → 2
2 → 3
3 → 4
3 → 5
4 → 10
5 → 6
6 → 9
6 → 7
7 → 8
7 → 11
8 → 10
9 → 10
11 → 10
```

## Perhitungan

Rumus Cyclomatic Complexity:

```text
V(G) = E - N + 2
```

Keterangan:

- E = Jumlah Edge
- N = Jumlah Node

Perhitungan:

```text
V(G) = 13 - 11 + 2
V(G) = 4
```

## Hasil

Nilai Cyclomatic Complexity yang diperoleh adalah:

```text
V(G) = 4
```

Nilai tersebut menunjukkan bahwa terdapat empat jalur independen yang harus diuji pada modul login.

## Analisis

Berdasarkan hasil perhitungan, tingkat kompleksitas modul login tergolong rendah sehingga lebih mudah dipahami, diuji, dan dipelihara. Jumlah jalur independen yang sedikit juga mempermudah proses pengujian secara menyeluruh.

## Kesimpulan

Cyclomatic Complexity pada modul login menghasilkan nilai 4, yang berarti terdapat empat jalur independen yang wajib diuji untuk memastikan seluruh logika program berjalan sesuai dengan kebutuhan sistem.
