# Tugas ELiminasi  (3)

## 1. SPL (Sistem Persamaan Linear) 

$$\begin{cases}
1x_1 + 0x_2 + 0x_3 + 0x_4 + 0x_5 = 1 \\
2x_1 + 1x_2 + 0x_3 + 0x_4 + 0x_5 = 4 \\
0x_1 + 3x_2 + 1x_3 + 0x_4 + 0x_5 = 9 \\
0x_1 + 0x_2 + 4x_3 + 1x_4 + 0x_5 = 16 \\
0x_1 + 0x_2 + 0x_3 + 5x_4 + 1x_5 = 25
\end{cases}$$

## 2. Matriks Augmented 

$$\left[
\begin{array}{ccccc|c}
1 & 0 & 0 & 0 & 0 & 1 \\
2 & 1 & 0 & 0 & 0 & 4 \\
1 & 3 & 1 & 0 & 0 & 9 \\
1 & 0 & 4 & 1 & 0 & 16 \\
1 & 0 & 0 & 5 & 1 & 25
\end{array}
\right]$$

## 3. Eliminasi Gauss (OBE) 

### Langkah 1: nolkan elemen di bawah pivot kolom 1 

Operasi baris: $$R_2 \leftarrow R_2 - 2R_1$$

Penjelasan:

1.  Pivot pertama ada di kolom 1 baris 1 (angka 1).

2.  Di bawahnya (baris 2 kolom 1) ada angka 2.

3.  Kita ingin membuat elemen tersebut menjadi 0.

4.  Caranya dengan mengurangkan 2 kali baris 1 dari baris 2.

$$\left[
\begin{array}{ccccc|c}
1 & 0 & 0 & 0 & 0 & 1 \\
0 & 1 & 0 & 0 & 0 & 2 \\
1 & 3 & 1 & 0 & 0 & 9 \\
1 & 0 & 4 & 1 & 0 & 16 \\
1 & 0 & 0 & 5 & 1 & 25
\end{array}
\right]$$

### Langkah 2: nolkan elemen di bawah pivot kolom 2 

Operasi baris: $$R_3 \leftarrow R_3 - 3R_2$$

Penjelasan:

1.  Pivot kedua ada di kolom 2 baris 2 (angka 1).

2.  Di bawahnya (baris 3 kolom 2) ada angka 3.

3.  Kita membuat elemen tersebut menjadi 0 dengan mengurangkan 3 kali
    baris 2.

$$\left[
\begin{array}{ccccc|c}
1 & 0 & 0 & 0 & 0 & 1 \\
0 & 1 & 0 & 0 & 0 & 2 \\
1 & 0 & 1 & 0 & 0 & 3 \\
1 & 0 & 4 & 1 & 0 & 16 \\
1 & 0 & 0 & 5 & 1 & 25
\end{array}
\right]$$

### Langkah 3: nolkan elemen di bawah pivot kolom 3 

Operasi baris: $$R_4 \leftarrow R_4 - 4R_3$$

Penjelasan:

1.  Pivot ketiga ada di kolom 3 baris 3 (angka 1).

2.  Di bawahnya (baris 4 kolom 3) ada angka 4.

3.  Elemen tersebut dinolkan dengan mengurangkan 4 kali baris 3.

$$\left[
\begin{array}{ccccc|c}
1 & 0 & 0 & 0 & 0 & 1 \\
0 & 1 & 0 & 0 & 0 & 2 \\
1 & 0 & 1 & 0 & 0 & 3 \\
1 & 0 & 0 & 1 & 0 & 4 \\
1 & 0 & 0 & 5 & 1 & 25
\end{array}
\right]$$

### Langkah 4: nolkan elemen di bawah pivot kolom 4 

Operasi baris: $$R_5 \leftarrow R_5 - 5R_4$$

Penjelasan:

1.  Pivot keempat ada di kolom 4 baris 4 (angka 1).

2.  Di bawahnya (baris 5 kolom 4) ada angka 5.

3.  Elemen tersebut dibuat nol dengan mengurangkan 5 kali baris 4.

$$\left[
    \begin{array}{ccccc|c}
    1 & 0 & 0 & 0 & 0 & 1 \\
    0 & 1 & 0 & 0 & 0 & 2 \\
    1 & 0 & 1 & 0 & 0 & 3 \\
    1 & 0 & 0 & 1 & 0 & 4 \\
    1 & 0 & 0 & 0 & 1 & 5
    \end{array}
    \right]$$$$

## Hasil Akhir 

$$x_1 = 1,\quad x_2 = 2,\quad x_3 = 3,\quad x_4 = 4,\quad x_5 = 5$$


## SAGE CELL

![original image](https://cdn.mathpix.com/snip/images/aeU_3-oDook_mnKKIv2FYWNZY-_fwbTFVqVEcXw9jo4.original.fullsize.png)

Kesimpulan: Eliminasi Gauss adalah metode efisien untuk menyelesaikan sistem persamaan linear (SPL) dengan mengubah matriks diperbesar menjadi bentuk eselon baris (segitiga atas) menggunakan operasi baris elementer. Proses ini diakhiri dengan substitusi balik untuk mendapatkan solusi, menjadikannya metode sistematis yang ampuh. 