# Dataset-Online-Shoppers-Purchasing-Intention
Dataset ini berasal dari [UCI Machine Learning Repository](https://archive.ics.uci.edu/static/public/468/data.csv) dan berisi 12.330 sesi pengguna dari situs e-commerce, masing-masing mewakili satu sesi unik dalam periode satu tahun. Tujuan utama dataset ini adalah memprediksi apakah sesi tersebut akan menghasilkan transaksi pembelian (`Revenue = True`) atau tidak (`Revenue = False`).
## 🔍 Deskripsi Dataset
- **Jumlah Sesi:** 12.330
- **Fitur:** 17 fitur numerik dan kategorikal
- **Target:** `Revenue` (Boolean: True/False)

### Distribusi Kelas
- 84,5% sesi tidak menghasilkan pembelian (kelas negatif)
- 15,5% sesi menghasilkan pembelian (kelas positif)

## 🧾 Penjelasan Fitur

| Fitur                     | Tipe        | Deskripsi                                                                 |
|--------------------------|-------------|---------------------------------------------------------------------------|
| Administrative           | Integer     | Jumlah halaman administratif yang dikunjungi                             |
| Administrative_Duration  | Float       | Total waktu yang dihabiskan pada halaman administratif                   |
| Informational            | Integer     | Jumlah halaman informasi yang dikunjungi                                 |
| Informational_Duration   | Float       | Total waktu yang dihabiskan pada halaman informasi                       |
| ProductRelated           | Integer     | Jumlah halaman produk yang dikunjungi                                    |
| ProductRelated_Duration  | Float       | Total waktu yang dihabiskan pada halaman produk                          |
| BounceRates              | Float       | Persentase pengunjung yang meninggalkan situs setelah melihat satu halaman |
| ExitRates                | Float       | Persentase pengunjung yang keluar dari situs dari halaman tertentu       |
| PageValues               | Float       | Nilai rata-rata halaman sebelum transaksi terjadi                        |
| SpecialDay               | Float       | Indikator kedekatan dengan hari spesial (misalnya Hari Ibu, Valentine)   |
| Month                    | Kategorikal | Bulan saat sesi terjadi (misalnya 'Feb', 'Mar')                          |
| OperatingSystems         | Integer     | Sistem operasi yang digunakan pengunjung                                 |
| Browser                  | Integer     | Browser yang digunakan pengunjung                                        |
| Region                   | Integer     | Wilayah geografis pengunjung                                             |
| TrafficType              | Integer     | Sumber lalu lintas pengunjung                                            |
| VisitorType              | Kategorikal | Tipe pengunjung: Baru, Kembali, Lainnya                                  |
| Weekend                  | Boolean     | Apakah sesi terjadi pada akhir pekan                                     |
| Revenue                  | Boolean     | Target: Apakah sesi menghasilkan pembelian                               |

## 🎯 Tujuan Penggunaan
Dataset ini cocok untuk berbagai tugas pembelajaran mesin, seperti:

- **Klasifikasi:** Memprediksi kemungkinan terjadinya pembelian berdasarkan perilaku pengunjung.
- **Clustering:** Mengelompokkan pengunjung berdasarkan pola perilaku mereka.
- **Analisis Perilaku Pengguna:** Memahami faktor-faktor yang mempengaruhi keputusan pembelian.

# Penjelasan Notebook: OnlineShoppers Purchasing Intention

# INSTALASI PACKAGE
 python pip install ucimlrepo 
 - Penjelasan: Langkah-langkah lainnya dalam pemrosesan atau visualisasi data.
# PEMANGGILAN LIBRARY
 python import ucimlrepo 
 - Penjelasan: Mengimpor pustaka yang dibutuhkan untuk analisis, visualisasi, dan pemodelan.
# MELIHAT DATASET YANG DISEDIAKAN
 python dir(ucimlrepo)
 - Penjelasan: Langkah-langkah lainnya dalam pemrosesan atau visualisasi data.
 python from ucimlrepo import list_available_datasets
 - Penjelasan: Mengimpor pustaka yang dibutuhkan untuk analisis, visualisasi, dan
 pemodelan.
 python data = list_available_datasets()
 - Penjelasan: Langkah langkah lainnya dalam pemrosesan atau visualisasi data.
 Pada list dataset tersebut saya ingin menggunakan dataset Online Shoppers
 Purchasing Intention Dataset
# Import Library
 python import pandas as pd import numpy as np import seaborn as sns
 import matplotlib.pyplot as plt from ucimlrepo import fetch_ucirepo
 from sklearn.modelselection import traintestsplit from
 sklearn.preprocessing import LabelEncoder, StandardScaler from
 sklearn.ensemble import RandomForestClassifier from sklearn.metrics
 import classificationreport, confusionmatrix, accuracyscore ```
 - Penjelasan: Mengimpor pustaka yang dibutuhkan untuk analisis, visualisasi, dan
 pemodelan.
# FECT DATA / LOAD DATA
 python data = fetch_ucirepo(id=468)
 - Penjelasan: Langkah-langkah lainnya dalam pemrosesan atau visualisasi data.
 python data
 - Penjelasan: Langkah-langkah lainnya dalam pemrosesan atau
 visualisasi data.
# Load Dataset
 python data = pd.read_csv("https://archive.ics.uci.edu/static/
 public/468/data.csv")
 - Penjelasan: Langkah-langkah lainnya dalam
 pemrosesan atau visualisasi data.
 python data
 - Penjelasan: Langkah-langkah lainnya dalam pemrosesan atau visualisasi data.
# Pra-pemrosesan Data
 python label_encoders = {} categorical_cols = ['Month',
 'VisitorType', 'Weekend'] for col in categorical_cols: le =
 LabelEncoder() data[col] = le.fit_transform(data[col])
 label_encoders[col] = le
 - Penjelasan: Melakukan konversi fitur kategorikal ('Month', 'VisitorType', 'Weekend') menjadi nilai numerik.
 python data['Revenue'] = data['Revenue'].astype(int)
 - Penjelasan: Langkah-langkah lainnya dalam pemrosesan atau visualisasi data.
 python X = data.drop('Revenue', axis=1) y = data['Revenue'] 
 - Penjelasan: Langkah-langkah lainnya dalam pemrosesan atau visualisasi data.
 python scaler = StandardScaler() X_scaled =
 scaler.fit_transform(X)
 - Penjelasan: Langkah-langkah lainnya dalam pemrosesan atau visualisasi data.
 python X_train, X_test, y_train, y_test =
 train_test_split(X_scaled, y, test_size=0.2, random_state=42,
 stratify=y)
 - Penjelasan: Langkah-langkah lainnya dalam pemrosesan atau visualisasi data.
# Split Data
 python model = RandomForestClassifier(random_state=42)
 model.fit(X_train, y_train) Penjelasan: Langkah-langkah lainnya
 dalam pemrosesan atau visualisasi data.
# Evaluasi Model
 ```python ypred = model.predict(Xtest)
 print("Confusion Matrix:") print(confusionmatrix(ytest, ypred))
 print("\nClassification Report:") print(classificationreport(ytest, ypred))
 print("\nAccuracy:", accuracyscore(ytest, y_pred)) ```
 - Penjelasan: Langkah langkah lainnya dalam pemrosesan atau visualisasi data.
 # Visualisasi Pentingnya Fitur
 python feature_importances =
 pd.Series(model.feature_importances_, index=X.columns)
 feature_importances.sort_values(ascending=True).plot(kind='barh',
 figsize=(10,6)) plt.title("Feature Importances") plt.show() 
 - Penjelasan: Mengimpor pustaka yang dibutuhkan untuk analisis,visualisasi, dan pemodelan.
# visualisasi distribusi data
 python sns.countplot(x='Month', hue='Revenue', data=data)
 plt.title("Distribusi Transaksi per Bulan")
 plt.xticks(rotation=45) plt.show()
 - Penjelasan: Membuat plot batang untuk menunjukkan distribusi data per bulan dan dikategorikan berdasarkan variabel target 'Revenue'.
 # Oversampling dengan SMOTE
 ```python from imblearn.over_sampling import SMOTE
 smote = SMOTE(randomstate=42) Xresampled, yresampled =
 smote.fitresample(X_scaled, y) ```
 - Penjelasan: Mengimpor pustaka yang
 dibutuhkan untuk analisis, visualisasi, dan pemodelan.
 # Membangun Model Klasifikasi dengan Logistic Regression
 python from sklearn.linear_model import LogisticRegression model
 = LogisticRegression(class_weight='balanced') model.fit(X_train,
 y_train)
 - Penjelasan: Mengimpor pustaka yang dibutuhkan untuk analisis,visualisasi, dan pemodelan.
# visualisasi data berdimensi tinggi menggunakan PCA (Principal Component Analysis)
 ```python from sklearn.decomposition import PCA
 pca = PCA(ncomponents=2) Xpca = pca.fittransform(Xscaled)
 plt.scatter(Xpca[:, 0], Xpca[:, 1], c=y, cmap='coolwarm', alpha=0.6)
 plt.title("PCA Visualization") plt.xlabel("PC1") plt.ylabel("PC2") plt.show() ```
  - Penjelasan: Mengimpor pustaka yang dibutuhkan untuk analisis,
 visualisasi, dan pemodelan.
 # Import library yang dibutuhkan untuk clustering, reduksi dimensi,dan visualisasi
 ```python from sklearn.cluster import KMeans
 kmeans = KMeans(nclusters=3, randomstate=42) clusters =
 kmeans.fitpredict(Xscaled) data['Cluster'] = clusters ```
 - Penjelasan: Mengimpor pustaka yang dibutuhkan untuk analisis, visualisasi, dan pemodelan.
 python from sklearn.cluster import KMeans from
 sklearn.decomposition import PCA import matplotlib.pyplot as plt
 import seaborn as sns
 - Penjelasan: Mengimpor pustaka yang dibutuhkan untuk analisis, visualisasi, dan pemodelan.
 # Mereduksi fitur dari X_scaled(data hasil preprocessing dan scaling) menjadi 2 dimensi utama dengan PCA, supaya bisa divisualisasikan dalam grafik 2D
 python pca = PCA(n_components=2, random_state=42) X_pca =
 pca.fit_transform(X_scaled)
 - Penjelasan: Menerapkan PCA (Principal Component Analysis) untuk reduksi dimensi dan memvisualisasikan data.
python kmeans = KMeans(n_clusters=2, random_state=42)
 cluster_labels = kmeans.fit_predict(X_scaled)
 - Penjelasan: Menggunakan KMeans clustering untuk mengelompokkan data pengunjung.
 Membangun model K-Means dengan jumlah klaster = 2 (bisa diubah ke 3, 4,
 dst tergantung kebutuhan), dan menyimpan hasil prediksi klaster masing
masing data dalam cluster_labels
 # Membuat visualisasi hasil klastering:
 python plt.figure(figsize=(8, 6)) sns.scatterplot(x=X_pca[:, 0],
 y=X_pca[:, 1], hue=cluster_labels, palette='Set2', alpha=0.7)
 plt.title('Clustering Pengunjung (K-Means, PCA 2D)')
 plt.xlabel('Principal Component 1') plt.ylabel('Principal
 Component 2') plt.legend(title='Cluster') plt.show()
 - Penjelasan:Menampilkan visualisasi hasil analisis (seperti scatter plot, histogram, dll).
 • Titik-titik mewakili pengunjung (data),
 • Sumbu X dan Y adalah hasil reduksi dimensi PCA (PC1 dan PC2),
 • Warna berbeda menunjukkan cluster berbeda,
 • Tujuannya untuk melihat apakah klaster memang membentuk
 kelompok yang jelas.
