# Tugas Komputasi Determinan Menggunakan Operasi Baris Elementer (OBE)

Pada bab penutup ini, kita akan mempelajari pendekatan numerik untuk menghitung nilai determinan dari suatu matriks persegi menggunakan **Operasi Baris Elementer (OBE)**.

Meskipun metode Sarrus dan Ekspansi Kofaktor sangat populer, kedua metode tersebut memiliki kompleksitas waktu faktorial $\mathcal{O}(n!)$, yang membuatnya sangat lambat dan tidak efisien untuk memproses matriks berdimensi besar di dalam ilmu komputer. Sebagai solusinya, kita menggunakan metode eliminasi Gauss (OBE) yang memiliki kompleksitas jauh lebih cepat, yaitu $\mathcal{O}(n^3)$.

---

## 1. Sifat-Sifat Determinan Terhadap Operasi Baris Elementer (OBE)

Saat kita melakukan transformasi baris pada matriks untuk membentuk matriks segitiga atas, setiap jenis operasi baris akan memberikan efek yang berbeda terhadap nilai determinan asli. Berikut adalah tiga aturan dasar yang wajib diperhatikan:

1. **Pertukaran Dua Baris ($R_i \leftrightarrow R_j$):** Jika dua baris pada matriks saling ditukar posisinya, maka nilai determinan matriks baru akan menjadi negatif dari determinan sebelumnya.
   $$\det(A_{\text{baru}}) = -\det(A_{\text{lama}})$$

2. **Perkalian Baris dengan Konstanta Skalar ($k \cdot R_i \rightarrow R_i$):** Jika suatu baris dikalikan dengan konstanta skalar bukan nol $k$, maka nilai determinan matriks juga akan ikut terkali dengan konstanta $k$ tersebut.
   $$\det(A_{\text{baru}}) = k \cdot \det(A_{\text{lama}})$$

3. **Penjumlahan Kelipatan Baris ($R_i + k \cdot R_j \rightarrow R_i$):** Jika suatu baris ditambahkan dengan kelipatan baris lainnya, maka **nilai determinan matriks tidak berubah sama sekali**.
   $$\det(A_{\text{baru}}) = \det(A_{\text{lama}})$$

---

## 2. Algoritma Segitiga Atas

Strategi utama dari metode ini adalah memanfaatkan Operasi Baris Elementer (khususnya aturan nomor 3 agar tidak mengubah nilai determinan) untuk menyulap matriks acak $A$ menjadi Matriks Segitiga Atas ($U$).

Setelah matriks berhasil dikonversi menjadi matriks segitiga atas (di mana seluruh elemen di bawah diagonal utamanya bernilai 0), maka nilai determinannya secara otomatis adalah **hasil perkalian dari seluruh elemen yang berada di diagonal utamanya**:

$$\det(A) = (-1)^s \cdot \prod_{i=1}^{n} u_{ii}$$

_Di mana $s$ adalah jumlah total berapa kali kita melakukan operasi pertukaran baris selama proses eliminasi._

---

## 3. Studi Kasus Perhitungan Manual

Misalkan kita memiliki matriks persegi $A$ berukuran $3 \times 3$ sebagai berikut:

$$A = \begin{bmatrix} 2 & 1 & 1 \\ 4 & 3 & 3 \\ 2 & 4 & 9 \end{bmatrix}$$

Mari kita hitung nilai determinannya menggunakan langkah-langkah OBE:

- **Langkah 1:** Eliminasi elemen di bawah poros $a_{11} = 2$.
  Kita bersihkan angka 4 pada baris kedua menggunakan operasi: $R_2 - 2R_1 \rightarrow R_2$
  $$\begin{bmatrix} 2 & 1 & 1 \\ 4 - 2(2) & 3 - 2(1) & 3 - 2(1) \\ 2 & 4 & 9 \end{bmatrix} = \begin{bmatrix} 2 & 1 & 1 \\ 0 & 1 & 1 \\ 2 & 4 & 9 \end{bmatrix}$$
  _(Ingat: Operasi ini tidak mengubah nilai determinan)_

- **Langkah 2:** Bersihkan angka 2 pada baris ketiga kolom pertama menggunakan operasi: $R_3 - 1R_1 \rightarrow R_3$
  $$\begin{bmatrix} 2 & 1 & 1 \\ 0 & 1 & 1 \\ 2 - 1(2) & 4 - 1(1) & 9 - 1(1) \end{bmatrix} = \begin{bmatrix} 2 & 1 & 1 \\ 0 & 1 & 1 \\ 0 & 3 & 8 \end{bmatrix}$$

- **Langkah 3:** Eliminasi elemen di bawah poros baru $a_{22} = 1$.
  Kita bersihkan angka 3 pada baris ketiga kolom kedua menggunakan operasi: $R_3 - 3R_2 \rightarrow R_3$
  $$\begin{bmatrix} 2 & 1 & 1 \\ 0 & 1 & 1 \\ 0 & 3 - 3(1) & 8 - 3(1) \end{bmatrix} = \begin{bmatrix} 2 & 1 & 1 \\ 0 & 1 & 1 \\ 0 & 0 & 5 \end{bmatrix}$$

Sekarang, matriks telah sukses bertransformasi menjadi **Matriks Segitiga Atas**.

- **Langkah Akhir:** Kalikan seluruh elemen diagonal utamanya.
  $$\det(A) = 2 \cdot 1 \cdot 5 = 10$$

---

## 4. Implementasi Program Python (Metode Eliminasi Gauss)

Berikut adalah kode program lengkap berbasis Python menggunakan pustaka NumPy untuk menghitung determinan dengan metode OBE secara bertahap:

```python
import numpy as np

def hitung_determinan_obe(matriks_awal):
    A = matriks_awal.copy()
    n = A.shape[0]
    determinan_sign = 1.0

    print("="*60)
    print("COMPUTATIONAL DETERMINAN MATRIKS VIA OBE")
    print("="*60)
    print(f"Matriks Awal A:\n{A}\n")

    # Proses Eliminasi Gauss
    for i in range(n):
        # 1. Antisipasi jika elemen pivot bernilai 0 (Pertukaran Baris)
        if A[i, i] == 0:
            for j in range(i + 1, n):
                if A[j, i] != 0:
                    A[[i, j]] = A[[j, i]] # Tukar baris i dan j
                    determinan_sign *= -1.0 # Aturan OBE 1: Tanda determinan berbalik
                    print(f"-> Mengubah Baris: R{i+1} <-> R{j+1} (Tanda Determinan Dikali -1)")
                    break

        # 2. Proses Eliminasi elemen di bawah pivot
        for j in range(i + 1, n):
            if A[j, i] != 0:
                faktor = A[j, i] / A[i, i]
                A[j] = A[j] - faktor * A[i] # Aturan OBE 3: Determinan konstan
                print(f"-> Operasi Baris: R{j+1} - ({faktor:.2f})*R{i+1} -> R{j+1}")

    print("\nMatriks Hasil Transformasi Segitiga Atas (U):")
    print(np.round(A, 4))

    # 3. Menghitung hasil perkalian elemen diagonal utama
    elemen_diagonal = np.diag(A)
    perkalian_diagonal = np.prod(elemen_diagonal)

    determinan_akhir = determinan_sign * perkalian_diagonal

    print("\n" + "="*60)
    print("ANALISIS KESIMPULAN NUMERIK:")
    print("="*60)
    print(f"Elemen Diagonal Utama : {np.round(elemen_diagonal, 4)}")
    print(f"Faktor Pengali Tanda  : {determinan_sign}")
    print(f"Nilai Determinan (det) : {determinan_akhir:.4f}")

    return determinan_akhir

# --- EKSEKUSI DATA UJI ---
Matriks_A = np.array([[2, 1, 1],
                      [4, 3, 3],
                      [2, 4, 9]], dtype=float)

det_A = hitung_determinan_obe(Matriks_A)
```

### berikut link collabnya

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1XDU4Czy9K_GSH3dP6pO574DA-DuYcIDa?usp=sharing)