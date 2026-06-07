# Evaluasi Determinan Dan Invers

## # Evaluasi Determinan Dan Invers

SOAL.

**A. Hitunglah determinan matrik berikut dengan menggunakan rumus expansi baris**

$$\sum_{k=1}^n (-1)^{i+k} a_{ik} M_{ik}$$

dengan $M_{ij}$ adalah minior dari matrik A dan

$$M_{ij} = \det A_{ij}.$$

$A_{ij}$ adalah submatrik dengan menghapus baris i dan kolom kolom j dari matrix $A_{mxn}$ dengan $1 \le i, j \le n$


---

## 1. Matriks 2×2 (Determinan)

$$ A = \begin{bmatrix} -7 & -5 \\ 1 & 4 \end{bmatrix} $$

Ekspansi baris pertama:

$$
\det(A) = a_{11}C_{11} + a_{12}C_{12}
$$

Minor:

$$
M_{11} = 4, \quad M_{12} = 
$$

Determinan:

$$
\det(A) = (-7)(4) + (1)(5) = -28 + 5 = -23
$$

---

## 2. Matriks 3×3 (Determinan)

$$ A = \begin{bmatrix} 0 & 1 & 0 \\ 2 & -2 & 0 \\ -3 & -1 & 1 \end{bmatrix} $$

Ekspansi baris pertama:

$$
\det(A) = a_{11}C_{11} + a_{12}C_{12} + a_{13}C_{13}
$$

Minor:

$$
M_{11} =
\begin{vmatrix}
-2 & 0 \
-1 & 1
\end{vmatrix}
= -2
$$

$$
M_{12} =
\begin{vmatrix}
2 & 0 \
-3 & 1
\end{vmatrix}
= 2
$$

$$
M_{13} =
\begin{vmatrix}
2 & -2 \
-3 & -1
\end{vmatrix}
= -2 - 6 = -8
$$

Determinan:

$$
\det(A) = 0(-2) + 1(-2) + 0(-8) = -2
$$

---

## 3. Matriks 4×4 (Determinan)

$$ A = \begin{bmatrix} 1 & -3 & 1 & 1 \\ -3 & 1 & 1 & 1 \\ 1 & 1 & -3 & 1 \\ 1 & 1 & 1 & -3 \end{bmatrix} $$

Ekspansi baris pertama:

$$
\det(A) = a_{11}C_{11} + a_{12}C_{12} + a_{13}C_{13} + a_{14}C_{14}
$$

Minor:

$$
M_{11} = 16, \quad M_{12} = -16, \quad M_{13} = 16, \quad M_{14} = -16
$$

Determinan:

$$
\det(A) = 1(16) + (-3)(16) + 1(16) + 1(16)
= 16 - 48 + 16 + 16 = 0
$$

---

**B. Gunakan rumus matriks adjoin untuk menghitung invers dari matriks berikut dengan rumus**

$$(\operatorname{adj} A)_{ij} = (-1)^{i+j} M_{ji}$$

dan

$$A^{-1} = \frac{1}{\det A} \operatorname{adj} A.$$

---


## 4. Matriks 2×2 (Invers)

$$A = \begin{bmatrix} -7 & -5 \\ 1 & 4 \end{bmatrix}$$

Diketahui Determinan:

$$\det(A) = - 23$$

Minor:

$$
M_{11} = \begin{vmatrix} 4 \end{vmatrix} = 4
$$

$$
M_{12} = \begin{vmatrix} 1 \end{vmatrix} = 1
$$

$$
M_{21} = \begin{vmatrix} -5 \end{vmatrix} = -5
$$

$$
M_{22} = \begin{vmatrix} -7 \end{vmatrix} = -7
$$

Kofaktor:

$$
C_{11} = (+)M_{11} = 4
$$

$$
C_{12} = (-)M_{12} = -1
$$

$$
C_{21} = (-)M_{21} = 5
$$

$$
C_{22} = (+)M_{22} = -7
$$

Adjoin (Transpose kofaktor):

$$
\operatorname{adj}(A) =
\begin{bmatrix}
4 & 5 \\
-1 & -7
\end{bmatrix}
$$

Invers:

$$
A^{-1} = \frac{1}{\det(A)} \operatorname{adj}(A)
$$

$$
A^{-1} = \frac{1}{-23}
\begin{bmatrix}
4 & 5 \\
-1 & -7
\end{bmatrix}
$$

Hasil Akhir:

$$
A^{-1} =
\begin{bmatrix}
-\frac{4}{23} & -\frac{5}{23} \\
\frac{1}{23} & \frac{7}{23}
\end{bmatrix}
$$

## 5. Matriks 3×3 (Invers)

$$A = \begin{bmatrix} 0 & 2 & -3 \\ 1 & -2 & -1 \\ 0 & 0 & 1 \end{bmatrix}$$

Diketahui Determinan:

$$
\det(A) = -2
$$

Minor:

$M_{11}$:

$$
M_{11} =
\begin{vmatrix}
-2 & -1 \\
0 & 1
\end{vmatrix}
$$

$$
= (-2)(1) - (-1)(0)
$$

$$
= -2 - 0 = -2
$$

$M_{12}$:

$$
M_{12} =
\begin{vmatrix}
1 & -1 \\
0 & 1
\end{vmatrix}
$$

$$
= (1)(1) - (-1)(0)
$$

$$
= 1 - 0 = 1
$$

$M_{13}$:

$$
M_{13} =
\begin{vmatrix}
1 & -2 \\
0 & 0
\end{vmatrix}
$$

$$
= (1)(0) - (-2)(0)
$$

$$
= 0 - 0 = 0
$$

$M_{21}$:

$$
M_{21} =
\begin{vmatrix}
2 & -3 \\
0 & 1
\end{vmatrix}
$$

$$
= (2)(1) - (-3)(0)
$$

$$
= 2 - 0 = 2
$$

$M_{22}$:

$$
M_{22} =
\begin{vmatrix}
0 & -3 \\
0 & 1
\end{vmatrix}
$$

$$
= (0)(1) - (-3)(0)
$$

$$
= 0 - 0 = 0
$$

$M_{23}$:

$$
M_{23} =
\begin{vmatrix}
0 & 2 \\
0 & 0
\end{vmatrix}
$$

$$
= (0)(0) - (2)(0)
$$

$$
= 0 - 0 = 0
$$

$M_{31}$:

$$
M_{31} =
\begin{vmatrix}
2 & -3 \\
-2 & -1
\end{vmatrix}
$$

$$
= (2)(-1) - (-3)(-2)
$$

$$
= -2 - 6 = -8
$$

$M_{32}$:

$$
M_{32} =
\begin{vmatrix}
0 & -3 \\
1 & -1
\end{vmatrix}
$$

$$
= (0)(-1) - (-3)(1)
$$

$$
= 0 + 3 = 3
$$

$M_{33}$:

$$
M_{33} =
\begin{vmatrix}
0 & 2 \\
1 & -2
\end{vmatrix}
$$

$$
= (0)(-2) - (2)(1)
$$

$$
= 0 - 2 = -2
$$

Kofaktor:

$$
C_{ij} = (-1)^{i+j} M_{ij}
$$

$$
C =
\begin{bmatrix}
-2 & -1 & 0 \\
-2 & 0 & 0 \\
-8 & -3 & -2
\end{bmatrix}
$$

Adjoin (Transpose kofaktor):

$$
\operatorname{adj}(A) =
\begin{bmatrix}
-2 & -2 & -8 \\
-1 & 0 & -3 \\
0 & 0 & -2
\end{bmatrix}
$$

Invers:

$$
A^{-1} = \frac{1}{\det(A)} \operatorname{adj}(A)
$$

$$
A^{-1} = \frac{1}{-2}
\begin{bmatrix}
-2 & -2 & -8 \\
-1 & 0 & -3 \\
0 & 0 & -2
\end{bmatrix}
$$

Hasil Akhir:

$$
A^{-1} =
\begin{bmatrix}
1 & 1 & 4 \\
\frac{1}{2} & 0 & \frac{3}{2} \\
0 & 0 & 1
\end{bmatrix}
$$

## 6. Matriks 4×4 (Invers)

$$A = \begin{bmatrix} 1 & -3 & 1 & 1 \\ -3 & 1 & 1 & 1 \\ 1 & 1 & -3 & 1 \\ 1 & 1 & 1 & -3 \end{bmatrix}.$$

Diketahui Determinan:

$$
\det(A) = 0
$$

Invers

$$
A^{-1} = \frac{1}{\det(A)} \operatorname{adj}(A)
$$

Karena:

$$
\det(A) = 0
$$

maka:

$$
A^{-1} = \frac{1}{0} \operatorname{adj}(A)
$$

Pembagian dengan nol tidak terdefinisi, sehingga:

$$
A^{-1} \text{ tidak ada}
$$

---