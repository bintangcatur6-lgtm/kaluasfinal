# Tugas Eigenface (PCA)

## 1. Representasi Vektor Wajah

Misalkan kita memiliki 3 buah data gambar wajah training yang disederhanakan menjadi vektor baris berukuran $1 \times 4$ piksel:

$$\begin{aligned}
\Gamma_1 &= \begin{bmatrix} 2 & 4 & 4 & 2 \end{bmatrix} \\
\Gamma_2 &= \begin{bmatrix} 4 & 2 & 2 & 4 \end{bmatrix} \\
\Gamma_3 &= \begin{bmatrix} 3 & 3 & 3 & 3 \end{bmatrix}
\end{aligned}$$

## 2. Menghitung Rata-Rata Wajah (Mean Face)

Wajah rata-rata ($\Psi$) dihitung dengan menjumlahkan seluruh vektor wajah training lalu dibagi dengan jumlah total sampel ($M=3$):

$$\Psi = \frac{1}{3} \sum_{i=1}^{3} \Gamma_i$$

$$\Psi = \frac{1}{3} \left( \begin{bmatrix} 2 & 4 & 4 & 2 \end{bmatrix} + \begin{bmatrix} 4 & 2 & 2 & 4 \end{bmatrix} + \begin{bmatrix} 3 & 3 & 3 & 3 \end{bmatrix} \right)$$

$$\Psi = \begin{bmatrix} 3 & 3 & 3 & 3 \end{bmatrix}$$

## 3. Normalisasi Selisih Wajah ($\Phi$)

Setiap vektor wajah dikurangi dengan vektor wajah rata-rata ($\Phi_i = \Gamma_i - \Psi$) untuk mendapatkan fitur unik:

$$\begin{aligned}
\Phi_1 &= \begin{bmatrix} 2-3 & 4-3 & 4-3 & 2-3 \end{bmatrix} = \begin{bmatrix} -1 & 1 & 1 & -1 \end{bmatrix} \\
\Phi_2 &= \begin{bmatrix} 4-3 & 2-3 & 2-3 & 4-3 \end{bmatrix} = \begin{bmatrix} 1 & -1 & -1 & 1 \end{bmatrix} \\
\Phi_3 &= \begin{bmatrix} 3-3 & 3-3 & 3-3 & 3-3 \end{bmatrix} = \begin{bmatrix} 0 & 0 & 0 & 0 \end{bmatrix}
\end{aligned}$$

Matriks Deviasi Data ($A$):

$$A = \begin{bmatrix} \Phi_1 \\ \Phi_2 \\ \Phi_3 \end{bmatrix} = \begin{bmatrix} -1 & 1 & 1 & -1 \\ 1 & -1 & -1 & 1 \\ 0 & 0 & 0 & 0 \end{bmatrix}$$

## 4. Pembentukan Matriks Kovarian ($C$)

Matriks Kovarian dihitung menggunakan perkalian matriks deviasi transpose dengan matriks deviasi itu sendiri ($C = A^T \cdot A$):

$$C = \begin{bmatrix} -1 & 1 & 0 \\ 1 & -1 & 0 \\ 1 & -1 & 0 \\ -1 & 1 & 0 \end{bmatrix} \begin{bmatrix} -1 & 1 & 1 & -1 \\ 1 & -1 & -1 & 1 \\ 0 & 0 & 0 & 0 \end{bmatrix} = \begin{bmatrix} 2 & -2 & -2 & 2 \\ -2 & 2 & 2 & -2 \\ -2 & 2 & 2 & -2 \\ 2 & -2 & -2 & 2 \end{bmatrix}$$

Dari matriks kovarian $C$, kita dapatkan Vektor Eigen Utama (**Eigenface**) setelah dinormalisasi:

$$u_1 = \begin{bmatrix} 0.5 & -0.5 & -0.5 & 0.5 \end{bmatrix}$$

## 5. Proyeksi dan Perhitungan Bobot Wajah Training

Setiap wajah training diproyeksikan ke dalam ruang eigen dengan mengalikan vektor $\Phi_i$ terhadap Transpose Eigenface ($W_i = \Phi_i \cdot u_1^T$):

$$\begin{aligned}
W_1 &= \begin{bmatrix} -1 & 1 & 1 & -1 \end{bmatrix} \cdot \begin{bmatrix} 0.5 \\ -0.5 \\ -0.5 \\ 0.5 \end{bmatrix} = -2 \\
W_2 &= \begin{bmatrix} 1 & -1 & -1 & 1 \end{bmatrix} \cdot \begin{bmatrix} 0.5 \\ -0.5 \\ -0.5 \\ 0.5 \end{bmatrix} = 2 \\
W_3 &= \begin{bmatrix} 0 & 0 & 0 & 0 \end{bmatrix} \cdot \begin{bmatrix} 0.5 \\ -0.5 \\ -0.5 \\ 0.5 \end{bmatrix} = 0
\end{aligned}$$

## 6. Pengujian Wajah Baru (Testing)

Diberikan sebuah input vektor wajah baru yang ingin diidentifikasi:

$$\Gamma_{\text{baru}} = \begin{bmatrix} 1 & 5 & 5 & 1 \end{bmatrix}$$

### Langkah A: Normalisasi Wajah Baru
$$\Phi_{\text{baru}} = \Gamma_{\text{baru}} - \Psi = \begin{bmatrix} 1-3 & 5-3 & 5-3 & 1-3 \end{bmatrix} = \begin{bmatrix} -2 & 2 & 2 & -2 \end{bmatrix}$$

### Langkah B: Proyeksi ke Eigenspace
$$W_{\text{baru}} = \Phi_{\text{baru}} \cdot u_1^T = \begin{bmatrix} -2 & 2 & 2 & -2 \end{bmatrix} \cdot \begin{bmatrix} 0.5 \\ -0.5 \\ -0.5 \\ 0.5 \end{bmatrix} = -4$$

### Langkah C: Perhitungan Jarak Euclidean
Selisih bobot wajah baru dengan setiap wajah training:

$$\begin{aligned}
d(\text{baru}, \Gamma_1) &= |W_{\text{baru}} - W_1| = |-4 - (-2)| = 2 \\
d(\text{baru}, \Gamma_2) &= |W_{\text{baru}} - W_2| = |-4 - 2| = 6 \\
d(\text{baru}, \Gamma_3) &= |W_{\text{baru}} - W_3| = |-4 - 0| = 4
\end{aligned}$$

## 7. Visualisasi Hasil Gambar Wajah

Untuk melihat bagaimana representasi matriks angka di atas jika diubah menjadi visualisasi gambar grayscale (skala abu-abu), kita dapat menggunakan kode Python berikut (bisa dijalankan di `notebooks.ipynb` atau skrip lokal):

```python
import numpy as np
import matplotlib.pyplot as plt

# 1. Definisikan ulang matriks wajah (di-reshape dari 1x4 menjadi 2x2)
wajah_1 = np.array([[2, 4], [4, 2]])
wajah_2 = np.array([[4, 2], [2, 4]])
wajah_3 = np.array([[3, 3], [3, 3]])
wajah_baru = np.array([[1, 5], [5, 1]])
mean_face = np.array([[3, 3], [3, 3]])
eigenface = np.array([[0.5, -0.5], [-0.5, 0.5]])

# 2. Setup Plot Visualisasi
fig, axes = plt.subplots(2, 3, figsize=(10, 6))
fig.suptitle('Visualisasi Grid Wajah (2x2 Piksel)', fontsize=14, fontweight='bold')

# Wajah Training
axes[0, 0].imshow(wajah_1, cmap='gray', vmin=0, vmax=5)
axes[0, 0].set_title('Wajah 1 ($\Gamma_1$)')
axes[0, 0].axis('off')

axes[0, 1].imshow(wajah_2, cmap='gray', vmin=0, vmax=5)
axes[0, 1].set_title('Wajah 2 ($\Gamma_2$)')
axes[0, 1].axis('off')

axes[0, 2].imshow(wajah_3, cmap='gray', vmin=0, vmax=5)
axes[0, 2].set_title('Wajah 3 ($\Gamma_3$)')
axes[0, 2].axis('off')

# Fitur dan Testing
axes[1, 0].imshow(mean_face, cmap='gray', vmin=0, vmax=5)
axes[1, 0].set_title('Wajah Rata-rata ($\Psi$)')
axes[1, 0].axis('off')

axes[1, 1].imshow(eigenface, cmap='coolwarm') # Menggunakan coolwarm untuk melihat nilai negatif/positif
axes[1, 1].set_title('Eigenface ($u_1$)')
axes[1, 1].axis('off')

axes[1, 2].imshow(wajah_baru, cmap='gray', vmin=0, vmax=5)
axes[1, 2].set_title('Wajah Baru (Input)')
axes[1, 2].axis('off')

plt.tight_layout()
plt.show()

### Kesimpulan Akhir
Berdasarkan nilai jarak terkecil ($d = 2$), sistem memutuskan bahwa input wajah baru memiliki kemiripan paling dekat dengan **Wajah Training 1 ($\Gamma_1$)**.