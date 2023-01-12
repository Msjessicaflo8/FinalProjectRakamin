# 🛒 Online Shoppers Purchasing Intention 🛒

## 📂 **Stage 0 : Problem Statement**
### **Problem Statement**
- Majestic merupakan suatu perusahaan E-commerce (marketplace) yang menyediakan berbagai macam kebutuhan untuk pelanggan. 
- Pada satu tahun terakhir, perusahaan hanya menghasilkan conversion rate (revenue true) sebesar 15% dari pelanggan yang mengunjungi website.
- Pada masa pandemi (2020-2021) menurut data Digital Experience Benchmark Report, conversion rate diberbagai industri e-commerce mengalami peningkatan rata-rata sebesar 28% dikarenakan secara signifikan kebiasaan customers untuk berbelanja beralih ke sistem online. Hal ini akan merupakan suatu kesempatan yang besar bagi perusahaan untuk meningkatkan revenue.

### **Objectives**
- Mendapatkan insight dari pola customer.
- Memprediksi pengunjung yang memiliki kecenderungan membeli atau tidak.
- Memberikan bisnis rekomendasi yang tepat.

### **Goals**
- Membuat model machine learning yang dapat memprediksi customer yang berpeluang menghasilkan revenue.
- Diharapkan revenue conversion rate dapat meningkat mencapai 28%.

### **Business Metrics**
-  Revenue Conversion Rate

## 📂 Stage 1 : Exploratory Data Analysis
### Dataset
Dataset memiliki fitur-fitur yang menunjukkan aktivitas website dan aktivitas pembelian.

### Descriptive Statistics
Insight yang di dapat dari analisis statistik berupa:
- Dataset Berisi 12330 baris dan 18 kolom
- Dataset meiliki kolom bertipe bool(2), float64(7), int64(7), objek(2)
- Variabel Target Revenue mempunhyai nilai bool, jadi ini klasifikasi biner True/False.
- Tidak ada null value

### Univariate Analysis
Semua kolom memiliki nilai outliers. Namun ada beberapa fitur yang tidak terdistribusi dengan baik yaitu fitur informational, informational_duration, pave_values, special_days, dan browser.

### Multivariate Analysis
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
### Data Cleansing
#### 1. Handle Missing Value
Tidak ada nilai yang kosong pada kolom, sehingga tidak dilakukan handling missing value.

#### 2. Handle Duplicated Value
Terdapat 125 data yang duplikat. Hanya diambil satu data untuk masing-masing duplikat.

#### 3. Handle Outlier
Presentase outlier menggunakan analisis Z-Score dalam data adalah 17.90%, nilai tersebut cukup besar, maka outlier tidak dihilangkan. Tidak dilakukan handle outlier ini juga kerana diasumsikan bukan dari kesalahan dalam pengambilan data.

#### 4. Feature Transformation
Transformasi feature tidak menggunakan log karena data memiliki banyak value dengan nilai 0. PowerTransformer Yeo-Johnson dipilih untuk membuat distribusi lebih mendekati normal (Guassian) dan mendukung value data memiliki nilai positif atau negatif.

#### 5. Feature Extraction
Mengubah data kategorikal kedalam numerikal. 
- OperatingSystems, Browser, Region, TrafficType sudah memiliki feature numerik
- Month akan dilakukan label encoding, pada bulan dibuat label peringkat berdasarkan jumlah peringkat user dari yang terbesar.
- VisitorType, Weekend, dan Revenue akan dilakukan One Hot Encoding

#### 6. Handle Class Imbalance
Handle imbalance menggunakan SMOTE dengan hasil False 10297 dan True 5148.

### Feature Enginering
#### 1. Feature Selection
Pada tahap feature selection ini fitur yang redundant adalah :
- Administrative - Administrative_Duration
- Informational - Informational_Duration
- ProductRelated - ProductRelated_Duration
- BounceRates - ExitRates
- Administrative - Administrative_Duration
- Informational - Informational_Duration
- ProductRelated - ProductRelated_Duration

Ketiga terakhir akan dibuat feature extraction untuk mendapatkan durasi tiap page nya, sedangkan BounceRates - ExitRates, akan dipilih salah satu, yaitu ExitRates

#### 2. Feature Extraction
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
