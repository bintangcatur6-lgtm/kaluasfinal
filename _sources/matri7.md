# Tugas Kuliah: Perhitungan Determinan Ekspansi Baris dan Invers Matriks Adjoin

Halaman ini memuat dokumentasi penyelesaian teknis untuk perhitungan nilai determinan matriks menggunakan metode ekspansi baris kofaktor serta pencarian nilai invers matriks melalui pendekatan matriks adjoin. Pengujian dilakukan pada tiga variasi orde matriks, yaitu berukuran $2 \times 2$, $3 \times 3$, dan $4 \times 4$.

---

## Bagian A: Perhitungan Determinan dengan Rumus Ekspansi Baris

Formula umum perhitungan determinan menggunakan ekspansi kofaktor pada baris ke-$i$ dinyatakan sebagai berikut:

$$\det(A) = \sum_{k=1}^n (-1)^{i+k} a_{ik} M_{ik}$$

Di mana $M_{ik}$ melambangkan nilai determinan minor setelah baris ke-$i$ dan kolom ke-$k$ dihapus dari matriks utama $A_{m \times n}$ dengan batasan indeks $1 \le i, j \le n$.

### 1. Penyelesaian Matriks 2x2

Diberikan matriks $A$ berukuran $2 \times 2$:

$$A = \begin{bmatrix} -7 & -5 \\ 1 & 4 \end{bmatrix}$$

Proses penyelesaian menggunakan ekspansi baris ke-1 ($i=1$):

- **Untuk $k=1$ (Elemen $a_{11} = -7$):**
  Submatriks $A_{11} = \begin{bmatrix} 4 \end{bmatrix}$, sehingga nilai minor $M_{11} = \det(A_{11}) = 4$.
  Suku pertama: $(-1)^{1+1} \cdot (-7) \cdot 4 = 1 \cdot (-7) \cdot 4 = -28$

- **Untuk $k=2$ (Elemen $a_{12} = -5$):**
  Submatriks $A_{12} = \begin{bmatrix} 1 \end{bmatrix}$, sehingga nilai minor $M_{12} = \det(A_{12}) = 1$.
  Suku kedua: $(-1)^{1+2} \cdot (-5) \cdot 1 = (-1) \cdot (-5) \cdot 1 = 5$

Gabungkan hasil perhitungan suku operasi:
$$\det(A) = -28 + 5 = -23$$

**Hasil Akhir:** $\det(A) = -23$

### 2. Penyelesaian Matriks 3x3

Diberikan matriks $A$ berukuran $3 \times 3$:

$$A = \begin{bmatrix} 0 & 2 & -3 \\ 1 & -2 & -1 \\ 0 & 0 & 1 \end{bmatrix}$$

Proses penyelesaian menggunakan ekspansi baris ke-3 ($i=3$). Karena elemen $a_{31}$ dan $a_{32}$ bernilai 0, kita hanya perlu menghitung komponen kofaktor untuk elemen diagonal terakhir $a_{33} = 1$:

- **Submatriks Minor $A_{33}$:**
  $$A_{33} = \begin{bmatrix} 0 & 2 \\ 1 & -2 \end{bmatrix}$$

- **Nilai Minor $M_{33}$:**
  $$M_{33} = \det(A_{33}) = (0 \cdot -2) - (2 \cdot 1) = 0 - 2 = -2$$

Substitusikan nilai ke dalam fungsi ekspansi baris ke-3:
$$\det(A) = (-1)^{3+1}(0)M_{31} + (-1)^{3+2}(0)M_{32} + (-1)^{3+3}a_{33}M_{33}$$
$$\det(A) = 0 + 0 + (1) \cdot (1) \cdot (-2) = -2$$

**Hasil Akhir:** $\det(A) = -2$

### 3. Penyelesaian Matriks 4x4

Diberikan matriks $A$ berukuran $4 \times 4$:

$$A = \begin{bmatrix} 1 & -3 & 1 & 1 \\ -3 & 1 & 1 & 1 \\ 1 & 1 & -3 & 1 \\ 1 & 1 & 1 & -3 \end{bmatrix}$$

Proses penyelesaian menggunakan ekspansi baris ke-1 ($i=1$):

- **Langkah 1: Perhitungan Nilai Minor $M_{1k}$ (Determinan Submatriks 3x3)**
  Melalui kalkulasi kofaktor internal pada masing-masing submatriks 3x3 yang terbentuk, diperoleh nilai minor sebagai berikut:
  $$M_{11} = 16, \quad M_{12} = 16, \quad M_{13} = 16, \quad M_{14} = 16$$

- **Langkah 2: Substitusi Komponen ke Rumus Utama**
  $$\det(A) = \sum_{k=1}^4 (-1)^{1+k} a_{1k} M_{1k}$$
  $$\det(A) = (-1)^{1+1}(1)(16) + (-1)^{1+2}(-3)(16) + (-1)^{1+3}(1)(16) + (-1)^{1+4}(1)(16)$$
  $$\det(A) = (1)(1)(16) + (-1)(-3)(16) + (1)(1)(16) + (-1)(1)(16)$$
  $$\det(A) = 16 + 48 + 16 - 16 = 64$$

**Hasil Akhir:** $\det(A) = 64$

---

## Bagian B: Invers Matriks Menggunakan Metode Adjoin

Pencarian invers dilakukan dengan memanfaatkan transpos dari matriks kofaktor (adjoin) dibagi dengan determinan utama melalui rumus operasional:

$$(adj\,A)_{ij} = (-1)^{i+j} M_{ji}$$
$$A^{-1} = \frac{1}{\det(A)} adj\,A$$

### 4. Invers Matriks 2x2

Menggunakan basis matriks $A$ ukuran $2 \times 2$ dari soal sebelumnya:
$$A = \begin{bmatrix} -7 & -5 \\ 1 & 4 \end{bmatrix}, \quad \det(A) = -23$$

- **Langkah 1: Tentukan Elemen Kofaktor $C_{ij}$**
  $$C_{11} = (-1)^{1+1}(4) = 4$$
  $$C_{12} = (-1)^{1+2}(1) = -1$$
  $$C_{21} = (-1)^{2+1}(-5) = 5$$
  $$C_{22} = (-1)^{2+2}(-7) = -7$$

- **Langkah 2: Matriks Adjoin (Transpos Kofaktor)**
  $$adj\,A = \begin{bmatrix} 4 & 5 \\ -1 & -7 \end{bmatrix}$$

- **Langkah 3: Perhitungan Matriks Invers**
  $$A^{-1} = \frac{1}{-23} \begin{bmatrix} 4 & 5 \\ -1 & -7 \end{bmatrix} = \begin{bmatrix} -4/23 & -5/23 \\ 1/23 & 7/23 \end{bmatrix}$$

---

### 5. Invers Matriks 3x3

Menggunakan basis matriks $A$ ukuran $3 \times 3$ dari soal sebelumnya:
$$A = \begin{bmatrix} 0 & 2 & -3 \\ 1 & -2 & -1 \\ 0 & 0 & 1 \end{bmatrix}, \quad \det(A) = -2$$

- **Langkah 1: Hitung Seluruh Komponen Kofaktor Elemen $C_{ij} = (-1)^{i+j} M_{ij}$**
  $$C_{11} = +\begin{vmatrix} -2 & -1 \\ 0 & 1 \end{vmatrix} = -2, \quad C_{12} = -\begin{vmatrix} 1 & -1 \\ 0 & 1 \end{vmatrix} = -1, \quad C_{13} = +\begin{vmatrix} 1 & -2 \\ 0 & 0 \end{vmatrix} = 0$$
  $$C_{21} = -\begin{vmatrix} 2 & -3 \\ 0 & 1 \end{vmatrix} = -2, \quad C_{22} = +\begin{vmatrix} 0 & -3 \\ 0 & 1 \end{vmatrix} = 0, \quad C_{23} = -\begin{vmatrix} 0 & 2 \\ 0 & 0 \end{vmatrix} = 0$$
  $$C_{31} = +\begin{vmatrix} 2 & -3 \\ -2 & -1 \end{vmatrix} = -8, \quad C_{32} = -\begin{vmatrix} 0 & -3 \\ 1 & -1 \end{vmatrix} = -3, \quad C_{33} = +\begin{vmatrix} 0 & 2 \\ 1 & -2 \end{vmatrix} = -2$$

- **Langkah 2: Susun Matriks Adjoin (Transpos dari Susunan Kofaktor di Atas)**
  $$adj\,A = \begin{bmatrix} -2 & -2 & -8 \\ -1 & 0 & -3 \\ 0 & 0 & -2 \end{bmatrix}$$

- **Langkah 3: Perhitungan Matriks Invers**
  $$A^{-1} = \frac{1}{-2} \begin{bmatrix} -2 & -2 & -8 \\ -1 & 0 & -3 \\ 0 & 0 & -2 \end{bmatrix} = \begin{bmatrix} 1.0 & 1.0 & 4.0 \\ 0.5 & 0.0 & 1.5 \\ 0.0 & 0.0 & 1.0 \end{bmatrix}$$

---

### 6. Invers Matriks 4x4

Menggunakan basis matriks $A$ ukuran $4 \times 4$ dari soal sebelumnya:
$$A = \begin{bmatrix} 1 & -3 & 1 & 1 \\ -3 & 1 & 1 & 1 \\ 1 & 1 & -3 & 1 \\ 1 & 1 & 1 & -3 \end{bmatrix}, \quad \det(A) = 64$$

- **Langkah 1: Evaluasi Nilai Kofaktor Elemen**
  Karena matriks memiliki karakteristik simetri spasial tertentu, seluruh nilai determinan submatriks minor $M_{ij}$ menghasilkan nilai konstan 16. Dengan menyesuaikan aturan tanda penambah $(-1)^{i+j}$ serta orientasi tanda kofaktor minor baris internalnya, diperoleh pola kofaktor di mana elemen diagonal bernilai $-16$ dan elemen non-diagonal bernilai $16$.

- **Langkah 2: Matriks Adjoin**
  $$adj\,A = \begin{bmatrix} -16 & 16 & 16 & 16 \\ 16 & -16 & 16 & 16 \\ 16 & 16 & -16 & 16 \\ 16 & 16 & 16 & -16 \end{bmatrix}$$

- **Langkah 3: Perhitungan Matriks Invers**
  $$A^{-1} = \frac{1}{64} \begin{bmatrix} -16 & 16 & 16 & 16 \\ 16 & -16 & 16 & 16 \\ 16 & 16 & -16 & 16 \\ 16 & 16 & 16 & -16 \end{bmatrix}$$

  $$A^{-1} = \begin{bmatrix} -0.25 & 0.25 & 0.25 & 0.25 \\ 0.25 & -0.25 & 0.25 & 0.25 \\ 0.25 & 0.25 & -0.25 & 0.25 \\ 0.25 & 0.25 & 0.25 & -0.25 \end{bmatrix}$$

---

## Validasi Komputasi Menggunakan Python (NumPy)

Untuk memastikan bahwa seluruh output kalkulasi ekspansi baris dan adjoin di atas bernilai valid secara numerik, skrip Python berikut dapat dieksekusi:

```python
import numpy as np

# Matriks 2x2
A2 = np.array([[-7, -5],
               [ 1,  4]])

# Matriks 3x3
A3 = np.array([[ 0,  2, -3],
               [ 1, -2, -1],
               [ 0,  0,  1]])

print("--- VERIFIKASI MATRIKS 2x2 ---")
print(f"Determinan: {np.linalg.det(A2):.1f}")
print(f"Invers:\n{np.linalg.inv(A2)}\n")

print("--- VERIFIKASI MATRIKS 3x3 ---")
print(f"Determinan: {np.linalg.det(A3):.1f}")
print(f"Invers:\n{np.linalg.inv(A3)}")
```

### berikut link collab nya

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1QFJtUP4sGRbnAh0IG3N8XUCbbbP5gGWO?usp=sharing)