# Eigenface

## ## Pengenalan Wajah dengan Metode Eigenfaces (PCA)

Metode **Eigenfaces** adalah salah satu pendekatan klasik paling populer dalam pengenalan wajah yang berbasis pada teknik statistik bernama **Principal Component Analysis (PCA)**. 

Secara umum, metode ini bekerja dengan cara mereduksi dimensi gambar wajah yang tinggi (ribuan piksel) menjadi ruang dimensi yang lebih rendah yang disebut **Eigenspace** (ruang eigen) tanpa kehilangan karakteristik penting dari wajah tersebut.

---

### Alur Kerja Algoritma Eigenfaces

Proses pengenalan wajah baru melalui alur matematis dan komputasi sebagai berikut:

#### 1. Preprocessing Data Training
* Setiap gambar wajah training berukuran $M \times N$ piksel diubah (*flatten*) menjadi sebuah vektor satu dimensi berukuran $D \times 1$, di mana $D = M \times N$.
* Seluruh vektor wajah digabungkan ke dalam sebuah matriks data wajah.

#### 2. Menghitung Wajah Rata-Rata (Mean Face)
Sistem menghitung rata-rata dari seluruh wajah training menggunakan rumus:
$$\Psi = \frac{1}{M} \sum_{i=1}^{M} \Gamma_i$$

Di mana $\Gamma_i$ adalah vektor wajah ke-$i$, dan $M$ adalah total gambar training.

#### 3. Normalisasi Wajah (Mencari Deviasi)
Setiap wajah training dikurangi dengan wajah rata-rata untuk menyisakan fitur-fitur pembeda yang unik saja:
$$\Phi_i = \Gamma_i - \Psi$$

#### 4. Membangun Eigenspace (Matriks Kovarian & Eigenvectors)
* Menghitung matriks kovarian dari data yang telah dinormalisasi untuk melihat korelasi antar piksel.
* Dari matriks kovarian tersebut, dicari nilai eigen (*eigenvalues*) dan vektor eigen (*eigenvectors*).
* Vektor eigen yang memiliki nilai varians terbesar dipilih sebagai komponen utama. Vektor inilah yang disebut sebagai **Eigenfaces** (Wajah Eigen).

#### 5. Proyeksi dan Pencocokan Wajah Baru
Ketika ada input wajah baru ($\Gamma_{\text{baru}}$) masuk ke sistem:
1. **Normalisasi:** Wajah baru dikurangi wajah rata-rata training $\Phi_{\text{baru}} = \Gamma_{\text{baru}} - \Psi$.
2. **Proyeksi:** Vektor $\Phi_{\text{baru}}$ dikalikan dengan matriks Eigenfaces untuk mendapatkan bobot atau koordinatnya di dalam *Eigenspace*.
3. **Pencocokan:** Koordinat wajah baru ini dibandingkan dengan seluruh koordinat wajah training menggunakan perhitungan jarak **Euclidean Distance**.
4. **Hasil:** Wajah training yang memiliki jarak paling dekat (*minimum distance*) dinyatakan sebagai identitas orang yang paling mirip.

---

### Contoh Implementasi Sederhana dengan Python

Jika Anda ingin mencoba simulasinya menggunakan Python (bisa diterapkan pada file `notebooks.ipynb`), berikut adalah potongan kode dasarnya:

```python
import numpy as np
from sklearn.decomposition import PCA
from sklearn.metrics.pairwise import euclidean_distances

# 1. Simulasi Data Gambar Wajah (Ukuran 100x100 piksel = 10.000 fitur)
# Misal ada 3 sampel wajah training
X_train = np.random.rand(3, 10000) 
labels = ["Andi", "Budi", "Cici"]

# 2. Proses Training: Membangun Eigenspace dengan PCA
pca = PCA(n_components=2, whiten=True).fit(X_train)
X_train_pca = pca.transform(X_train) # Bobot training

# 3. Proses Testing: Input wajah baru
X_new_face = np.random.rand(1, 10000)
X_new_pca = pca.transform(X_new_face) # Proyeksi ke Eigenspace

# 4. Hitung Jarak Terdekat (Euclidean Distance)
distances = euclidean_distances(X_new_pca, X_train_pca)[0]
idx_terdekat = np.argmin(distances)

print(f"Wajah baru paling mirip dengan: {labels[idx_terdekat]} (Jarak: {distances[idx_terdekat]:.4f})")