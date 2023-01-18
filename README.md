# 🛒 **Online Shoppers Purchasing Intention** 🛒
---
## 📂 **Stage 0 : Problem Statement**
### Problem Statement
- Majestic merupakan suatu perusahaan E-commerce (marketplace) yang menyediakan berbagai macam kebutuhan untuk pelanggan. 
- Pada satu tahun terakhir, perusahaan hanya menghasilkan **Conversion Rate** sebesar **15%** dari pelanggan yang mengunjungi website.
- Pada masa pandemi (2020-2021) menurut data [**Digital Experience Benchmark Report**](https://contentsquare.com/blog/ecommerce-conversion-rate/), Conversion Rate diberbagai industri E-commerce mengalami **peningkatan** rata-rata sebesar **28%** dikarenakan secara signifikan kebiasaan pelanggan untuk berbelanja beralih ke sistem online. Hal ini akan menjadi suatu kesempatan besar bagi perusahaan untuk meningkatkan revenue.

<br>
<p align="center">
  <kbd><img src="pictures/ecommerce_data.png" width=600px> </kbd> <br>
  Gambar 1 – Rata-rata Conversion Rate untuk Industri E-commerce
</p>

### Objectives
- Mendapatkan **insight** mengenai pola kebiasaan pelanggan dalam berselancar di website.
- **Memprediksi** pengunjung yang memiliki kecenderungan membeli atau tidak.
- Memberikan **bisnis rekomendasi** yang tepat guna meningkatkan kecenderungan pelanggan untuk membeli.

### Goals
- Membuat model machine learning yang dapat memprediksi customer yang berpeluang menghasilkan revenue.
- Diharapkan model dapat menigkatkan Revenue Conversion Rate sebesar 28%.

### Business Matrics
-  Revenue Conversion Rate
---

## 📂 **Stage 1 : Exploratory Data Analysis**
### Dataset
<p align="center">
  Tabel 1 – Ringkasan Dataset<br>
  <kbd><img src="pictures/dataset.png" width=600px> </kbd> <br>
</p>

### Descriptive Statistics

<p align="center">
  <kbd><img src="pictures/distribusi.png" width=600px> </kbd> <br>
  Gambar 2 – Distribusi Dataset
</p>
<br>
<p align="center">
  <kbd><img src="pictures/outlier.png" width=600px> </kbd> <br>
  Gambar 3 – Distribusi Dataset dengan Boxplot
</p> 
<br>

Hasil analisi statistik deskriptif untuk fitur-fitur numerik adalah sebagai berikut :
1. Distribusi data secara keseluruhan cenderung **positively-skewed** (Mean > Median).
2. Administrative, Administrative_Duration, Informational, Informational_Duration, ProductRelated, ProductRelated_Duration, BounceRate, PageValues memiliki ekor distribusi yang pang panjang dengan nilai yang **menumpuk disekitar angka 0**.
3. Dari kedua kondisi diatas dan dari analisa menggunakan boxplot mayoritas fitur memiliki outlier. <br>


Sedangkan hasil analisis statistik deskriptif untuk fitur-fitur kategorik adalah sebagai berikut.
1. Beberapa fitur memiliki nilai yang **telah di encoding** seperti OperatingSystems, Browser, Region, dan TrafficType, sehingga apabila diperlukan interpretasi nilai maka diperlukan data tambahan.
2. Mayoritas pengunjung  berasal dari **region wilayah 2** dan ketika berselancar di website menggunakan **OperatingSystem jenis 2** dengan **Browser jenis 1**.
3. **Returning Visitor** merupakan pengunjung yang paling dominan. Pada fitur VisitorType ini perlu dilakukan penanganan terhadap nilai Other.
4. Terdapat dua bulan yang hilang pada fitur Month yaitu January dan April. Bulan **Mei** memiliki jumlah pengunjung terbanyak, lalu diikuti dengan bulan November.

### Analysis
<p align="center">
  <kbd><img src="pictures/corre.png" width=600px> </kbd> <br>
  Gambar 4 – Heatmap Analisis Multivariat
</p>
<br>

Hasil analisis korelasi antar fitur adalah sebagai berikut:
1. **PageValues** memiliki **korelasi yang tinggi** terhadap fitur **target** yaitu Revenue. Semakin tinggi nilai PageValue, maka semakin tinggi juga kemungkinan pelanggan untuk membeli.
2. Sedangkan **BounceRates** dan **ExitRates memiliki** nilai **korelasi negatif** terhadap **Revenue**, artinya semakin kecil nilai kedua fitur tersebut maka revenue akan semakin tinggi.
3. Beberapa fitur yang memiliki **multikorenialitas** diantaranya adalah :
    - ProductRelated dengan ProductRelated_Duration
    - Adminisitrative dengan Adminisitrative_Duration
    - Informational dengan Informational_Duration
    - BounceRates dengan ExitRates

### Insight
#### Revenue Conversion Rate Berdasarkan Visitor Type
<br>
<p align="center">
  <kbd><img src="pictures/visitor x revenue.png" width=600px> </kbd> <br>
  Gambar 5 – Revenue Conversion Rate Berdasarkan Visitor Type
</p>
<br>

- Hampir sebanyak **80%** pengunggung website didominasi oleh **Returning Visitor**. Hal ini dapat menunjukkan bahwa perusahaan E-commerce telah berhasil untuk mempertahankan pelanggan untuk selalu mengunjugi website. Namun **Revenue Conversion Rate lebih besar** terjadi pada **New Visitor**, yaitu **25% New Visitor melakukan pembelian**. Berbeda dengan Returning Visitor.
- Dibutuhkan data tambahan berupa angka revenue atau profit apabila ingin dilakukan analisa lebih jauh untuk mengetahui pelanggan tipe pengunjung mana yang menghasilkan keuntungan lebih besar bagi perusahaan.
- Dari insight yang ditemukan dibutuhkan rekomendasi bisnis yang tepat untuk **meningkatkan Revenue Conversion Rate bagi Returning Visitor** dan juga untuk **meningkatkan jumlah New Visitor**.

#### Total Pengunjung per Bulan berdasarkan Revenue
<br>
<p align="center">
  <kbd><img src="pictures/monthly visitor x revenue.png" width=600px> </kbd> <br>
  Gambar 6 – Total Pengunjung per Bulan berdasarkan Revenue
</p>
<br>

- Berdasarkan grafik analisis diatas dapat dilihat bahwa trafik kunjungan pelanggan, memiliki jumlah **pengunjung yang paling tinggi** pada bulan **Mei** dan selanjutnya disusul dengan bulan **November**. 
- Namun pada bulan Mei tingginya trafik **tidak diikuti dengan tingginya angka Revenue Conversion Rate** yang hanya menghasilkan **11%**, angka ini masih cukup rendah dibandingkan dengan bulan-bulan lainnya. Sedangkan **November** merupakan bulan yang memiliki cukup **banyak pengunjung** dengan nilai **Revenue Conversion Rate** bulanan yang **paling tinggi**, yaitu mencapai **25%**.

---

## 📂 **Stage 3 : Data Pre-processing**
### Workflow Data Pre-processing
<br>
<p align="center">
  <kbd><img src="pictures/workflow preprocessing.png" width=300px> </kbd> <br>
  Gambar 7 – Workflow Data Pre-Processing
</p>

#### 1. Handling Tipe Data, Nilai, dan Duplikat
- tipe data
- nilai
- Terdapat 125 data yang duplikat. Hanya diambil satu data untuk masing-masing duplikat.

#### 2. Handling Outlier
Presentase outlier menggunakan analisis Z-Score dalam data adalah 17.90%, nilai tersebut cukup besar, maka outlier tidak dihilangkan. Tidak dilakukan handle outlier ini juga kerana diasumsikan bukan dari kesalahan dalam pengambilan data.

#### 3. Feature Transformation
Transformasi feature tidak menggunakan log karena data memiliki banyak value dengan nilai 0. PowerTransformer Yeo-Johnson dipilih karena dapat digunakan pada data yang distribusi awalnya positively/negatively-skewed, untuk membuat distribusinya menjadi lebih mendekati normal (Guassian), dan mendukung value data memiliki nilai positif atau negatif.

#### 4. Feature Encoding

#### 5. Feature Extraction
Handle imbalance menggunakan SMOTE dengan hasil False 10297 dan True 5148.

#### 6. Feature Selection
Pada tahap feature selection ini fitur yang redundant adalah :
- Administrative - Administrative_Duration
- Informational - Informational_Duration
- ProductRelated - ProductRelated_Duration
- BounceRates - ExitRates
- Administrative - Administrative_Duration
- Informational - Informational_Duration
- ProductRelated - ProductRelated_Duration

Ketiga terakhir akan dibuat feature extraction untuk mendapatkan durasi tiap page nya, sedangkan BounceRates - ExitRates, akan dipilih salah satu, yaitu ExitRates

#### 7. Split Data Train dan Test
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

#### 8. Handling Class Imbalance



---
## 📂 **Stage 4 : Modeling and Evaluation**
---
## 📂 **Stage 5 : Business Insight and Recomendation**
