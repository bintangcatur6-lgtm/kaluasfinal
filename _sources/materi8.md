# Dokumentasi Cara Kerja Program Face Recognition dengan SVD / Eigenfaces

## File Program

`pengenalan copy.py`

---

# 1. Tujuan Program

Program ini digunakan untuk melakukan **pengenalan wajah (face recognition)** menggunakan metode:

- Singular Value Decomposition (SVD)
- Eigenfaces
- Euclidean Distance

Secara sederhana:

1. Gambar wajah dibaca
2. Diubah menjadi angka/matriks
3. Direduksi dimensinya menggunakan SVD
4. Dibandingkan tingkat kemiripannya
5. Dipilih wajah paling mirip

Karena manusia rupanya suka mengubah wajah menjadi ribuan angka lalu memaksa matriks mencari identitas seseorang. Dunia benar-benar memberi aljabar linear pekerjaan yang aneh.

---

# 2. Library yang Harus Diinstall

Program membutuhkan beberapa library Python.

## Install Python

Gunakan:

- Python 3.10+
- Disarankan Python 3.11 atau 3.12

Cek versi:

```bash
python --version
```

### Install Dependensi

Jalankan:

```bash
pip install numpy pillow
```

### Library yang digunakan:

| Library    | Fungsi                       |
| ---------- | ---------------------------- |
| `numpy`    | Operasi matriks dan SVD      |
| `Pillow`   | Membaca dan memproses gambar |
| `argparse` | Membaca argumen terminal     |
| `math`     | Operasi matematika           |
| `tempfile` | Membuat dataset demo         |
| `pathlib`  | Mengelola path file/folder   |

---

### struktur dataset

```
dataset/
│
├── train/
│ ├── face1/
│ │ ├── img1.jpg
│ │ ├── img2.jpg
│ │
│ ├── face2/
│ ├── foto1.jpg
│ ├── foto2.jpg
│
└── test.jpg
```

### Penjelasan:

Folder train berisi data training

Setiap subfolder dianggap 1 orang

Nama folder menjadi label identitas

test.jpg adalah gambar yang ingin dikenali

### 4. Cara Menjalankan Program

Menjalankan Dataset Asli

```bash
python "pengenalan copy.py" --train dataset/train --test dataset/test.jpg --size 64x64
```

### Menjalankan Mode Demo

```bash
python "pengenalan copy.py" --demo
```

### Mode demo akan:

membuat dataset wajah palsu otomatis

menjalankan SVD

melakukan pengenalan wajah

---

Jadi bahkan kalau belum punya dataset asli, program tetap bisa diuji. Komputer membuat wajah sintetis untuk membuktikan matematika bekerja. Sedikit menyeramkan kalau dipikir terlalu lama.

### 5. Alur Besar Program

Secara umum program bekerja seperti ini:

```text
Load gambar
↓
Ubah grayscale
↓
Resize gambar
↓
Flatten menjadi vektor
↓
Gabungkan menjadi matriks X
↓
Hitung mean face
↓
Centering data
↓
Lakukan SVD
↓
Ambil eigenface
↓
Proyeksikan wajah
↓
Hitung jarak Euclidean
↓
Pilih wajah paling mirip
```

### 6. Penjelasan Step-by-Step Pengolahan Data

STEP 1 — Membaca Dataset

Fungsi:

```bash
load_training_images()
```

### Kode utama:

```python
for person_dir in sorted(path for path in train_dir.iterdir() if path.is_dir()):
```

### Yang terjadi:

Program membuka folder training

Membaca semua subfolder

Nama subfolder dianggap label orang

Semua gambar di dalamnya dimuat

### Contoh:

```text
train/
 ├── face1/
 ├── face2/
```

### Maka:

label face1

label face2

### STEP 2 — Membaca Gambar

### Fungsi:

```bash
load_grayscale_image()
```

### Kode:

```python
image = Image.open(path).convert("L").resize(size)
```

### Yang dilakukan:

### a. Membuka gambar

```bash
Image.open(path)
```

### Gambar dibaca dari file.

### b. Mengubah ke grayscale

```bash
.convert("L")
```

### Gambar RGB:

```text
Merah Hijau Biru
```

### diubah menjadi:

```text
1 channel abu-abu
```

### Tujuannya:

- komputasi lebih ringan

- lebih mudah diproses matriks

Karena SVD tidak peduli warna kulit, hanya pola intensitas cahaya.

### c. Resize gambar

```bash
.resize(size)
Semua gambar harus sama ukuran.
```

### Contoh:

```text
64 x 64
```

Kenapa penting?
Karena matriks harus punya dimensi sama.

Kalau satu gambar 64x64 dan lainnya 300x500, SVD akan protes secara matematis. Dan untuk sekali ini, protesnya valid.

### STEP 3 — Mengubah Gambar Menjadi Matriks

Kode:

```python
matrix = np.asarray(image, dtype=np.float64) / 255.0
```

hasilnya

```text
[[0.1 0.2 0.3]
 [0.5 0.8 0.1]]
```

Setiap piksel menjadi angka antara:

- $\rightarrow$ hitam1
- $\rightarrow$ putih

### STEP 4 — Flatten Menjadi Vektor

Kode:

```python
vector = matrix.reshape(-1, 1)
```

### Contoh Matriks:

```text
[[1 2]
 [3 4]]
```

Menjadi Vektor Kolom:
$$\begin{bmatrix} 1 \\ 2 \\ 3 \\ 4 \end{bmatrix}$$

Kenapa dilakukan?
Karena algoritma SVD bekerja pada bentuk vektor.

### STEP 5 — Membentuk Matriks Training X

Kode:

```python
x_matrix = np.hstack(vectors)
```

Semua vektor digabung:
$$X = [x_1 \quad x_2 \quad x_3 \quad \dots \quad x_n]$$Contoh susunan kolom:$$\begin{bmatrix} 1 & 4 & 7 \\ 2 & 5 & 8 \\ 3 & 6 & 9 \end{bmatrix}$$
Makna:

- setiap kolom = 1 wajah
- setiap baris = nilai piksel tertentu

### STEP 6 — Menghitung Mean Face

Kode:

```python
mean_face = np.mean(x_matrix, axis=1, keepdims=True)
```

Program menghitung wajah rata-rata.

Secara matematis:

$$\mu = \text{rata-rata seluruh wajah}$$

Hasilnya disebut mean face. Ini penting karena algoritma ingin mencari perbedaan wajah terhadap wajah rata-rata.

### STEP 7 — Centering Data

Kode:

```python
centered_matrix = x_matrix - mean_face
```

Artinya: Setiap gambar dikurangi wajah rata-rata.

Kenapa? Karena PCA/SVD bekerja lebih baik jika data dipusatkan terhadap mean. Kalau tidak dicenter, variasi data sulit dianalisis dan eigenface kurang representatif.

### STEP 8 — Singular Value Decomposition (SVD)

Kode:

```python
u_matrix, singular_values, vt_matrix = np.linalg.svd(centered_matrix)
```

Inilah inti program.
Rumus:
$$A = U \Sigma V^T$$

### Penjelasan komponen matriks hasil dekomposisi:

| matriks  | Fungsi                 |
| -------- | ---------------------- |
| $U$      | Basis fitur wajah      |
| $\Sigma$ | Besarnya informasi     |
| $V^T$    | Koefisien transformasi |

### Apa itu Eigenface?

Kolom pada matriks $U$ disebut eigenface.Eigenface adalah pola wajah utama yang ditemukan sistem. Bukan wajah manusia normal. Lebih seperti mimpi buruk statistik abu-abu hasil kompresi matematika.

### STEP 9 — Memilih Komponen Penting

Kode:

```python
u_k = u_matrix[:, :component_count]
```

Program hanya mengambil beberapa komponen terbaik.

Kenapa? Karena komponen besar melambangkan informasi penting, sedangkan komponen kecil melambangkan noise.

Tujuannya adalah reduksi dimensi:

```text
4096 piksel  ↓  20 fitur penting
```

### STEP 10 — Proyeksi Wajah Training

Kode:

```python
train_weights = u_k.T @ centered_matrix
```

Artinya: Semua wajah training diproyeksikan ke ruang eigenface.

Hasilnya, setiap wajah berubah menjadi bobot fitur murni.

### STEP 11 — Memproses Wajah Test

Kode:

```python
test_centered = test_image.vector - mean_face
```

lalu

```python
test_weights = u_k.T @ test_centered
```

Artinya:

Gambar test dikurangi mean face.

Hasilnya diproyeksikan ke ruang eigenface.

### STEP 12 — Menghitung Jarak

Kode:

```python
distance = np.linalg.norm(test_weights - train_weights[:, [index]])
```

Program menghitung jarak Euclidean. Semakin kecil nilai jaraknya, berarti semakin mirip wajahnya.

### STEP 13 — Menentukan Prediksi

Kode:

```python
distances.sort(key=lambda row: row[2])
```

Program mencari jarak terkecil.

Contoh urutan data:

| Label | Jarak |
| ----- | ----- |
| face1 | 0.21  |
| face2 | 1.90  |

Maka kesimpulannya, objek test.jpg jauh lebih mirip dengan face1.

### STEP 14 — Threshold

Kode:

```python
accepted = nearest_distance <= computed_threshold
```

Threshold digunakan untuk menentukan apakah wajah dikenali atau tidak. Kalau jaraknya terlalu besar, output yang keluar adalah UNKNOWN.

Karena sistem sadar dia tidak tahu siapa orang itu. Langkah langka dalam sejarah teknologi.

### 7. Visualisasi yang Dihasilkan

Program juga membuat beberapa gambar analisis:

Mean Face: Rata-rata dari semua wajah sampel.

Centered Face: Tampilan wajah setelah dikurangi komponen mean.

Eigenface: Pola fitur utama wajah hasil dekomposisi SVD.

Reconstruction: Hasil wajah yang disusun kembali dari komponen eigenface.

Error Image: Selisih atau perbedaan antara wajah asli dengan hasil rekonstruksi.

### 8. Penjelasan Fungsi Penting

- parse_size(): Mengubah string input "64x64" menjadi format tuple (64, 64).
- image_paths(): Mencari dan mendaftar semua file gambar di direktori.
- normalize_to_uint8(): Mengubah nilai matriks kembali agar bisa divisualisasikan menjadi citra standar.- matrix_to_image(): Mengonversi array matriks menjadi objek gambar utuh.
- save_grid(): Menggabungkan banyak gambar analisis menjadi satu grid gambar komposit.
- choose_threshold(): Menghitung batas toleransi threshold otomatis berdasarkan sebaran data training.
- recognize_with_svd(): Fungsi inti seluruh algoritma, di mana semua pemrosesan utama terjadi di sini.

### 9. Rumus Penting yang Dipakai

#### Mean Face

$$\mu = \text{rata-rata seluruh wajah}$$

#### Centering

$$A = X - \mu$$

#### SVD

$$A = U \Sigma V^T$$

#### Proyeksi Eigenface

$$W = U^T A$$Euclidean Distance$$d = \|x - y\|$$

### 10. Output Program

Program menghasilkan dua komponen keluaran utama:

- File laporan (laporan_svd.txt): Berisi salinan matriks, nilai singular, hasil prediksi, bobot jarak, dan komponen eigenface.

- Folder visualisasi (hasil_analisis_svd/): Berisi berkas gambar mean face, eigenface, grafik perkembangan singular value, hingga visualisasi reconstruction.

### 11. Kesimpulan Cara Kerja Program

Secara singkat:

1. Gambar diubah menjadi angka.

2. Angka diproses menjadi matriks.

3. SVD mencari pola utama wajah (eigenfaces).

4. Wajah diproyeksikan ke ruang fitur rendah.

5. Jarak spasial dihitung.

6. Wajah terdekat dipilih sebagai hasil pengenalan.

Program ini sebenarnya adalah gabungan dari pengolahan citra, aljabar linear, reduksi dimensi, dan klasifikasi sederhana. Menariknya, inti pengenalan wajah di sini bukan AI modern berat miliaran parameter, tapi matematika klasik yang sudah ada sejak lama. Kadang solusi elegan memang tidak perlu GPU seharga motor.