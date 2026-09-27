<h1 align="center">Customer Segmentation & Real-Time Classification Inference Engine</h1>

<p align="center">
  <b>End-to-End Machine Learning Pipeline: Unsupervised K-Means + Inverse Transformation + Supervised Classification Engine</b>
</p>

<br>

---

<br>

<h2>📌 Problem Statement & Workflow</h2>

Mengalokasikan nasabah baru ke dalam kelompok segmen secara manual atau dengan menghitung ulang algoritma K-Means (*re-clustering*) dari awal membutuhkan daya komputasi yang besar dan berisiko menggeser titik pusat kelompok (*centroid*) yang sudah terbentuk.

Proyek ini mengatasi masalah tersebut dengan menggabungkan **Unsupervised Learning** dan **Supervised Learning**:

* <b>Unsupervised Learning (K-Means):</b> Mengelompokkan data historis transaksi nasabah secara otomatis dan menghasilkan label kelompok (<code>Target</code>).
* <b>Inverse Transformation:</b> Mengembalikan data ter-scale ke unit asli (seperti nominal Rupiah, usia tahun, dan profesi) untuk interpretasi bisnis.
* <b>Supervised Learning (Classification):</b> Melatih model untuk mempelajari garis batas matematika K-Means sebagai <i>inference engine</i> otomatis untuk memprediksi segmen nasabah baru secara <i>real-time</i>.

<br>
<br>

<h2>🛠️ Alur Kerja Proyek (Pipeline)</h2>

<pre>
[ Raw Data ] ──► [ Preprocessing & Scaling ] ──► [ K-Means Clustering ]
                                                         │
                                                         ▼
[ Hyperparameter Tuning ] ◄── [ Supervised Model ] ◄── [ Inverse Scaling & Profiling ]
</pre>

<br>

1. <b>Preprocessing & Feature Scaling:</b> Normalisasi data numerik menggunakan <code>StandardScaler</code> dan variabel kategorikal menggunakan <code>LabelEncoder</code>.
2. <b>K-Means Clustering:</b> Membagi dataset menjadi 2 kluster utama (<code>Cluster 0</code> dan <code>Cluster 1</code>).
3. <b>Inverse Transformation:</b> Mengembalikan nilai ter-scale ke skala asli (Rupiah/Dolar, usia, profesi) untuk analisis karakteristik bisnis.
4. <b>Data Encoding & Train-Test Split:</b> Penerapan <i>One-Hot Encoding</i> dan pembagian data latih (80%) dan data uji (20%) menggunakan <i>stratified sampling</i>.
5. <b>Supervised Modeling:</b> Melatih model <i>Decision Tree</i> dan <i>Random Forest Classifier</i> untuk mempelajari aturan pembentukan kluster.
6. <b>Hyperparameter Tuning:</b> Optimasi parameter model menggunakan <code>GridSearchCV</code> (<code>n_estimators</code>, <code>max_depth</code>, <code>min_samples_split</code>).

<br>
<br>

<h2>📊 Ringkasan Profil Kluster (Inverse Analysis)</h2>

Berdasarkan analisis nilai riil setelah *inverse transformation*, diperoleh profil utama dari setiap kelompok nasabah:

<br>

| Fitur / Karakteristik | Cluster 0 (Mapan / Profesional) | Cluster 1 (Muda / Pelajar) |
| :--- | :--- | :--- |
| **Rata-rata Usia** | ~45 Tahun (*Sedang*) | ~44 Tahun (*Muda*) |
| **Pekerjaan Dominan** | Dokter (*Doctor*) | Pelajar / Mahasiswa (*Student*) |
| **Rata-rata Saldo** | $5.142,17 | $5.058,81 |
| **Nilai Transaksi Rata-rata** | $255,55 | $258,15 |
| **Lokasi & Saluran** | Charlotte, Kantor Cabang | Tucson, Kantor Cabang |

<br>
<br>

<h2>🚀 Hasil Evaluasi Model Klasifikasi</h2>

Model klasifikasi dievaluasi pada data uji (*test set*) menggunakan metrik *Accuracy*, *Precision*, *Recall*, dan *F1-Score*:

<br>

```text
               precision    recall  f1-score   support

    Cluster 0       1.00      1.00      1.00       196
    Cluster 1       1.00      1.00      1.00       193

     accuracy                           1.00       389
    macro avg       1.00      1.00      1.00       389
 weighted avg       1.00      1.00      1.00       389
