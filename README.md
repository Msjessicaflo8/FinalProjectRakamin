# 🛒 Online Shoppers Purchasing Intention 🛒

## 📂 Stage 0 : Overview
### 📌 Problem Statement
Sebuah platform online shop pada rentang waktu tertentu memiliki 12.330 visitor. Namun visitor yang menghasilkan revenue hanya sebesar 15%. Dangan kata lain sebagian besar 85% visitor tidak melakukan pembelian. Menganalisa pola mengapa visitor yang membeli lebih kecil daripada yang tidak, perlu dilakukan untuk pembuatan model prediksi yang dapat meningkatkan revenue conversion rate.

### 📌 Objective
- Mendapatkan insight dari pola user yang menghasilkan revenue
- Memprediksi pengunjung yang memiliki kecenderungan membeli atau tidak guna meningkatkan revenue convesion rate
- Memberikan bisnis rekomendasi yang tepat

### 📌 Business Metrics
-  Revenue Conversion Rate

## 📂 Stage 1 : Exploratory Data Analysis
### 📌 Descriptive Statistics
Insight yang di dapat dari analisis statistik berupa:
- Dataset Berisi 12330 baris dan 18 kolom
- Dataset meiliki kolom bertipe bool(2), float64(7), int64(7), objek(2)
- Variabel Target Revenue mempunhyai nilai bool, jadi ini klasifikasi biner True/False.
- Tidak ada null value

### 📌 Univariate Analysis
Semua kolom memiliki nilai outliers. Namun ada beberapa fitur yang tidak terdistribusi dengan baik yaitu fitur informational, informational_duration, pave_values, special_days, dan browser.

### 📌 Multivariate Analysis
**Hubungan Antar Kolom Numerikal :**
- Beberapa feature yang kemungkinan redundan karena memiliki korelasi yang cukup tinggi (>0.7) diantaranya ProductRelated dengan ProductRelated_Duration, Adminisitrative dengan Adminisitrative_Duration, Informational dengan Informational_Duration, dan begitu pula BounceRates dengan ExitRates. Dalam tahap data prepocessing feature-feature tersebut dapat di drop ataupun dipilih salah satu.
- Kolom PageValues ternyata memiliki korelasi yang cukup dengan Revenue_numbers (0.49) sehingga perlu dipertahankan.
- Kolom BounceRates dengan beberapa kolom lain, exitrates dengan beberapa kolom lain, dan page values dengan beberapa kolom lain berkumpul di bawah dan samping kiri cenderung membentuk pola logaritmik. Itu artinya, Apabila kolom BounceRates dan kolom Informational_Duration berhubungan secara logaritmik, semakin besar nilai BounceRates, nilai Informational_Duration semakin kecil secara logaritmik. 
- Terdapat beberapa kolom yang bentuknya linier, seperti kolom BounceRates dan kolom ExitRates juga kolom ProductRelated dan ProductRelated_Duration.

**Hubungan Antar Kolom Kategorikal :**
- Korelasi VisitorType dengan Browser dan OperatingSystem angkanya terlalu dekat (0.47 dan 0.51), sehingga antara Browser dan OperatingSystem ada kemungkinan akan di drop namun perlu dipertimbangkan kembali berhubung nilai korelasi Browser dan OperatingSystem yang tidak terlalu tinggi (0.6).
- Ada korelasi yang rendah antara kolom TrafficType dan VisitorType (0.39).
- Nilai korelasi antar kolom dengan kolom Revenue cenderung rendah.

**Hubungan Antar Kolom Kategorikal dan Numerikal:**
- Tidak banyak insight yang bisa didapatkan. Contohnya pada kolom revenue terhadap kolom numerikal lain (di samping). Persebaran kolom merata baik customer yang memberikan revenue dan yang tidak. Begitu pula dengan grafik kolom Month dengan kolom numerikal lain (bawah).

## 📂 Stage 2 : Data Preprocessing
### 📌 Data Cleansing
### 1. Handle Missing Value
Tidak ada nilai yang kosong pada kolom, sehingga tidak dilakukan handling missing value.

### 2. Handle Duplicated Value
Terdapat 125 data yang duplikat. Hanya diambil satu data untuk masing-masing duplikat.

### 3. Handle Outlier
Presentase outlier menggunakan analisis Z-Score dalam data adalah 17.90%, nilai tersebut cukup besar, maka outlier tidak dihilangkan. Tidak dilakukan handle outlier ini juga kerana diasumsikan bukan dari kesalahan dalam pengambilan data.

### 4. Feature Transformation
Transformasi feature tidak menggunakan log karena data memiliki banyak value dengan nilai 0. PowerTransformer Yeo-Johnson dipilih untuk membuat distribusi lebih mendekati normal (Guassian) dan mendukung value data memiliki nilai positif atau negatif.

### 5. Feature Extraction
Mengubah data kategorikal kedalam numerikal. 
- OperatingSystems, Browser, Region, TrafficType sudah memiliki feature numerik
- Month akan dilakukan label encoding, pada bulan dibuat label peringkat berdasarkan jumlah peringkat user dari yang terbesar.
- VisitorType, Weekend, dan Revenue akan dilakukan One Hot Encoding

### 6. Handle Class Imbalance
Handle imbalance menggunakan SMOTE dengan hasil False 10297 dan True 5148.

## 📌 Feature Enginering
### 1. Feature Selection
Pada tahap feature selection ini fitur yang redundant adalah :
- Administrative - Administrative_Duration
- Informational - Informational_Duration
- ProductRelated - ProductRelated_Duration
- BounceRates - ExitRates
- Administrative - Administrative_Duration
- Informational - Informational_Duration
- ProductRelated - ProductRelated_Duration

Ketiga terakhir akan dibuat feature extraction untuk mendapatkan durasi tiap page nya, sedangkan BounceRates - ExitRates, akan dipilih salah satu, yaitu ExitRates

### 2. Feature Extraction
Pembuatan feature :
- Duration per Page Administrative
- Duration per Page Informational
- Duration per Page ProductRelated

**Data yang dipilih :**
- Duration per Page Administrative
- Duration per Page Informational
- Duration per Page ProductRelated
- ExitRates
- PageValues
- SpecialDay
- Month
- VisitorType_Returning_Visito
- Revenue_True
