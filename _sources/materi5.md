# Eigenface 

## Tugas Eigenface (PCA)

## 1. Data Representasi Wajah (Vektor Wajah)

Misalkan kita memiliki 3 buah gambar wajah training yang sudah diubah menjadi vektor baris 1D berukuran $1 \times 4$ piksel (dimensi rendah untuk penyederhanaan kalkulasi):

$$\begin{aligned}
\Gamma_1 &= \begin{bmatrix} 2 & 4 & 4 & 2 \end{bmatrix} \\
\Gamma_2 &= \begin{bmatrix} 4 & 2 & 2 & 4 \end{bmatrix} \\
\Gamma_3 &= \begin{bmatrix} 3 & 3 & 3 & 3 \end{bmatrix}
\end{aligned}$$

## 2. Menghitung Wajah Rata-Rata (Mean Face)

Wajah rata-rata ($\Psi$) dihitung dengan menjumlahkan seluruh vektor wajah lalu dibagi dengan jumlah sampel ($M=3$):

$$\Psi = \frac{1}{3} \sum_{i=1}^{3} \Gamma_i$$

$$\Psi = \frac{1}{3} \left( \begin{bmatrix} 2 & 4 & 4 & 2 \end{bmatrix} + \begin{bmatrix} 4 & 2 & 2 & 4 \end{bmatrix} + \begin{bmatrix} 3 & 3 & 3 & 3 \end{bmatrix} \right)$$

$$\Psi = \begin{bmatrix} 3 & 3 & 3 & 3 \end{bmatrix}$$

## 3. Normalisasi Wajah (Mencari Deviasi $\Phi$)

Setiap wajah dikurangi dengan wajah rata-rata ($\Phi_i = \Gamma_i - \Psi$):

$$\begin{aligned}
\Phi_1 &= \begin{bmatrix} 2-3 & 4-3 & 4-3 & 2-3 \end{bmatrix} = \begin{bmatrix} -1 & 1 & 1 & -1 \end{bmatrix} \\
\Phi_2 &= \begin{bmatrix} 4-3 & 2-3 & 2-3 & 4-3 \end{bmatrix} = \begin{bmatrix} 1 & -1 & -1 & 1 \end{bmatrix} \\
\Phi_3 &= \begin{bmatrix} 3-3 & 3-3 & 3-3 & 3-3 \end{bmatrix} = \begin{bmatrix} 0 & 0 & 0 & 0 \end{bmatrix}
\end{aligned}$$

Matriks Deviasi Total ($A$):

$$A = \begin{bmatrix} \Phi_1 \\ \Phi_2 \\ \Phi_3 \end{bmatrix} = \begin{bmatrix} -1 & 1 & 1 & -1 \\ 1 & -1 & -1 & 1 \\ 0 & 0 & 0 & 0 \end{bmatrix}$$

## 4. Membangun Eigenspace (Matriks Kovarian)

Matriks Kovarian ($C$) dihitung melalui rumus $C = A^T \cdot A$:

$$C = \begin{bmatrix} -1 & 1 & 0 \\ 1 & -1 & 0 \\ 1 & -1 & 0 \\ -1 & 1 & 0 \end{bmatrix} \begin{bmatrix} -1 & 1 & 1 & -1 \\ 1 & -1 & -1 & 1 \\ 0 & 0 & 0 & 0 \end{bmatrix} = \begin{bmatrix} 2 & -2 & -2 & 2 \\ -2 & 2 & 2 & -2 \\ -2 & 2 & 2 & -2 \\ 2 & -2 & -2 & 2 \end{bmatrix}$$

Dari matriks $C$ di atas, diperoleh Vektor Eigen Utama (Eigenface) setelah dinormalisasi:

$$u_1 = \begin{bmatrix} 0.5 & -0.5 & -0.5 & 0.5 \end{bmatrix}$$

## 5. Proyeksi Wajah Training (Menghitung Bobot / Weights)

Setiap wajah training diproyeksikan ke Eigenface ($u_1$) untuk mendapatkan bobot ($W_i = \Phi_i \cdot u_1^T$):

$$\begin{aligned}
W_1 &= \begin{bmatrix} -1 & 1 & 1 & -1 \end{bmatrix} \cdot \begin{bmatrix} 0.5 \\ -0.5 \\ -0.5 \\ 0.5 \end{bmatrix} = (-0.5) + (-0.5) + (-0.5) + (-0.5) = -2 \\
W_2 &= \begin{bmatrix} 1 & -1 & -1 & 1 \end{bmatrix} \cdot \begin{bmatrix} 0.5 \\ -0.5 \\ -0.5 \\ 0.5 \end{bmatrix} = 0.5 + 0.5 + 0.5 + 0.5 = 2 \\
W_3 &= \begin{bmatrix} 0 & 0 & 0 & 0 \end{bmatrix} \cdot \begin{bmatrix} 0.5 \\ -0.5 \\ -0.5 \\ 0.5 \end{bmatrix} = 0
\end{aligned}$$

## 6. Pengenalan Wajah Baru (Testing)

Misalkan ada input gambar wajah baru:

$$\Gamma_{\text{baru}} = \begin{bmatrix} 1 & 5 & 5 & 1 \end{bmatrix}$$

### Langkah 1: Normalisasi Wajah Baru
$$\Phi_{\text{baru}} = \Gamma_{\text{baru}} - \Psi = \begin{bmatrix} 1-3 & 5-3 & 5-3 & 1-3 \end{bmatrix} = \begin{bmatrix} -2 & 2 & 2 & -2 \end{bmatrix}$$

### Langkah 2: Proyeksikan ke Eigenspace
$$W_{\text{baru}} = \Phi_{\text{baru}} \cdot u_1^T = \begin{bmatrix} -2 & 2 & 2 & -2 \end{bmatrix} \cdot \begin{bmatrix} 0.5 \\ -0.5 \\ -0.5 \\ 0.5 \end{bmatrix} = -1 - 1 - 1 - 1 = -4$$

### Langkah 3: Hitung Jarak Euclidean dengan Wajah Training
$$\begin{aligned}
d(\text{baru}, \Gamma_1) &= |W_{\text{baru}} - W_1| = |-4 - (-2)| = 2 \\
d(\text{baru}, \Gamma_2) &= |W_{\text{baru}} - W_2| = |-4 - 2| = 6 \\
d(\text{baru}, \Gamma_3) &= |W_{\text{baru}} - W_3| = |-4 - 0| = 4
\end{aligned}$$

### Hasil Akhir
Jarak terkecil adalah $2$ yang merujuk pada **$\Gamma_1$**. Maka, sistem memutuskan bahwa input wajah baru paling mirip dengan **Wajah 1 (Andi)**.