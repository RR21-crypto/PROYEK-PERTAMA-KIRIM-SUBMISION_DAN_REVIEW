
 # Laporan Proyek Machine Learning - Rayhan Gibrani Uhum  



## Acknowledgements
dataset ini di download dari : https://finance.yahoo.com/quote/%5ERUT/history?p=%5ERUT


## Domain Proyek
Pasar FOREX (Foreign Exchange) adalah pasar keuangan global terbesar di dunia, yang dikenal dengan volatilitasnya yang tinggi dan perubahan harga yang cepat. Dalam menghadapi tantangan ini, banyak trader dan institusi keuangan telah beralih ke teknologi Machine Learning untuk membantu mereka mengambil keputusan perdagangan yang lebih baik.

Pasar saham seperti indeks Russell 2000 (^RUT) seringkali memiliki volatilitas yang tinggi dan perubahan harga yang cepat. Oleh karena itu, penggunaan metode Machine Learning untuk forecasting time series dapat membantu trader dan investor dalam membuat keputusan yang lebih informasional.

Machine Learning memungkinkan trader untuk menganalisis data pasar dalam waktu nyata dan mendeteksi pola yang mungkin tidak terlihat oleh analisis manusia. Ini melibatkan penggunaan algoritma Machine Learning untuk memproses sejumlah besar data, termasuk data historis harga, indikator teknis, berita ekonomi, dan faktor-faktor lain yang memengaruhi pasar.

Salah satu aplikasi utama Machine Learning dalam trading FOREX adalah dalam meramalkan pergerakan harga mata uang. Dengan memanfaatkan data historis dan berbagai faktor penggerak pasar, model Machine Learning dapat menghasilkan prediksi harga yang lebih akurat. Hal ini dapat membantu trader dalam mengambil keputusan pembelian atau penjualan mata uang yang lebih tepat waktu.Salah satu cara yang dapat dilakukan adalah dengan menggunakan teknik forecasting.

Forecasting adalah suatu teknik untuk meramalkan keadaan dimasa yang akan datang dengan menggunakan data-data yang telah ada di masa lalu. Hal ini termasuk dalam time series forecasting, dengan mendeteksi pola dan kecenderungan data time series kemudian memformulasikannya dalam suatu model, maka dapat digunakan untuk memprediksi data yang akan datang.


## BUSINESS UNDERSTANDING 
### Goals

Tujuan proyek ini dibuat adalah sebagai berikut :

- Dapat memprediksi harga forex dengan akurat menggunakan model machine learning
- Melakukan analisa dan mengolah data yang optimal agar diterima dengan baik oleh model machine learning.
- Membantu para trader dalam melakukan transaksi pada forex   market

Solution Statement
Solusi yang dapat dilakukan agar goals terpenuhi adalah sebagai berikut :

- Melakukan analisa, eksplorasi, pemrosesan pada data dengan memvisualisasikan data agar mendapat gambaran bagaimana data tersebut. Berikut adalah analisa yang dapat dilakukan :
    * Menangani missing value pada data
    * Mencari korelasi pada data untuk mencari dependant variable dan independent variable
    * Menangani outlier pada data dengan menggunakan IQR Method
    * Melakukan normalisasi pada data terutama pada fitur numerik
- Membuat model regresi untuk memprediksi bilangan kontinu untuk memprediksi harga yang akan datang. Berikut beberapa algoritma yang digunakan pada proyek ini :
    - Support Vector Machine (Support Vector Regression)
    - K-Nearest Neighbors
    - Boosting Algorithm (Gradient Boosting Regression)

## Data Understanding
 untuk projek kali ini dataset yang akan digunakan adalah dataset dari https://finance.yahoo.com/quote/%5ERUT/history?period1=1535932800&period2=1693699200&interval=1d&filter=history&frequency=1d&includeAdjustedClose=true

data set yang kitamerupakan data set dari Sep 04, 2018 - Sep 04, 2023 pada Russell 2000 (^RUT) yang memmiliki 1258 sample dan 7 kolom diantaranya :
- date : tanggal data terekam
- open : Harga pembukaan pada hari tersebut
- High : harga tertinggi pada hari itu

- LOw : Harga terendah pada hari tersebut

- Close : Harga penutupan pada hari tersebut item

- Adj Close : Harga penutupan pada hari tersebut setelah disesuaikan dengan aksi korporasi seperti right issue, stock split atau stock reverse

- volume : berapa banyak transaksi yang terjadi pada hari tersebut
dari 7 kolom diatas memiliki missing value pada High sebanyak 12 sample dan pada Low sebanyak 39 sample. 

### Exploratory Data Analysis
 dalam mengerjakan projek ini untuk lebih memahami dataset yang telah dipilih , kami menggunakan comand df.shape , df.describe(),df.info() dan df.head().

 setelah kita mengetahui data  yang kita miliki secara garis besar untuk mencek apakah dataset kita memiliki nilai kosong (Null).Command yang di gunakan adalah df.null().

 setelah mengetahui nilai yanh kosong , selanjutya menghadapi missing value memiliki 2 cara populer yaitu dihilangkan atau dengan mengisinya dengan menggunakan nilai mean (rata-rata).

 dalam projek ini saya memilih untuk mengisi missing value dengan menggunakan Simple Imputer.

 from sklearn.impute import SimpleImputer

pengisi = SimpleImputer()

df[kolom_kosong]=pengisi.fit_transform(df[kolom_kosong]) 





## Data Preparation
### Menghapus fitur yang tidak diperlukan
dalam melakukan data preparation, menghapus fitur yang tidak  memiliki effect besar sangat di perlukan, dengan metode ini kita dapat membuat pelatihan kita menjadi lebih cepat dan effisien. 

di dalam projek ini kita menggunakan sns plot , untuk melihat keterkaitan satu fitur dengan fitur lain,dalam projek saya telah melampirkan dua cara melihatnya, yaitu dengan menggunakan sns plot dan menggunakan Correlation Matrix untuk Fitur Numerik.

Correlation Matrix untuk Fitur Numerik sanagat mudah di pahami , dengan melihat jika angka lebih dekat ke 1 atau -1 maka keterkaitan antar 2 fitur tersebut sangat kuat dan saling berpengaruh . namun jika lebih dekat dengan 0 maka terjadi sebaliknya. 

setelah melakukan visualisasi. saya memutuskan untuk menghapus fitur Volume,Date .Disebabkan kedua fitur memiliki effect yang sangat kecil dengan Adj Close. 

### Spliting data set 

Kita akan membagi dataset menjadi 2 yaitu sebagai train data dan test data. Train data digunakan sebagai training model dan test data digunakan sebagai validasi apakah model sudah akurat atau belum. Proposi yang umum dalam splitting dataset adalah 80:20, 80% sebagai train data dan 20% sebagai test data, sehingga kita akan menggunakan proporsi tersebut.

### Data normaliszation

normalisasi adalah cara kita mensederhanakan fitur yang memiliki angka yang besar dan akan di transformasi dalam range 0 sampai dengan 1. dalam proyek ini kita akan menggunakna normaliszation dengan range 0 sampai dengan 1.


## Modeling
### K-Nearest Neighbors (K-NN):

Kelebihan:

- Sederhana: K-NN adalah algoritma yang relatif sederhana dan mudah dipahami. Ini adalah pilihan yang baik untuk pemula dalam machine learning.
- Non-Parametrik: Tidak ada asumsi yang diperlukan tentang distribusi data. Ini membuatnya cocok untuk berbagai jenis data.
- Dinamis: Model dapat menyesuaikan diri dengan perubahan data saat ini tanpa memerlukan pelatihan ulang.
Kekurangan:

- Sensitif terhadap Noise: K-NN rentan terhadap gangguan dan noise dalam data, yang dapat menghasilkan hasil yang tidak stabil.
- Komputasi Mahal: Perhitungan jarak antara titik data bisa mahal, terutama jika datasetnya besar.
- Kurangnya Interpretasi: Model K-NN tidak memberikan wawasan tentang faktor-faktor yang mendasari prediksi, sehingga sulit untuk memahami mengapa model mengambil keputusan tertentu.
### Random Forest:

 Kelebihan:

- Akurasi Tinggi: Random Forest sering memberikan kinerja yang sangat baik dalam memprediksi dengan akurasi tinggi karena menggabungkan banyak pohon keputusan.
- Tidak Sensitif terhadap Overfitting: Kemampuan model ini untuk menangani overfitting adalah salah satu kekuatan utamanya.
- Mampu Memproses Data Besar: Random Forest mampu menangani dataset besar dan berbagai jenis data tanpa memerlukan banyak pra-pemrosesan.
Kekurangan:

- Kompleksitas Model: Karena model terdiri dari banyak pohon, Random Forest bisa menjadi kompleks dan sulit untuk diinterpretasi.
- Waktu Pelatihan: Proses pelatihan Random Forest mungkin memerlukan waktu yang lama, terutama jika terdapat banyak pohon atau fitur dalam dataset.
- Pemilihan Fitur: Random Forest cenderung memberikan bobot yang tinggi pada fitur yang umumnya informatif, sehingga fitur-fitur yang lebih jarang mungkin diabaikan.
Boosting Algorithm (misalnya, AdaBoost, Gradient Boosting):

Kelebihan:

- Akurasi yang Tinggi: Boosting Algorithm cenderung menghasilkan model dengan akurasi yang sangat tinggi karena fokus pada kasus yang sulit.
- Mampu Menangani Data yang Tidak Seimbang: Boosting cocok untuk menangani masalah kelas yang tidak seimbang.
- Interpretasi yang Baik: Model Boosting seringkali lebih mudah diinterpretasi daripada Random Forest karena mereka memberikan bobot pada fitur yang paling penting.
Kekurangan:

- Overfitting: Terlalu banyak iterasi dalam proses Boosting dapat menyebabkan overfitting jika tidak diatur dengan benar.
- Komputasi yang Mahal: Proses Boosting memerlukan perhitungan yang intensif, yang bisa memakan waktu dan sumber daya komputasi yang signifikan.
- Sensitif terhadap Noise: Seperti K-NN, Boosting Algorithm bisa cukup sensitif terhadap noise dalam data.
## Evaluation
Untuk evaluasi pada machine learning model ini, metrik yang digunakan adalah mean squared error (mse). Dimana metrik ini mengukur seberapa dekat garis pas dengan titik data.
 
dalam proyek ini saya mendpatkan hasil dengan melakukan perbandingan antara ketiga algoritma yaitu Random Forest,K-Nearest Neighbo, Boosting Algorithm. di dapatkan bahwa algoritma rainforest merupakan algoritma dengan hasil prediksi yang mendekati dengan nilai asal yaitu 1968,4.