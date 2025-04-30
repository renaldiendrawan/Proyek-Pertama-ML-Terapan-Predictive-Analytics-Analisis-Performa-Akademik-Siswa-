# 📘 Laporan Proyek Machine Learning - Analisis Performa Akademik Siswa

## 🧠 Domain Proyek

Dalam dunia pendidikan, pemahaman terhadap faktor-faktor yang memengaruhi performa siswa sangat penting untuk meningkatkan kualitas pembelajaran. Banyak lembaga pendidikan kini memanfaatkan data untuk membuat keputusan berbasis bukti, termasuk dalam hal prediksi hasil belajar siswa.

**Manfaat proyek ini:**
- Menentukan intervensi akademik lebih awal.
- Menyusun program pembelajaran yang lebih personal.
- Meningkatkan tingkat kelulusan siswa.

---

## 🎯 Business Understanding

### Problem Statements
1. Bagaimana cara memprediksi apakah seorang siswa akan lulus mata pelajaran matematika, membaca, dan menulis?
2. Fitur demografis dan sosial apa yang paling memengaruhi performa akademik siswa?

### Goals
1. Mengembangkan model klasifikasi untuk memprediksi kelulusan siswa pada tiga mata pelajaran utama.
2. Mengidentifikasi fitur-fitur yang paling memengaruhi nilai siswa dengan pendekatan regresi.

### Solution Statements
- Menggunakan Logistic Regression untuk klasifikasi kelulusan siswa.
- Menggunakan Linear Regression untuk memprediksi skor nilai dan menganalisis kontribusi fitur.
- Metrik evaluasi yang digunakan:  
  - **Klasifikasi**: Accuracy, Precision, Recall, F1-Score  
  - **Regresi**: RMSE

---

## 📊 Data Understanding

- **Sumber data**: [Kaggle - Students Performance](https://www.kaggle.com/datasets/spscientist/students-performance-in-exams)
- **Jumlah data**: 1000 baris, 8 kolom (fitur asli), dengan penambahan fitur klasifikasi.
- **Kondisi data**:
  - Tidak ada missing value
  - Tidak ada data duplikat
  - Skor dibatasi antara 0–100 (tidak ada outlier ekstrem)

### Fitur:
- `gender`: jenis kelamin siswa  
- `race/ethnicity`: kelompok etnis  
- `parental level of education`: pendidikan terakhir orang tua  
- `lunch`: status subsidi makan siang  
- `test preparation course`: apakah mengikuti pelatihan ujian  
- `math score`, `reading score`, `writing score`: nilai ujian siswa

---

## 🧹 Data Preparation

1. Menambahkan kolom target klasifikasi kelulusan (`math_pass`, `reading_pass`, `writing_pass`) berdasarkan threshold nilai ≥ 65.
2. Melakukan label encoding pada fitur kategorikal: `gender`, `race/ethnicity`, `parental level of education`, `lunch`, `test preparation course`.
3. Menentukan fitur prediktor (`X`) dengan menghapus kolom nilai asli dan label kelulusan.
4. Melakukan pembagian data (train-test split) secara terpisah:
   - Untuk klasifikasi (`math_pass`, `reading_pass`, `writing_pass`)
   - Untuk regresi (`math score`, `reading score`, `writing score`)
   - Rasio pembagian: 80:20 dengan `random_state=42`

---

## 🤖 Modeling

### Model 1: Logistic Regression (Klasifikasi)
- **Cara kerja**: Mengestimasi probabilitas kelulusan berdasarkan fungsi logit.
- **Parameter**: `max_iter=1000`
- **Output**: Prediksi kelulusan (1 = lulus, 0 = tidak lulus) untuk setiap mata pelajaran.

### Model 2: Linear Regression (Regresi)
- **Cara kerja**: Mencari hubungan linier antara fitur dan skor ujian.
- **Parameter**: Default
- **Output**: Prediksi nilai numerik untuk matematika, membaca, dan menulis.

---

## ✅ Evaluation

### Klasifikasi
**Metrik yang digunakan**:  
- **Accuracy**: Mengukur seberapa banyak prediksi yang benar dari seluruh data.  
- **Precision**: Ketepatan model dalam memprediksi kelulusan.  
- **Recall**: Kemampuan model dalam mendeteksi siswa yang benar-benar lulus.  
- **F1-score**: Rata-rata harmonis dari precision dan recall.

**Hasil Evaluasi Model Klasifikasi:**

- **Matematika**
  - Accuracy: **0.655**
  - Precision: **0.648**
  - Recall: **0.764**
  - F1 Score: **0.701**

- **Membaca**
  - Accuracy: **0.620**
  - Precision: **0.649**
  - Recall: **0.810**
  - F1 Score: **0.721**

- **Menulis**
  - Accuracy: **0.670**
  - Precision: **0.684**
  - Recall: **0.802**
  - F1 Score: **0.738**

> Hasil ini menunjukkan bahwa model cukup efektif dalam mendeteksi siswa yang akan lulus, terutama dengan recall tinggi di semua mata pelajaran.

---

### Regresi
**Metrik yang digunakan**:  
- **RMSE (Root Mean Squared Error)**: Mengukur rata-rata kesalahan prediksi terhadap nilai aktual. Semakin kecil nilai RMSE, semakin akurat model.

**Hasil Evaluasi Model Regresi:**

- **Matematika**: RMSE **14.24**
- **Membaca**: RMSE **14.02**
- **Menulis**: RMSE **13.88**

> Model regresi memiliki performa yang moderat, dengan tingkat kesalahan prediksi berada di kisaran 13–14 poin.

---

### 🎯 Kesimpulan

Berdasarkan hasil evaluasi:

- Model klasifikasi menunjukkan performa cukup baik dengan F1-score > 0.70 untuk semua mata pelajaran, menandakan efektivitas model dalam mengidentifikasi siswa yang akan lulus.
- Meskipun RMSE pada model regresi cukup tinggi (sekitar 14), model masih mampu memberikan estimasi kasar terhadap nilai ujian siswa.

**Kesimpulan terhadap Business Understanding:**
- **Problem statement pertama** telah dijawab dengan baik: model klasifikasi mampu memprediksi kelulusan siswa dengan cukup akurat.
- **Problem statement kedua** didukung oleh model regresi yang memungkinkan analisis lebih dalam terhadap pengaruh fitur terhadap nilai.

Model yang dibangun berpotensi besar digunakan sebagai dasar dalam:
- Menentukan intervensi akademik awal bagi siswa yang diprediksi tidak lulus.
- Menyusun strategi pengajaran personal sesuai prediksi performa siswa.
