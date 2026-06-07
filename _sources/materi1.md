# (SPL)Sistem Persaman Linier

## # (SPL)Sistem Persaman Linier

## 1.(SPL)Sistem Persaman Linier
$$\begin{cases} 
2x_1 + 0x_2 + 0x_3 + 0x_4 + 0x_5 = 2 \\
4x_1 + 3x_2 + 0x_3 + 0x_4 + 0x_5 = 10 \\
1x_1 + 2x_2 + 2x_3 + 0x_4 + 0x_5 = 11 \\
3x_1 + 1x_2 + 1x_3 + 1x_4 + 0x_5 = 12 \\
2x_1 + 3x_2 + 1x_3 + 2x_4 + 1x_5 = 24 
\end{cases}$$

## 2. Matriks Augmented
$$\left[ \begin{array}{ccccc|c} 
2 & 0 & 0 & 0 & 0 & 2 \\
4 & 3 & 0 & 0 & 0 & 10 \\
1 & 2 & 2 & 0 & 0 & 11 \\
3 & 1 & 1 & 1 & 0 & 12 \\
2 & 3 & 1 & 2 & 1 & 24 
\end{array} \right]$$

## 3.Eliminasi Gauss (OBE)

### Langkah 1:

 Menjadikan Pivot Baris 1 menjadi 1Kita bagi Baris 1 ($R_1$) dengan 2 Operasi: 
 
 $R_1 \leftarrow \frac{1}{2} R_1$ 

 $$[ \begin{array}{ccccc|c} 
\mathbf{1} & 0 & 0 & 0 & 0 & 1 \\
4 & 3 & 0 & 0 & 0 & 10 \\
1 & 2 & 2 & 0 & 0 & 11 \\
3 & 1 & 1 & 1 & 0 & 12 \\
2 & 3 & 1 & 2 & 1 & 24 
\end{array}

### Langkah 2: 

Mengnolkan elemen di bawah Pivot Kolom 1 Kita akan mengnolkan angka 4, 1, 3, dan 2 pada kolom pertama.

$R_2 \leftarrow R_2 - 4R_1$ (Hasil: $10 - 4(1) = 6$)

$R_3 \leftarrow R_3 - 1R_1$ (Hasil: $11 - 1(1) = 10$)

$R_4 \leftarrow R_4 - 3R_1$ (Hasil: $12 - 3(1) = 9$)

$R_5 \leftarrow R_5 - 2R_1$ (Hasil: $24 - 2(1) = 22$)

$$\left[ \begin{array}{ccccc|c} 
1 & 0 & 0 & 0 & 0 & 1 \\
0 & \mathbf{3} & 0 & 0 & 0 & 6 \\
0 & 2 & 2 & 0 & 0 & 10 \\
0 & 1 & 1 & 1 & 0 & 9 \\
0 & 3 & 1 & 2 & 1 & 22 
\end{array} \right]$$


### Langkah 3: 

Menjadikan Pivot Baris 2 menjadi 1Operasi: 

$R_2 \leftarrow \frac{1}{3} R_2$ (Hasil: $6/3 = 2$)

$$\left[ \begin{array}{ccccc|c} 
1 & 0 & 0 & 0 & 0 & 1 \\
0 & \mathbf{1} & 0 & 0 & 0 & 2 \\
0 & 2 & 2 & 0 & 0 & 10 \\
0 & 1 & 1 & 1 & 0 & 9 \\
0 & 3 & 1 & 2 & 1 & 22 
\end{array} \right]$$

### Langkah 4:

 Mengnolkan elemen di bawah Pivot Kolom 2
 
 $R_3 \leftarrow R_3 - 2R_2$ (Hasil: $10 - 2(2) = 6$)
 
 $R_4 \leftarrow R_4 - 1R_2$ (Hasil: $9 - 1(2) = 7$)
 
 $R_5 \leftarrow R_5 - 3R_2$ (Hasil: $22 - 3(2) = 16$)
 
 $$\left[ \begin{array}{ccccc|c} 
1 & 0 & 0 & 0 & 0 & 1 \\
0 & 1 & 0 & 0 & 0 & 2 \\
0 & 0 & \mathbf{2} & 0 & 0 & 6 \\
0 & 0 & 1 & 1 & 0 & 7 \\
0 & 0 & 1 & 2 & 1 & 16 
\end{array} \right]$$

### Langkah 5: 

Menjadikan Pivot Baris 3 menjadi 1Operasi: 

$R_3 \leftarrow \frac{1}{2} R_3$ (Hasil: $6/2 = 3$)

$$\left[ \begin{array}{ccccc|c} 
1 & 0 & 0 & 0 & 0 & 1 \\
0 & 1 & 0 & 0 & 0 & 2 \\
0 & 0 & \mathbf{1} & 0 & 0 & 3 \\
0 & 0 & 1 & 1 & 0 & 7 \\
0 & 0 & 1 & 2 & 1 & 16 
\end{array} \right]$$

### Langkah 6: 

Mengnolkan elemen di bawah Pivot Kolom 3

$R_4 \leftarrow R_4 - 1R_3$ (Hasil: $7 - 3 = 4$)

$R_5 \leftarrow R_5 - 1R_3$ (Hasil: $16 - 3 = 13$)

$$\left[ \begin{array}{ccccc|c} 
1 & 0 & 0 & 0 & 0 & 1 \\
0 & 1 & 0 & 0 & 0 & 2 \\
0 & 0 & 1 & 0 & 0 & 3 \\
0 & 0 & 0 & \mathbf{1} & 0 & 4 \\
0 & 0 & 0 & 2 & 1 & 13 
\end{array} \right]$$


### Hasil Akhir:  \begin{array}{ccccc|c} 
1 & 0 & 0 & 0 & 0 & 1 \\
0 & 1 & 0 & 0 & 0 & 2 \\
0 & 0 & 1 & 0 & 0 & 3 \\
0 & 0 & 0 & 1 & 0 & 4 \\
0 & 0 & 0 & 0 & \mathbf{1} & 5 
\end{array}