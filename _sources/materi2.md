# Tugas Transformasi sumbu Y menggunakan Translasi dan pencerminan

## # Tugas Transformasi sumbu Y menggunakan Translasi dan pencerminan

## 1. Titik Awal

Objek awal berupa persegi dengan titik:

A(1,1)
B(3,1)
C(3,3)
D(1,3)

Dalam bentuk matriks (koordinat homogen):
$$
P =
\begin{bmatrix}
x \\
y \\
1
\end{bmatrix}
$$

## 2. Translasi (Langkah Pertama)

Pada program, setiap titik digeser ke kanan sejauh 1 satuan.

Rumus:

$$
T(x,y) = (x+1, y)
$$

Matriks translasi:	​
Matriks translasi:

$$
T =
\begin{bmatrix}
1 & 0 & 1 \\
0 & 1 & 0 \\
0 & 0 & 1
\end{bmatrix}
$$

Transformasi:

$$
P' = T \cdot P
$$

dengan:

$$
P =
\begin{bmatrix}
x \\
y \\
1
\end{bmatrix}
$$

Hasil:

$$
(x, y) \rightarrow (x+1, y)
$$

Contoh:

$$
A(1,1) \rightarrow (2,1)
$$
​
	​

Contoh hasil translasi (Step 1):
A(1,1) → A₁(2,1)
B(3,1) → B₁(4,1)
C(3,3) → C₁(4,3)
D(1,3) → D₁(2,3)


## 3. Refleksi terhadap Sumbu Y

Refleksi terhadap sumbu Y dapat ditulis dalam bentuk matriks:

$$
R =
\begin{bmatrix}
-1 & 0 \\
0 & 1
\end{bmatrix}
$$

Sehingga transformasinya:

$$
P' = R \cdot P
$$

dengan:

$$
P =
\begin{bmatrix}
x \\
y
\end{bmatrix}
$$

Hasilnya:

$$
\begin{bmatrix}
x' \\
y'
\end{bmatrix}
=
\begin{bmatrix}
-1 & 0 \\
0 & 1
\end{bmatrix}
\begin{bmatrix}
x \\
y
\end{bmatrix}
=
\begin{bmatrix}
-x \\
y
\end{bmatrix}
$$

Rumus:

R(x,y)=(−x,y)

Matriks refleksi terhadap sumbu Y:

$$
R =
\begin{bmatrix}
-1 & 0 & 0 \\
0 & 1 & 0 \\
0 & 0 & 1
\end{bmatrix}
$$

Transformasi:

$$
P' = R \cdot P
$$

dengan:

$$
P =
\begin{bmatrix}
x \\
y \\
1
\end{bmatrix}
$$

Hasil:

$$
(x, y) \rightarrow (-x, y)
$$

Contoh hasil refleksi (dari Step 1):
A₁(2,1) → A'(−2,1)
B₁(4,1) → B'(−4,1)
C₁(4,3) → C'(−4,3)
D₁(2,3) → D'(−2,3)

## 4. Transformasi Gabungan

UUrutan transformasi:
Translasi kemudian refleksi

Sehingga:

$$
P' = R \cdot T \cdot P
$$

Dengan:

$$
T =
\begin{bmatrix}
1 & 0 & 1 \\
0 & 1 & 0 \\
0 & 0 & 1
\end{bmatrix}
,\quad
R =
\begin{bmatrix}
-1 & 0 & 0 \\
0 & 1 & 0 \\
0 & 0 & 1
\end{bmatrix}
$$

Matriks gabungan:

$$
R \cdot T =
\begin{bmatrix}
-1 & 0 & -1 \\
0 & 1 & 0 \\
0 & 0 & 1
\end{bmatrix}
$$

## 5. Hasil Transformasi Akhir

Hasil Transformasi Akhir:

$$
(x, y) \rightarrow (-(x+1), y)
$$
## 6. Proses Berulang (Sesuai Loop di Program)

Transformasi dilakukan sebanyak 6 langkah.

Contoh beberapa step:

Step 0 (awal):

A(1,1)

Step 1:

Translasi → (2,1)
Refleksi → (−2,1)

Step 2:

Translasi → (3,1)
Refleksi → (−3,1)

Step 3:

Translasi → (4,1)
Refleksi → (−4,1)

dan seterusnya

Pola transformasi:

$$
(x, y) \rightarrow (x+n, y) \rightarrow (-(x+n), y)
$$

## 7. Hubungan dengan T(x) = A(x)

Dalam konteks program:

T(x) = hasil translasi
A(x) = hasil akhir (setelah refleksi)

Sehingga:

$$
A(x, y) = R(T(x, y))
$$

## 8. Kesimpulan
Titik A, B, C, D membentuk persegi
Objek bergerak ke kanan setiap langkah
Setiap hasil langsung dicerminkan ke sumbu Y
Transformasi dilakukan secara bertahap (animasi)

Transformasi akhir:

Komposisi dalam bentuk matriks:
Urutan transformasi:
Translasi kemudian refleksi

Sehingga:

$$
P' = R \cdot T \cdot P
$$

Dengan:

$$
T =
\begin{bmatrix}
1 & 0 & 1 \\
0 & 1 & 0 \\
0 & 0 & 1
\end{bmatrix}
,\quad
R =
\begin{bmatrix}
-1 & 0 & 0 \\
0 & 1 & 0 \\
0 & 0 & 1
\end{bmatrix}
$$

Matriks gabungan:

$$
R \cdot T =
\begin{bmatrix}
-1 & 0 & -1 \\
0 & 1 & 0 \\
0 & 0 & 1
\end{bmatrix}
$$
