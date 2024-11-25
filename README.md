# CapstoneProjectModule3 - California Housing Prices
## Capstone Project Module 3 - [Rina Adibah]

---

## **A. Business Problem Understanding**

### **1. Background**
Properti merupakan salah satu kebutuhan primer yang memerlukan analisis mendalam sebelum mengambil keputusan, baik dari sisi pembeli maupun penjual. Di California, yang memiliki 58 counties dan 482 municipalities, harga rumah bervariasi tergantung pada lokasi geografis, fasilitas, dan faktor sosial ekonomi. Model prediktif yang baik dapat membantu memahami harga pasar secara lebih akurat.

### **2. Problem Statement**
Penjual dan pembeli rumah menghadapi tantangan dalam menentukan harga pasar yang wajar. Ketidakakuratan ini dapat mengarah pada peluang yang terlewatkan atau kerugian finansial. Dengan menggunakan dataset dari sensus California 1990, kita dapat membangun model yang membantu memprediksi harga rumah secara akurat.

### **3. Goals**
- Memahami faktor-faktor utama yang memengaruhi harga rumah.
- Mengembangkan model prediktif untuk mempermudah pengambilan keputusan bisnis.
- Memberikan wawasan berbasis data kepada pembeli dan penjual properti.

### **4. Analytic Approach**
- Melakukan eksplorasi data, pembersihan data, dan analisis fitur.
- Membangun model supervised machine learning (regresi).
- Mengevaluasi performa model dengan berbagai metrik evaluasi.

### **5. Modelling**
- Menggunakan model regresi seperti Linear Regression, KNN, Decision Tree, Random Forest, Gradient Boosting, AdaBoost, dan XGBoost.

### **6. Evaluation Metric**
- Evaluasi model menggunakan **RMSE**, **MAE**, **MAPE**, dan **R-squared** untuk menilai akurasi dan performa.

---

## **B. Data Understanding**

### **1. Column Description**
| **No** | **Nama Kolom**       | **Deskripsi Kolom**                                                   |
|--------|-----------------------|------------------------------------------------------------------------|
| 1      | longitude             | Koordinat garis bujur lokasi rumah.                                   |
| 2      | latitude              | Koordinat garis lintang lokasi rumah.                                 |
| 3      | housingMedianAge      | Usia median rumah di suatu distrik.                                   |
| 4      | totalRooms            | Total jumlah ruangan dalam satu distrik.                              |
| 5      | totalBedrooms         | Total jumlah kamar tidur dalam satu distrik.                          |
| 6      | population            | Total populasi dalam satu distrik.                                    |
| 7      | households            | Total rumah tangga dalam satu distrik.                                |
| 8      | medianIncome          | Median pendapatan per rumah tangga.                                   |
| 9      | medianHouseValue      | Median harga rumah (target).                                          |
| 10     | oceanProximity        | Jarak geografis rumah dari laut.                                      |

---

## **C. Data Preprocessing**

### **1. Missing Values**
- Kolom `total_bedrooms` memiliki missing values sebesar 0.1% dan diimputasi menggunakan median.

### **2. Outliers dan Data Abnormal**
- Outliers dihapus pada kolom:
  - `housing_median_age` (nilai > 52).
  - `median_house_value` (nilai > 500,001).

### **3. Feature Engineering**
- Fitur baru ditambahkan:
  - `bedrooms_per_room`: Rasio kamar tidur terhadap total ruangan.
  - `population_per_household`: Rasio populasi terhadap rumah tangga.

---

## **D. Machine Learning Modelling**

### **1. Data Splitting & Scaling**
- Splitting data: 70:30 untuk train-test set.
- Scaling:
  - One-Hot Encoding untuk fitur kategorikal (`ocean_proximity`).
  - PowerTransformer untuk fitur numerikal.

### **2. Model Selection**
- Model benchmark: Linear Regression, KNN, Decision Tree, Random Forest, AdaBoost, Gradient Boosting, dan XGBoost.
- Model terbaik: **XGBoost** dengan performa terbaik setelah tuning parameter.

### **3. Tuning Model**
- **XGBoost**:
  - RMSE: 38,376 (setelah tuning).
  - MAE: 26,119.6.
  - MAPE: 16.02% (kategori "Good Forecast").
- Hyperparameter optimal:
  - max_depth: 7, learning_rate: 0.07, n_estimators: 197.

---

## **E. Conclusion & Recommendation**

### **1. Conclusion**
- **XGBoost** memberikan performa terbaik dengan MAE 26,119.6 dan R² sebesar 0.81.
- Fitur `ocean_proximity` dan `median_income` memiliki pengaruh terbesar terhadap harga rumah.
- Model memiliki keterbatasan dalam memprediksi harga di luar rentang dataset (14,999 hingga 433,800).

### **2. Recommendation**
- **Untuk Bisnis Properti:**
  - Fokus pada pengembangan di area `INLAND` karena harga lebih stabil.
  - Tambahkan fasilitas di area dekat pantai (`<1H OCEAN`) untuk meningkatkan nilai properti.
- **Untuk Pengembangan Model:**
  - Gunakan dataset properti terbaru untuk mencerminkan kondisi pasar terkini.
  - Tambahkan fitur relevan seperti luas tanah, fasilitas rumah, dan aksesibilitas lokasi.

---

## **F. Save Model**
Model XGBoost yang telah dituning disimpan menggunakan library **pickle** untuk digunakan dalam implementasi lebih lanjut.
