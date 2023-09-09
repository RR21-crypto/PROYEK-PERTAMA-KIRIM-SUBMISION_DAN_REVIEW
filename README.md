
 # Laporan Proyek Machine Learning - Rayhan Gibrani Uhum  



## Acknowledgements
dataset ini di download dari : https://finance.yahoo.com/quote/%5ERUT/history?p=%5ERUT


## Domain Proyek
Pasar FOREX (Foreign Exchange) adalah pasar keuangan global terbesar di dunia, yang dikenal dengan volatilitasnya yang tinggi dan perubahan harga yang cepat. Dalam menghadapi tantangan ini, banyak trader dan institusi keuangan telah beralih ke teknologi _Machine Learning_ untuk membantu mereka mengambil keputusan perdagangan yang lebih baik.Hal ini di dukung dengan adanya resesi ekonomi yang sedang terjadi pada tahun 2023, yang membuat arah pasar dan saham yang semakin sulit di predikisi. 

![image](https://github.com/RR21-crypto/PROYEK-PERTAMA-KIRIM-SUBMISION_DAN_REVIEW/assets/81364035/51bafe16-c200-49e2-9a4a-e0fa391002c4)


Pasar saham seperti indeks Russell 2000 (^RUT) seringkali memiliki volatilitas yang tinggi dan perubahan harga yang cepat yang mana merupakan gabungan dari 2000 indeks pasar saham AS berkapitalisasi kecil yang membentuk 2.000 saham terkecil. Tentunya pasar saham ini yang akan menjadi salah satu korban atas resesi yang terjadi. sebagai investor tentu ingin mengetahui arah pasar secara cepat dan tepat , yang mana menjadi kebutuhan. oleh sebab itu projek ini  memilih saham Russel 2000 sebagai salah satu contoh untuk memperkirakan harga saham di dalam resesi yang terjadi di tahun 2023. metode  dipilih adalah metode _Time series forecasting method_. _Machine learning_ memiliki keunggulan yang dapat menjawab masalah yang telah di sebutkan sebelumnya seperti _Machine Learning_ memungkinkan trader untuk menganalisis data pasar dalam waktu nyata dan mendeteksi pola yang mungkin tidak terlihat oleh analisis manusia. Ini melibatkan penggunaan algoritma _Machine Learning_ untuk memproses sejumlah besar data, termasuk data historis harga, indikator teknis, berita ekonomi, dan faktor-faktor lain yang memengaruhi pasar.

Salah satu aplikasi utama Machine Learning dalam trading FOREX adalah dalam meramalkan pergerakan harga mata uang. Dengan memanfaatkan data historis dan berbagai faktor penggerak pasar, model _Machine Learning_ dapat menghasilkan prediksi harga yang lebih akurat. Hal ini dapat membantu trader dalam mengambil keputusan pembelian atau penjualan mata uang yang lebih tepat waktu.Salah satu cara yang dapat dilakukan adalah dengan menggunakan teknik _forecasting_.


## BUSINESS UNDERSTANDING 
### Goals

Tujuan proyek ini dibuat adalah sebagai berikut :

- membantu trader yang ingin invest di saham Russel 2000
- memberikan perkiraan kepada trader di tengah resesi ekonomi global  untuk saham Russel 2000 

### Problem Statement
- Fitur apa saja yang mempengaruhi dalam naik dan turunnya harga suatu saham terkhusus Russell 2000 ?
- agoritma apa yang paling tepat untuk memperkirakan harga saham Russel 2000 ?

### Solution Statement
Solusi yang dapat dilakukan agar goals terpenuhi adalah sebagai berikut :

- Melakukan analisa, eksplorasi, pemrosesan pada data dengan memvisualisasikan data agar mendapat gambaran bagaimana data tersebut. Berikut adalah analisa yang dapat dilakukan :
    * Menangani _missing value_ pada data
    * Mencari korelasi pada data untuk mencari _dependant variable_ dan _independent variable_
    * Menangani outlier pada data dengan menggunakan _IQR Method_
    * Melakukan normalisasi pada data terutama pada fitur numerik
- Membuat model regresi untuk memprediksi bilangan kontinu untuk memprediksi harga yang akan datang. dalam projek ini  menggunakan 3 algoritma yang memiliki kemampuan yang mumpuni dalam hal memperkirakan harga saham yang  merupakan adalah satu goals  , ke tiga saham tersebut adalah 
    - Support Vector Machine (Support Vector Regression)
    - K-Nearest Neighbors
    - Boosting Algorithm (Gradient Boosting Regression)

## Data Understanding
 untuk projek kali ini dataset yang akan digunakan adalah dataset dari https://finance.yahoo.com/quote/%5ERUT/history?period1=1535932800&period2=1693699200&interval=1d&filter=history&frequency=1d&includeAdjustedClose=true


|  Date  | Open | High | Low	 | Close | Adj Close | Volume |
| --- | --- | --- | --- | --- | --- | --- |
| 9/6/2022 | 1813.180 | 1815.150 | 1786.680 | 1792.3190 |1792.30 | 41273400 |
| 9/7/2022 | 1789.560 |1832.560 | 1787.430 | 1832.000 | 1832.0000 | 389030 |
| 9/8/2022 | 1857.14 | 1884.900 | 1857.140 | 1882.840 | 1882.840 | 390190 |

data set merupakan data set dari Sep 04, 2018 - Sep 04, 2023 pada Russell 2000 (^RUT) yang memmiliki 1258 sample dan 7 kolom diantaranya :
- date : tanggal data terekam
- open : Harga pembukaan pada hari tersebut
- High : harga tertinggi pada hari itu

- LOw : Harga terendah pada hari tersebut

- Close : Harga penutupan pada hari tersebut item

- Adj Close : Harga penutupan pada hari tersebut setelah disesuaikan dengan aksi korporasi seperti right issue, stock split atau stock reverse

- volume : berapa banyak transaksi yang terjadi pada hari tersebut
dari 7 kolom diatas memiliki missing value pada High sebanyak 12 sample dan pada Low sebanyak 39 sample.

setelah mengetahui mengenai data set yang di miliki ,  akan lebih mudah  memahami data jika melihat data dalam bentuk  ilustrasi.
![image](https://github.com/RR21-crypto/PROYEK-PERTAMA-KIRIM-SUBMISION_DAN_REVIEW/assets/81364035/06bb9f98-c273-4dc3-b263-8fda560656ed)

dari gambar diatas terlihat bahwa semua data memiliki bentuk yang sama atau mirip , namun berbeda dengan plot untuk Volume , dari gambar plot ini dapat mengindikasikan bahwa Volume memiliki keterkaitan dengan feature lain sangat lemah , untuk membuktikannya  akan dilihat di pembahasan selanjutnya.


### Exploratory Data Analysis

| Variable | Missing value |
| --- | --- |
| Date | 0 |
| Open | 0 |
| High | 12 |
| Low | 39 |
| Adj Close  | 0 |
| Volume | 0 |

 dalam mengerjakan projek ini untuk lebih memahami dataset yang telah dipilih , tentunya mesti melakukan pengecekan terhadap data set yang di gunakana .Untuk kasus ini dataset  memiliki beberapa _missing value_, dalam kasus ini ,memiliki _missing value_ pada kolom High dan kolom Low. setelah mengetahui nilai yang kosong , selanjutya menghadapi _missing value_ memiliki 2 cara populer yaitu dihilangkan atau dengan mengisinya dengan menggunakan nilai _mean_ (rata-rata).dalam projek ini penangannanya masalah ini dengan  memilih untuk mengisi _missing value_ dengan menggunakan *Simple Imputer*. pemilihan *Simple Imputer* di  sebabkan  jumlah sample yang tersedia, tentu jika membuang / _drop_ data yang  memiliki missing value akan mempengaruhi model yang di kembangkan saat ini, oleh karena itu *Simple Imputer* menjadi pilihan  dalam mengembangkan model ini. 


## Data Preparation
### Menghapus fitur yang tidak diperlukan
dalam melakukan data preparation, menghapus fitur yang tidak  memiliki effect besar sangat di perlukan, dengan metode ini  dapat membuat pelatihan model  menjadi lebih cepat dan _effisien_. 

di dalam projek ini  menggunakan _sns plot_ , untuk melihat keterkaitan satu fitur dengan fitur lain,dalam projek ini telah melampirkan dua cara melihatnya, yaitu dengan menggunakan sns plot dan menggunakan Correlation Matrix untuk Fitur Numerik.
![image](https://github.com/RR21-crypto/PROYEK-PERTAMA-KIRIM-SUBMISION_DAN_REVIEW/assets/81364035/8c4a28ac-ce6e-4138-ad27-9d198a1f38cf)

_Correlation Matrix_ untuk Fitur Numerik sanagat mudah di pahami , dengan melihat jika angka lebih dekat ke 1 atau -1 maka keterkaitan antar 2 fitur tersebut sangat kuat dan saling berpengaruh . namun jika lebih dekat dengan 0 maka terjadi sebaliknya. namun disini tujuan utama adalah  membuat model yang lebih ringan dan mempercepat model untuk  memperkirakan nilai saham, tentunya  perlu membuang kolom atau _feature_ yang tidak di perlukan. disini fitur yang dihapus adalah  fitur _Volume_,_Date_ .Disebabkan kedua fitur memiliki _effect_ yang sangat kecil dengan _Adj Close_.  tentunya jika merujuk pada _correlation tabble_ akan berlawanan, namun disini pemilihan kedua fitur ini di hapus tentu memiliki alasan. untuk penghapusan _date_ ini disebabkan nilai yang di ambil di data ini memiliki nilai yang sama semua yaitu satu, hal itu disebabkakn nilai diambil perhari.

untuk penghapusan fitur _volume_ ini akan merujuk pada gambar di bawah .Dimana  dapat dilihat bahwa semua numerik fitur memiliki bentuk yang mirip seiring bertambahnya _sample_ namun terjadi perbedaan dengan kolom numerik yang memiliki bentuk yang berbeda.
![image](https://github.com/RR21-crypto/PROYEK-PERTAMA-KIRIM-SUBMISION_DAN_REVIEW/assets/81364035/06bb9f98-c273-4dc3-b263-8fda560656ed)


### Spliting data set 

Projek membagi _dataset_ menjadi 2 yaitu sebagai _train data_ dan _test data_. Train data digunakan sebagai training model dan test data digunakan sebagai validasi apakah model sudah akurat atau belum. Proposi yang umum dalam splitting dataset adalah 80:20, 80% sebagai train data dan 20% sebagai test data.

### Data normaliszation

normalisasi adalah cara  menyederhanakan fitur yang memiliki angka yang besar dan akan di transformasi dalam range 0 sampai dengan 1. dalam proyek ini  akan menggunakan _normaliszation_ dengan range 0 sampai dengan 1.Normalisasi data memiliki tujuan untuk membuat model lebih memahami _dataset_   dengan memiliki range yang sama, dalam hal normalisasi perlu dilakukan setelah terjadi _spiliting data test_ , sehingga tidak terjadi kebocoran data dikarenakan kemampuaun dari normalisasi.


## Modeling
### K-Nearest Neighbors (K-NN):
algoritma knn adalah yang memiliki cara kerja dengan mmenggunakan ‘kesamaan fitur’ untuk memprediksi nilai dari setiap data yang baru. Dengan kata lain, setiap data baru diberi nilai berdasarkan seberapa mirip titik tersebut dalam set pelatihan. dalam kasus ini algoritma ini akan memilih sample dan membandingkannya. semakin banyak garis dan sample tentu akan meningkatkan akurasi  . dalam projek ini akan  menggunakan nilai K sebanyak 10, untuk kelebihan dan kekurangan dari algoritma ini sebagai berikut : 
Kelebihan:

- Sederhana: K-NN adalah algoritma yang relatif sederhana dan mudah dipahami. Ini adalah pilihan yang baik untuk pemula dalam machine learning.
- Non-Parametrik: Tidak ada asumsi yang diperlukan tentang distribusi data. Ini membuatnya cocok untuk berbagai jenis data.
- Dinamis: Model dapat menyesuaikan diri dengan perubahan data saat ini tanpa memerlukan pelatihan ulang.
Kekurangan:

- Sensitif terhadap Noise: K-NN rentan terhadap gangguan dan noise dalam data, yang dapat menghasilkan hasil yang tidak stabil.
- Komputasi Mahal: Perhitungan jarak antara titik data bisa mahal, terutama jika datasetnya besar.
- Kurangnya Interpretasi: Model K-NN tidak memberikan wawasan tentang faktor-faktor yang mendasari prediksi, sehingga sulit untuk memahami mengapa model mengambil keputusan tertentu.

  
### Random Forest:
algoritma Random forest merupakan algoritma yang menjalankan sejumlah _Decision tree_ secara bersamaan  dari sample yang berbeda dalam data set yang sama.Dalam hal ini semakin banyak _Decision tree_ yang digunakan tentu akan semakin bagus hal ini juga beresiko untuk _over fitting_.Dalam menentuka nilai yang di hasilkan oleh algoritma ini dalam projek ini , menggunakan nilai rata rata yang mana akan terlihat hasilnya pada evaluasi model. dalam projek ini  menggunakan parameter untuk membangun model ini diantaranya : 
- n_estimator: jumlah _trees_ (pohon) di forest. Di sini  set n_estimator=50.
- max_depth: kedalaman atau panjang pohon. Ia merupakan ukuran seberapa banyak pohon dapat membelah (splitting) untuk membagi setiap node ke dalam jumlah pengamatan yang diinginkan.
- random_state: digunakan untuk mengontrol random number generator yang digunakan.
- n_jobs: jumlah _job_ (pekerjaan) yang digunakan secara paralel

Setelah mengetahui parameter pada kode , tentunya algoritma ini memiliki beberapa kekurangan dan kelebihan diantaranya : 

 Kelebihan:

- Akurasi Tinggi: _Random Forest_ sering memberikan kinerja yang sangat baik dalam memprediksi dengan akurasi tinggi karena menggabungkan banyak pohon keputusan.
- Tidak Sensitif terhadap _Overfitting_: Kemampuan model ini untuk menangani overfitting adalah salah satu kekuatan utamanya.
- Mampu Memproses Data Besar: Random Forest mampu menangani dataset besar dan berbagai jenis data tanpa memerlukan banyak pra-pemrosesan.
Kekurangan:

- Kompleksitas Model: Karena model terdiri dari banyak pohon, _Random Forest_ bisa menjadi kompleks dan sulit untuk diinterpretasi.
- Waktu Pelatihan: Proses pelatihan Random Forest mungkin memerlukan waktu yang lama, terutama jika terdapat banyak pohon atau fitur dalam dataset.
- Pemilihan Fitur: Random Forest cenderung memberikan bobot yang tinggi pada fitur yang umumnya informatif, sehingga fitur-fitur yang lebih jarang mungkin diabaikan.

### Boosting Algorithm (misalnya, AdaBoost, Gradient Boosting):
Algoritma ini merupakan algoritma yang mirip dengan random forest namun  yang mmebedakan adalah cara kerja dari algoritma ini. di random forest  mengerjakan secara paralel dalam waktu bersama , namun hal ini kebalikan di boosting   akan menjalankan model secara satu persatu , sehingga jika terjadi _false_ akan di perbaiki di sesi selanjutnya. Untuk menjalankan algoritma ini tentunya membutuhkan  beberapa paramerter  dalam kode , parameter yang digunakan adalah
 - ***learning _ rate*** yang berfungsiuntuk menetaplan bobot pada setiap regresor pada saat iterasi boosting nilai yang digunakan adalah 1.0
 -  ***random_state*** digunakan untuk mengontrol random number yang di gunakan.
 - *** n_estimators*** fungsinya sama dengan _Random Forest_ dikarenakan tak disebut nilainya menjadi 50
 - max_depth: kedalaman atau panjang pohon. Ia merupakan ukuran seberapa banyak pohon dapat membelah (splitting) untuk membagi setiap node ke dalam jumlah pengamatan yang diinginkan. dalam hal ini dikarenakan tak disebut nilainya akan _max_depth_ = 3

untuk kekurangan dan kelebihan algoritma ini sebagai berikut : 

Kelebihan:

- Akurasi yang Tinggi: _Boosting Algorithm_ cenderung menghasilkan model dengan akurasi yang sangat tinggi karena fokus pada kasus yang sulit.
- Mampu Menangani Data yang Tidak Seimbang: Boosting cocok untuk menangani masalah kelas yang tidak seimbang.
- Interpretasi yang Baik: Model _Boosting_ seringkali lebih mudah diinterpretasi daripada _Random Forest_ karena mereka memberikan bobot pada fitur yang paling penting.
Kekurangan:

- Overfitting: Terlalu banyak iterasi dalam proses Boosting dapat menyebabkan _overfitting_ jika tidak diatur dengan benar.
- Komputasi yang Mahal: Proses Boosting memerlukan perhitungan yang intensif, yang bisa memakan waktu dan sumber daya komputasi yang signifikan.
- Sensitif terhadap Noise: Seperti K-NN, _Boosting Algorithm_ bisa cukup sensitif terhadap noise dalam data.

  
## Evaluation
Untuk evaluasi pada machine learning model ini, metrik yang digunakan adalah mean squared error (MSE). Dimana metrik ini mengukur seberapa dekat garis pas dengan titik data. Akurasi menentukan tingkat kemiripan antara hasil prediksi dengan nilai yang sebenarnya (y_test). Mean squared error (MSE) mengukur error dalam model statistik dengan cara menghitung rata-rata error dari kuadrat hasil aktual dikurang hasil prediksi. Berikut formulan MSE :

![image](https://github.com/RR21-crypto/PROYEK-PERTAMA-KIRIM-SUBMISION_DAN_REVIEW/assets/81364035/57517790-286e-4658-861e-21d71f111dec)

![image](https://github.com/RR21-crypto/PROYEK-PERTAMA-KIRIM-SUBMISION_DAN_REVIEW/assets/81364035/af742e8a-091a-409b-8860-3c0e52b6d173)

 tentunya terjadi perbedaan. perbedaan ini lah yang di sebut sebagai _eror_.Dalam hal ini  dapat dihitung secara manual dengan formula yang di atas.Dalam projek ini setiap algoritma memiliki _eror_ yang berbeda , nilai _eror_ akan di tampilkan dalam betuk table di bawah 

| | RF | KNN | Boosting |
| --- | --- | --- | --- |
|test | 0.05 | 0.11 | 0.32 |
| train | 0.01 | 0.1 | 0.13 |



dalam proyek ini hasil dengan melakukan perbandingan antara ketiga algoritma yaitu Random _Forest,K-Nearest Neighbor, Boosting Algorithm_. di dapatkan bahwa algoritma rainforest merupakan algoritma dengan hasil prediksi yang mendekati dengan nilai asal yaitu 202. 

|  | y_true | prediksi_KNN | prediksi_RF	 | prediksi_Boosting |
| --- | --- | --- | --- | --- |  
| 202 | 1849.930054	 | 1848.9| 1848.7 | 1854.0 |
|163| 1769.209961 |1770.3	 | 1768.8 | 1764 | 
| 146 | 1752.130005 | 1754.1	 | 1752.5 | 1759.7 | 


dari gambar di atas dapat di lihat ,dari ketiga perkiraan peforma dari  _Random forest_ menunjukan ketepatan prediksi yang mendekati dengan nilai aslinya, hal ini selaras dengan tabel MSE yang memperlihatkan bahwa algoritma ** Rain Forest ** adalah paling terkecil diantara kedua algoritma lain . dari pembahasan yang panjang ini tentu hal ini akan sangat berhubungan dengan pasar forex.Sebagai trader tentu saja kebutuhan ketepatan dalam memperkirakan nilai menadi hal utama dalam kasus ini. Apalagi seperti yang  di katakan sebelumnya , ditengah resesi global perlu adanya analisa data  yang banyak untuk memperkirakan harga pasar. Dengan adanya model ini di harapkan mempermudah kerja Trader yang ingin _invest_ pada saham Russel 2000.
