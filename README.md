
# Bank Customer Persona Analysis

## Deskripsi Dataset
Dataset ini menyajikan gambaran mendalam mengenai perilaku transaksi dan pola aktivitas keuangan, sehingga sangat ideal untuk eksplorasi **Fraud Detection**, **Anomaly Detection**, dan **Customer Segmentation** menggunakan teknik Machine Learning.

Dataset terdiri dari **2.512 data transaksi** yang mencakup informasi transaksi, demografi nasabah, serta pola penggunaan layanan keuangan.

Setiap entri memberikan wawasan komprehensif terhadap perilaku transaksi pengguna yang dapat digunakan untuk:
- Analisis keamanan finansial
- Deteksi aktivitas mencurigakan
- Segmentasi nasabah
- Pengembangan model prediktif
- Clustering perilaku transaksi

---

# Fitur Dataset

| Feature | Deskripsi |
|---|---|
| `TransactionID` | Pengidentifikasi unik alfanumerik untuk setiap transaksi |
| `AccountID` | ID unik akun nasabah |
| `TransactionAmount` | Nilai transaksi |
| `TransactionDate` | Tanggal dan waktu transaksi |
| `TransactionType` | Jenis transaksi (`Credit` / `Debit`) |
| `Location` | Lokasi transaksi (kota di Amerika Serikat) |
| `DeviceID` | ID perangkat yang digunakan |
| `IP Address` | Alamat IPv4 saat transaksi |
| `MerchantID` | ID merchant |
| `AccountBalance` | Saldo rekening setelah transaksi |
| `PreviousTransactionDate` | Waktu transaksi sebelumnya |
| `Channel` | Kanal transaksi (`Online`, `ATM`, `Branch`) |
| `CustomerAge` | Umur nasabah |
| `CustomerOccupation` | Pekerjaan nasabah |
| `TransactionDuration` | Durasi transaksi dalam detik |
| `LoginAttempts` | Jumlah percobaan login sebelum transaksi |

---

# Clustering Modeling

Pada tahap ini dilakukan pembangunan model clustering untuk mengelompokkan data berdasarkan kemiripan karakteristik transaksi nasabah.
Metode yang digunakan:

- K-Means Clustering
- Silhouette Score
- Elbow Method menggunakan KElbowVisualizer

# Menentukan Jumlah Cluster Terbaik

Visualisasi Elbow Method digunakan untuk menentukan jumlah cluster optimal.

<img width="696" height="507" alt="kelbow" src="https://github.com/user-attachments/assets/c95e2926-fa00-4fc1-a5e6-daab400cd97c" />

# PCA Clustering

```
# Buat (instantiate) objek PCA untuk 2 komponen (n_components=2)
pca = PCA(n_components=2)

# Terapkan (fit) PCA ke data 'df' dan transformasikan data tersebut
df_pca = pca.fit_transform(df)

# Buat DataFrame baru 'df_pca' dari hasil transformasi
df_pca = pd.DataFrame(data=df_pca, columns=['Principal Component 1', 'Principal Component 2'])
```

<img width="841" height="704" alt="pca" src="https://github.com/user-attachments/assets/f79f5884-2e59-4b8f-b262-8826a86c054f" />

---

# Hasil Clustering
## Cluster 1
Nasabah Aktivitas Transaksi Sedikit Lebih Tinggi dengan Saldo Stabil
Karakteristik (Data Standardisasi)
- Mean TransactionAmount : -0.01
- Mean CustomerAge : 0.02
- Mean TransactionDuration : 0.03
- Mean AccountBalance : 0.01
## Analisis
Cluster ini berisi nasabah dengan usia relatif sedikit lebih dewasa dibanding rata-rata dataset. Mereka memiliki saldo rekening yang stabil dan aktivitas transaksi yang cukup aktif dengan durasi transaksi sedikit lebih lama dibanding rata-rata.
Nilai transaksi berada di sekitar rata-rata sehingga menunjukkan pola penggunaan layanan perbankan yang normal dan stabil. Nasabah pada cluster ini dapat dianggap sebagai nasabah reguler dengan kondisi finansial yang cukup baik dan konsisten.

## Cluster 2
Nasabah Aktivitas Transaksi Cepat dengan Saldo Sedikit Lebih Rendah
Karakteristik (Data Standardisasi)
- Mean TransactionAmount : 0.01
- Mean CustomerAge : -0.02
- Mean TransactionDuration : -0.03
- Mean AccountBalance : -0.01
## Analisis
Cluster ini terdiri dari nasabah dengan usia relatif lebih muda dibanding cluster lainnya. Mereka memiliki aktivitas transaksi yang sedikit lebih tinggi dengan durasi transaksi lebih cepat.
Saldo rekening mereka sedikit lebih rendah dibanding cluster lain. Pola ini dapat mengindikasikan nasabah yang aktif menggunakan layanan transaksi cepat seperti mobile banking atau pembayaran digital.

# Interpretasi Cluster Setelah Inverse Transform
## Cluster 1
Profesional Mapan dengan Saldo Stabil

| Feature                 | Nilai     |
| ----------------------- | --------- |
| Mean TransactionAmount  | 255.55    |
| Mean CustomerAge        | 45.06     |
| Mean AccountBalance     | 5142.17   |
| Mode TransactionType    | Debit     |
| Mode Location           | Charlotte |
| Mode Channel            | Branch    |
| Mode CustomerOccupation | Doctor    |
| Mode CustomerAgeRange   | Mature    |

## Analisis
Cluster ini kemungkinan terdiri dari nasabah dengan kondisi karier yang lebih mapan. Hal ini terlihat dari dominasi profesi dokter serta kategori usia mature.
Saldo rekening rata-rata lebih tinggi dibanding cluster lainnya yang menunjukkan kestabilan finansial. Aktivitas transaksi dilakukan dalam tingkat sedang dan mayoritas melalui cabang bank (Branch), sehingga menunjukkan kecenderungan penggunaan layanan perbankan konvensional.

## Cluster 2
Nasabah Muda dengan Aktivitas Transaksi Dinamis

| Feature                 | Nilai   |
| ----------------------- | ------- |
| Mean TransactionAmount  | 258.15  |
| Mean CustomerAge        | 44.33   |
| Mean AccountBalance     | 5058.81 |
| Mode TransactionType    | Debit   |
| Mode Location           | Tucson  |
| Mode Channel            | Branch  |
| Mode CustomerOccupation | Student |
| Mode CustomerAgeRange   | Young   |

## Analisis
Cluster ini didominasi oleh nasabah muda dengan profesi pelajar atau mahasiswa. Walaupun saldo rata-rata sedikit lebih rendah dibanding Cluster 1, nilai transaksi rata-rata justru sedikit lebih tinggi.
Hal ini menunjukkan perilaku transaksi yang lebih aktif dan dinamis, kemungkinan berkaitan dengan kebutuhan pendidikan, gaya hidup, atau transaksi harian.

---

# Kesimpulan

## Model clustering berhasil membagi nasabah menjadi dua kelompok utama:

1. Profesional mapan dengan kondisi finansial stabil
2. Nasabah muda dengan aktivitas transaksi lebih dinamis

Hasil clustering ini dapat dimanfaatkan untuk:

- Customer segmentation
- Fraud detection
- Personalized financial services
- Risk profiling
- Targeted marketing
