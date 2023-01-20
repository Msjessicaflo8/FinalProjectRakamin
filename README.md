# 🛒 **Online Shoppers Purchasing Intention** 🛒
---
## 📂 **Stage 0 : Problem Statement**
### Problem Statement
- Majestic merupakan suatu perusahaan E-commerce (marketplace) yang menyediakan berbagai macam kebutuhan untuk pelanggan. 
- Pada satu tahun terakhir, perusahaan hanya menghasilkan **Conversion Rate** sebesar **15%** dari pelanggan yang mengunjungi website.
- Pada masa pandemi (2020-2021) menurut data [**Digital Experience Benchmark Report**](https://contentsquare.com/blog/ecommerce-conversion-rate/), Conversion Rate diberbagai industri E-commerce mengalami **peningkatan** rata-rata sebesar **28%** dikarenakan secara signifikan kebiasaan pelanggan untuk berbelanja beralih ke sistem online. Hal ini akan menjadi suatu kesempatan besar bagi perusahaan untuk meningkatkan revenue.

<br>
<p align="center">
  <kbd><img src="pictures/ecommerce_data.png" width=650px> </kbd> <br>
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
<br>

---

## 📂 **Stage 1 : Exploratory Data Analysis**
### Dataset
<p align="center">
  Tabel 1 – Ringkasan Dataset<br>
  <kbd><img src="pictures/dataset.png" width=650px> </kbd> <br>
</p>

### Descriptive Statistics

<p align="center">
  <kbd><img src="pictures/distribution.png" width=650px> </kbd> <br>
  Gambar 2 – Distribusi Dataset
</p>
<br>
<p align="center">
  <kbd><img src="pictures/outlier.png" width=650px> </kbd> <br>
  Gambar 3 – Distribusi Dataset dengan Boxplot
</p> 
<br>

Hasil analisi statistik deskriptif untuk **fitur-fitur numerikal** adalah sebagai berikut :
1. Distribusi data secara keseluruhan cenderung **positively-skewed** (**Mean > Median**).
2. Administrative, Administrative_Duration, Informational, Informational_Duration, ProductRelated, ProductRelated_Duration, BounceRate, PageValues memiliki ekor distribusi yang pang panjang dengan nilai yang **menumpuk disekitar angka 0**.
3. Dari kedua kondisi diatas dan dari analisa menggunakan boxplot mayoritas fitur memiliki outlier. <br>
<br>

Sedangkan hasil analisis statistik deskriptif untuk fitur-fitur **kategorikal** adalah sebagai berikut.
1. Beberapa fitur memiliki nilai yang **telah di encoding** seperti OperatingSystems, Browser, Region, dan TrafficType, sehingga apabila diperlukan interpretasi nilai maka diperlukan data tambahan.
2. Mayoritas pengunjung  berasal dari **region wilayah 2** dan ketika berselancar di website menggunakan **OperatingSystem jenis 2** dengan **Browser jenis 1**.
3. **Returning Visitor** merupakan pengunjung yang paling dominan. Pada fitur VisitorType ini perlu dilakukan penanganan terhadap nilai Other.
4. Terdapat dua bulan yang hilang pada fitur Month yaitu January dan April. Bulan **Mei** memiliki jumlah pengunjung terbanyak, lalu diikuti dengan bulan November.
<br>

### Analysis
<p align="center">
  <kbd><img src="pictures/corre.png" width=650px> </kbd> <br>
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
<br>

### Insight
#### Revenue Conversion Rate Berdasarkan Visitor Type
<br>
<p align="center">
  <kbd><img src="pictures/vistor x revenue.png"> </kbd> <br>
  Gambar 5 – Revenue Conversion Rate Berdasarkan Visitor Type
</p>
<br>

- Hampir sebanyak **80%** pengunggung website didominasi oleh **Returning Visitor**. Hal ini dapat menunjukkan bahwa perusahaan E-commerce telah berhasil untuk mempertahankan pelanggan untuk selalu mengunjugi website. Namun **Revenue Conversion Rate lebih besar** terjadi pada **New Visitor**, yaitu **25% New Visitor melakukan pembelian**. Berbeda dengan Returning Visitor.
- Dibutuhkan data tambahan berupa angka revenue atau profit apabila ingin dilakukan analisa lebih jauh untuk mengetahui pelanggan tipe pengunjung mana yang menghasilkan keuntungan lebih besar bagi perusahaan.
- Dari insight yang ditemukan dibutuhkan rekomendasi bisnis yang tepat untuk **meningkatkan Revenue Conversion Rate bagi Returning Visitor** dan juga untuk **meningkatkan jumlah New Visitor**.

#### Total Pengunjung per Bulan berdasarkan Revenue
<br>
<p align="center">
  <kbd><img src="pictures/monthly visitor x revenue.png"> </kbd> <br>
  Gambar 6 – Total Pengunjung per Bulan berdasarkan Revenue
</p>
<br>

- Berdasarkan grafik analisis diatas dapat dilihat bahwa trafik kunjungan pelanggan, memiliki jumlah **pengunjung yang paling tinggi** pada bulan **Mei** dan selanjutnya disusul dengan bulan **November**. 
- Namun pada bulan Mei tingginya trafik **tidak diikuti dengan tingginya angka Revenue Conversion Rate** yang hanya menghasilkan **11%**, angka ini masih cukup rendah dibandingkan dengan bulan-bulan lainnya. Sedangkan **November** merupakan bulan yang memiliki cukup **banyak pengunjung** dengan nilai **Revenue Conversion Rate** bulanan yang **paling tinggi**, yaitu mencapai **25%**.
<br>

---

## 📂 **Stage 3 : Data Pre-processing**
### Workflow Data Pre-processing
<br>
<p align="center">
  <kbd><img src="pictures/workflow preprocessing.png"> </kbd> <br>
  Gambar 7 – Workflow Data Pre-Processing
</p>
<br>

#### 1. Handling Nilai dan Duplikat
- Nilai **'Other'** pada fitur **VisitorType** diubah kedalam nilai dengan frekuensi terbanyak yaitu menjadi **'Returning Visitor'**.
- Terdapat 125 data yang duplikat. Hanya **diambil satu data** untuk masing-masing duplikat.

#### 2. Handling Outlier
Presentase outlier menggunakan analisis Z-Score dalam data adalah **17.90%**, nilai tersebut cukup besar, maka **outlier tidak dihilangkan**. Tidak dilakukan handle outlier ini juga kerana diasumsikan **bukan dari kesalahan dalam pengambilan data**.

#### 3. Feature Transformation
Transformasi feature tidak menggunakan log karena data memiliki banyak value dengan nilai 0. **PowerTransformer Yeo-Johnson** dipilih karena dapat digunakan pada data yang distribusi awalnya positively/negatively-skewed, untuk membuat distribusinya menjadi lebih mendekati normal (Guassian), dan mendukung value data memiliki nilai positif atau negatif.

#### 4. Feature Encoding
Fitur VisitorType dan Revenue dilakukan **One Hot Encoding**.

#### 5. Feature Extraction
Membuat fitur baru dari fitur yang sudah ada, diantaranya adalah:
- Duration Page Per Administrative
- Duration Page Per Informational
- Duration Page Per Product Related

#### 6. Feature Selection
Pada tahap ini dilakukan seleksi fitur yang memiliki **korelasi terhadap revenue**, menghilangkan fitur yang redundan dan kurang relavan terhadap performa model. Fitur-fitur yang dipilih antara lain adalah :
- Duration per Page Administrative
- Duration per Page Informational
- ProductRelated
- ExitRates
- PageValues
- SpecialDay
- VisitorType_Returning_Visitor
- Revenue_True

#### 7. Splitting Data Train dan Test
Splitting dataset train dan test dilakukan dengan proporsi **70 : 30**.

#### 8. Handling Class Imbalance
Dikarenakan jumlah kelas antar fitur target cukup besar maka Handling Class Imbalance dilakukan pada data train dengan menggunakan metode **SMOTE**. <br>
<br>

---

## 📂 **Stage 4 : Modeling and Evaluation**
Berdasarkan beberapa algoritma yang telah diterapkan untuk uji coba performa model, algoritma Random Forest yang telah dilakukan Hyperparameter Tuning dipilih untuk diterapkan.

### Random Forest : Modeling and Evaluation
ROC-AUC dipilih sebagai matriks evaluasi ntuk mengetahui **sejauh mana model klasifikasi memisahkan pengunjung mana yang diprediksi membeli dan tidak**. Metrik ROU-AUC ini diplot dengan dua matriks yang dibandingkan satu sama lain yaitu **TPR** (True Positive Rate atau Recall) dan **FPR** (False Positive Rate).

<p align="center">
   Tabel 2 – Hasil Evaluasi Matriks Random Forest dengan Hyperparameter Tuning  <br>
   <kbd><img src="pictures/matrix.png" width=500px> </kbd>
</p>
<br>

<p align="center">
  <kbd><img src="pictures/confussionmatrix.png" width=500px> </kbd> <br>
  Gambar 8 – Confussion Matrix Random Forest dengan Hyperparameter Tuning
</p>
<br>

Model yang sangat baik memiliki ROC-AUC mendekati 1 yang berarti memiliki ukuran keterpisahan yang baik. Menurut Gorunescu (2011), nilai ROC-AUC juga dapat di klasifikasikan sebagai berikut:

<p align="center">
   Tabel 2 – Hasil Evaluasi Metriks Random Forest dengan Hyperparameter Tuning  <br>
   <kbd><img src="pictures/auc.png" width=500px> </kbd>
</p>
<br>

Nilai ROC-AU dari Random Forest didapatkan hasil sebesar **0.90** yang berarti model memiliki performa yang **sudah baik**.
<br>

### Random Forest : Feature Importances
Selanjutnya, untuk mengetahui seberapa fitur-fitur berpengaruh terhadap model prediksi, dilakukan analisis menggunakan SHAP Value. Berikut ini hasil dari urutan fitur-fitur (**feature importance**) yang memiliki pengaruh paling tinggi hingga yang paling rendah pengaruhnya terhadap model prediksi.

<p align="center">
  <kbd><img src="pictures/barshap.png" width=800px> </kbd> <br>
  Gambar 9 – Grafik Feature Importance Menggunakan Barplot SHAP Value
</p>
<br>

- Grafik ini memperhitungkan **nilai SHAP absolut, jadi tidak masalah jika fitur mempengaruhi prediksi secara positif atau negatif**. 
- Tiga fitur yang paling mempengaruhi adalah **PageValues, ExitRates, dan ProductRelated**.
<br>

Pada grafik **beeswram** dapat diketahui bagaimana nilai yang lebih tinggi atau lebih rendah dari fitur tersebut akan mempengaruhi hasil prediksi.

<p align="center">
  <kbd><img src="pictures/beeswarm.png" width=800px> </kbd> <br>
  Gambar 10 – Grafik Summaryplot Beeswarm SHAP Value
</p>
<br>

- **PageValues** dan **ProductRelated** yang memiliki nilai lebih tinggi akan memiliki dampak positif terhadap prediksi (**berkorelasi positif terhadap target**). Dapat diinterpretasikan bahwa, **semakin besar** nilai pada **PageValues** dan **ProductRelated** maka kecenderungan model untuk memprediksi **target positif** (pengunjung yang membeli) akan **semakin besar**. 
- Sedangkan untuk **ExitRates**, apabila memiliki nilai yang lebih tinggi maka akan berdampak negatif pada prediksi (**berkorelasi negatif terhadap target**). Jadi **semakin kecil nilai ExitRates**-nya, maka model **memprediksi pengunjung yang membeli akan semakin besar**.
<br>

---
## 📂 **Stage 5 : Business Insight and Recomendation**

### Business Insight - PageValues

<p align="center">
  <kbd><img src="pictures/pagevaluedistribution.png" width=650px> </kbd> <br>
  Gambar 11 – Distribusi PageValues
</p>

<p align="center">
   Tabel 3 – Persentase PageValues berdasarkan Revenue Conversion Rate  <br>
   <kbd><img src="pictures/pagevalues.png" width=450px> </kbd>
</p>
<br>

- Pengunjung yang melakukan **pembelian** cenderung mengunjungi halaman website dengan nilai **PageValues** yang **lebih besar** dibandingkan dengan pengunjung yang tidak melakukan pembelian.
- Nilai **Revenue Conversion Rate** pada PageValues yang memiliki nilai **lebih dari 0** dapat mencapai **56%**. Dari hal tersebut PageValues ini memilki korelasi yang kuat terhadap target. <br>
<br>

### Business Insight - ExitRates

<p align="center">
  <kbd><img src="pictures/exitrate.png" width=650px> </kbd> <br>
  Gambar 12 – Distribusi ExitRates
</p>
<br>

- Pengunjung yang melakukan **pembelian** cenderung memiliki nilai **ExitRates** yang **lebih rendah** dibandingkan dengan pengunjung yang tidak melakukan pembelian.
- Dari analisis dapat dilihat bahwa nilai **maksimal ExitRates adalah 20%**. Menurut [sumber](https://upqode.com/bounce-rate-vs-exit-rate/) rata-rata Exit Rates untuk sebuah website e-commerce berada **dibawah 25%**. Jadi, nilai Exit Rates tersebut masih dapat diterima.<br>
<br>

### Business Insight - Product Related
<p align="center">
  <kbd><img src="pictures/productrelated.png" width=500px> </kbd> <br>
  Gambar 13 – Distribusi ExitRates
</p>
<br>

- Menurut [sumber](https://www.klipfolio.com/metrics/marketing/page-views-per-session/), **rata-rata page views** untuk website seluruh industri adalah **5**. Berdasarkan hal tersebut, nilai page views **ProductRelated** sebagian besar **sudah melebihi dari rata-rata**. 
- Probabilitas pengunjung untuk melakukan pembelian dapat menjadi tinggi apabila pengunjung tersebut menghabiskan waktu paling tidak [**50 detik**](https://medium.com/cappasity-blog/average-time-on-page-its-impact-on-purchase-probability-for-e-commerce-edcfab5b02ad) pada sebuah halaman produk.<br>
<br>

### Mechine Learning Prediction Workflow

Beikut ini adalah Workflow dari **Early Purchase Prediction** yaitu machine learning untuk memprediksi pengunjung untuk membeli atau tidak sebelum pengunjung melakukan pembelian.

<p align="center">
  <kbd><img src="pictures/workflow.png"> </kbd> <br>
  Gambar 14 – Mechine Learning Prediction Workflow
</p>
<br>

### Business Recomendation
#### Rekomendasi Bisnis Berdasarkan Mechine Learning
- Pemberian notifikasi rekomendasi laman produk untuk jenis yang sama dengan PageValues yang lebih tinggi. PageValues yang tinggi ini dapat dimaksimalkan dengan konten dan kegunaan pada halaman-halaman serta peringkat yang baik untuk produk. Dari hal tersebut diharapkan dapat meningkatkan nilai Revenue Conversion Rate.

#### Rekomendasi Bisnis Berdasarkan Insight
- Pemberian promosi dan pengadaan event pada bulan-bulan tertentu yang memiliki trafik tinggi atau Revenue Corversion Rate yang tinggi (Mei, Maret, November, dan Desember).
- Dikarenakan persentase revenue New Visitor lebih besar (25%) dibandingkan Returning Visitor (14%), maka direkomendasikan untuk meningkatkan trafik untuk New Visitor, dengan cara:
    - Pemberian diskon khusus pengguna baru
    - Melakukan iklan di beberapa media untuk meningkatkan awareness masyarakat terhadap E-Commerce ini.<br>
<br>

---

#### Sumber
- *Gorunescu, F. (2011). Data Mining Concepts, Models and Techniques. Berlin:
Springer.*
- *Ku, YC and Tai, YM, "What Happens When Recommendation System Meets Reputation System? The Impact of Recommendation Information on Purchase Intention," 2013 46th Hawaii International Conference on System Sciences, 2013, pp. 1376-1383, doi: 10.1109/HICSS.2013.605.*
