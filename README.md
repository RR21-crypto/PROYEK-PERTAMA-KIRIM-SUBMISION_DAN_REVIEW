
 # Laporan Proyek Machine Learning - Rayhan Gibrani Uhum  



## Acknowledgements
dataset ini di download dari : https://finance.yahoo.com/quote/%5ERUT/history?p=%5ERUT


## Domain Proyek
Pasar FOREX (Foreign Exchange) adalah pasar keuangan global terbesar di dunia, yang dikenal dengan volatilitasnya yang tinggi dan perubahan harga yang cepat. Dalam menghadapi tantangan ini, banyak trader dan institusi keuangan telah beralih ke teknologi Machine Learning untuk membantu mereka mengambil keputusan perdagangan yang lebih baik.Hal ini di dukung dengan adanya resesi ekonomi yang sedang terjadi pada tahun 2023, yang membuat arah pasar dan saham yang semakin sulit di predikisi. 

![image](https://github.com/RR21-crypto/PROYEK-PERTAMA-KIRIM-SUBMISION_DAN_REVIEW/assets/81364035/51bafe16-c200-49e2-9a4a-e0fa391002c4)


Pasar saham seperti indeks Russell 2000 (^RUT) seringkali memiliki volatilitas yang tinggi dan perubahan harga yang cepat yang mana merupakan gabungan dari 2000 indeks pasar saham AS berkapitalisasi kecil yang membentuk 2.000 saham terkecil. Tentunya pasar saham ini yang akan menjadi salah satu korban atas resesi yang terjadi.Kita sebagai investor tentu ingin mengetahui arah pasar secara cepat dan tepat , yang mana menjadi kebutuhan. oleh sebab itu saya memilih saham Russel 2000 sebagai salah satu contoh untuk memperkirakan harga saham di dalam resesi yang terjadi di tahun 2023. metode yang saya pilih adalah metode Time series forecasting methode. Machine learning memiliki keunggulan yang dapat menjawan masalah yang telah saya sebutkan sebelumnya seperti Machine Learning memungkinkan trader untuk menganalisis data pasar dalam waktu nyata dan mendeteksi pola yang mungkin tidak terlihat oleh analisis manusia. Ini melibatkan penggunaan algoritma Machine Learning untuk memproses sejumlah besar data, termasuk data historis harga, indikator teknis, berita ekonomi, dan faktor-faktor lain yang memengaruhi pasar.

Salah satu aplikasi utama Machine Learning dalam trading FOREX adalah dalam meramalkan pergerakan harga mata uang. Dengan memanfaatkan data historis dan berbagai faktor penggerak pasar, model Machine Learning dapat menghasilkan prediksi harga yang lebih akurat. Hal ini dapat membantu trader dalam mengambil keputusan pembelian atau penjualan mata uang yang lebih tepat waktu.Salah satu cara yang dapat dilakukan adalah dengan menggunakan teknik forecasting.


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
    * Menangani missing value pada data
    * Mencari korelasi pada data untuk mencari dependant variable dan independent variable
    * Menangani outlier pada data dengan menggunakan IQR Method
    * Melakukan normalisasi pada data terutama pada fitur numerik
- Membuat model regresi untuk memprediksi bilangan kontinu untuk memprediksi harga yang akan datang. dalam projek ini kami menggunakn 3 algoritma yang memiliki kemampuan yang mumpuni dalam hal memperkirakan harga saham yang mana merupakan dalah satu goals kita , ke tiga saham tersebut adalah 
    - Support Vector Machine (Support Vector Regression)
    - K-Nearest Neighbors
    - Boosting Algorithm (Gradient Boosting Regression)

## Data Understanding
 untuk projek kali ini dataset yang akan digunakan adalah dataset dari https://finance.yahoo.com/quote/%5ERUT/history?period1=1535932800&period2=1693699200&interval=1d&filter=history&frequency=1d&includeAdjustedClose=true

 ![image](https://github.com/RR21-crypto/PROYEK-PERTAMA-KIRIM-SUBMISION_DAN_REVIEW/assets/81364035/6f45732b-1f81-43cb-99ac-f471708a489d)

|  Date  | Open | High | Low	 | Close | Adj Close | Volume |
| --- | --- | --- | --- | --- | --- | --- |
| 9/6/2022 | 1813.180 | 1815.150 | 1786.680 | 1792.3190 |1792.30 | 41273400 |
| 9/7/2022 | 1789.560 |1832.560 | 1787.430 | 1832.000 | 1832.0000 | 389030 |
| 9/8/2022 | 1857.14 | 1884.900 | 1857.140 | 1882.840 | 1882.840 | 390190 |

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

| Variable | Missing value |
| --- | --- |
| Date | 0 |
| Open | 0 |
| High | 12 |
| Low | 39 |
| Adj Close  | 0 |
| Volume | 0 |

 dalam mengerjakan projek ini untuk lebih memahami dataset yang telah dipilih terlihar kita mesti melakukan pengecekan terhadap data set yang kita gunakana .Untuk kasus ini dataset kita  memiliki beberapa missing value, dalam kasus ini kita memmiliki misiing value pada kolom High dan kolom Low. setelah mengetahui nilai yanh kosong , selanjutya menghadapi missing value memiliki 2 cara populer yaitu dihilangkan atau dengan mengisinya dengan menggunakan nilai mean (rata-rata).dalam projek ini saya memilih untuk mengisi missing value dengan menggunakan Simple Imputer. pemilihan Simple Imputer di  sebabkan sedikitnyay jumlah sample yang kita milki, tentu jika kita mendrop data yang  memiliki missing value akan mempengaruhi model yang kita kembangkan saat ini, oleh karena itu Simple Imputer menjadi pilihan kami dalam mengembanhkan model ini. 


## Data Preparation
### Menghapus fitur yang tidak diperlukan
dalam melakukan data preparation, menghapus fitur yang tidak  memiliki effect besar sangat di perlukan, dengan metode ini kita dapat membuat pelatihan kita menjadi lebih cepat dan effisien. 

di dalam projek ini kita menggunakan sns plot , untuk melihat keterkaitan satu fitur dengan fitur lain,dalam projek saya telah melampirkan dua cara melihatnya, yaitu dengan menggunakan sns plot dan menggunakan Correlation Matrix untuk Fitur Numerik.
![image](https://github.com/RR21-crypto/PROYEK-PERTAMA-KIRIM-SUBMISION_DAN_REVIEW/assets/81364035/8c4a28ac-ce6e-4138-ad27-9d198a1f38cf)

Correlation Matrix untuk Fitur Numerik sanagat mudah di pahami , dengan melihat jika angka lebih dekat ke 1 atau -1 maka keterkaitan antar 2 fitur tersebut sangat kuat dan saling berpengaruh . namun jika lebih dekat dengan 0 maka terjadi sebaliknya. namun disini kita harus membuat model yang lebih ringan dan mempercepat model kita mmeprkirakan nilai saham tentunya kita perlu membuang kolom atau feature yang tidak di perlukan. disini saya memutuskan untuk menghapus fitur Volume,Date .Disebabkan kedua fitur memiliki effect yang sangat kecil dengan Adj Close.  tentunya jika kita merujuk pada correlation tabble akan berlawanan, namun disini pemilihan kedua fitur ini di hapus tentu memiliki alasan. untuk penhapusan date ini disebabkan nilai yang di ambil di data ini memiliki nilai yang sama semua yaitu satu, hal itu disebabkakn nilai diambil perhari. seperti akan terlihat pada gambar di bawah.
![image](https://github.com/RR21-crypto/PROYEK-PERTAMA-KIRIM-SUBMISION_DAN_REVIEW/assets/81364035/961a9445-9823-4a10-8012-df152071e04c)
untuk penghapusan vitur volume ini akan merujuk pada gambar di bawah .Dimana kita dapat melihat bahwa semua numerik fitur memiliki bentuk yang mirip seiring bertambahnya sammple namun terjadi perbedaan dengan kolom numerik yang memiliki bentuk yang berbeda.
![image](https://github.com/RR21-crypto/PROYEK-PERTAMA-KIRIM-SUBMISION_DAN_REVIEW/assets/81364035/06bb9f98-c273-4dc3-b263-8fda560656ed)


### Spliting data set 

Kita akan membagi dataset menjadi 2 yaitu sebagai train data dan test data. Train data digunakan sebagai training model dan test data digunakan sebagai validasi apakah model sudah akurat atau belum. Proposi yang umum dalam splitting dataset adalah 80:20, 80% sebagai train data dan 20% sebagai test data, sehingga kita akan menggunakan proporsi tersebut.

### Data normaliszation

normalisasi adalah cara kita mensederhanakan fitur yang memiliki angka yang besar dan akan di transformasi dalam range 0 sampai dengan 1. dalam proyek ini kita akan menggunakna normaliszation dengan range 0 sampai dengan 1.Normalisasi data memiliki tujuan untuk membuat model lebih memahami dataset  kita dengan memiliki range yang sama, dalam hal normalisasi perlu dilakukan setelah terjadi spiliting data test , sehingga tidak terjadi kebocoran data dikarenakan kemampuaun dari normalisasi.


## Modeling
### K-Nearest Neighbors (K-NN):
algoritma knn adalah yang memiliki cara kerja dengan mmenggunakan ‘kesamaan fitur’ untuk memprediksi nilai dari setiap data yang baru. Dengan kata lain, setiap data baru diberi nilai berdasarkan seberapa mirip titik tersebut dalam set pelatihan. dalam kasus ini algoritma ini akan memilih sample dan membandingkannya. semakin banyak garis dan sample tentu akan meningkatkan akurasi kita . dalam projek ini saya menggunakan nilai K sebanyak 10, untuk kelebihan dan kekurangan dari algoritma ini sebagai berikut : 
Kelebihan:

- Sederhana: K-NN adalah algoritma yang relatif sederhana dan mudah dipahami. Ini adalah pilihan yang baik untuk pemula dalam machine learning.
- Non-Parametrik: Tidak ada asumsi yang diperlukan tentang distribusi data. Ini membuatnya cocok untuk berbagai jenis data.
- Dinamis: Model dapat menyesuaikan diri dengan perubahan data saat ini tanpa memerlukan pelatihan ulang.
Kekurangan:

- Sensitif terhadap Noise: K-NN rentan terhadap gangguan dan noise dalam data, yang dapat menghasilkan hasil yang tidak stabil.
- Komputasi Mahal: Perhitungan jarak antara titik data bisa mahal, terutama jika datasetnya besar.
- Kurangnya Interpretasi: Model K-NN tidak memberikan wawasan tentang faktor-faktor yang mendasari prediksi, sehingga sulit untuk memahami mengapa model mengambil keputusan tertentu.
  
### Random Forest:
algoritma Random forest merupakan algoritma yang menjalankan sejumlah Decision tree secara bersamaan  dari sample yang berbeda dalam data set yang sama.Dalam hal ini semakin banyak Decision tree yang kita gunakan tentu akan semakin bagus hal ini juga beresiko untuk over fitting.Dalam menentuka nilai yang di hasilkan oleh algoritma ini dalam projek ini , menggunakan nilai rata rata yang mana akan kita lihat hasilnya pada evaluasi model.
 Kelebihan:

- Akurasi Tinggi: Random Forest sering memberikan kinerja yang sangat baik dalam memprediksi dengan akurasi tinggi karena menggabungkan banyak pohon keputusan.
- Tidak Sensitif terhadap Overfitting: Kemampuan model ini untuk menangani overfitting adalah salah satu kekuatan utamanya.
- Mampu Memproses Data Besar: Random Forest mampu menangani dataset besar dan berbagai jenis data tanpa memerlukan banyak pra-pemrosesan.
Kekurangan:

- Kompleksitas Model: Karena model terdiri dari banyak pohon, Random Forest bisa menjadi kompleks dan sulit untuk diinterpretasi.
- Waktu Pelatihan: Proses pelatihan Random Forest mungkin memerlukan waktu yang lama, terutama jika terdapat banyak pohon atau fitur dalam dataset.
- Pemilihan Fitur: Random Forest cenderung memberikan bobot yang tinggi pada fitur yang umumnya informatif, sehingga fitur-fitur yang lebih jarang mungkin diabaikan.
### Boosting Algorithm (misalnya, AdaBoost, Gradient Boosting):
Algoritma ini merupakan algoritma yang mirip dengan random forest namun  yang mmebedakan adalah cara kerja dari algoritma ini. di random forest kita mengerjakan secara paralel dalam waktu bersama , namun hal ini kebalikan di boosting kita menjalankan model secara satu persatu , sehingga jika terjadi false akan di perbaiki di sesi selanjutnya. untuk kekurangan dan kelebihan algoritma ini sebagai berikut : 

Kelebihan:

- Akurasi yang Tinggi: Boosting Algorithm cenderung menghasilkan model dengan akurasi yang sangat tinggi karena fokus pada kasus yang sulit.
- Mampu Menangani Data yang Tidak Seimbang: Boosting cocok untuk menangani masalah kelas yang tidak seimbang.
- Interpretasi yang Baik: Model Boosting seringkali lebih mudah diinterpretasi daripada Random Forest karena mereka memberikan bobot pada fitur yang paling penting.
Kekurangan:

- Overfitting: Terlalu banyak iterasi dalam proses Boosting dapat menyebabkan overfitting jika tidak diatur dengan benar.
- Komputasi yang Mahal: Proses Boosting memerlukan perhitungan yang intensif, yang bisa memakan waktu dan sumber daya komputasi yang signifikan.
- Sensitif terhadap Noise: Seperti K-NN, Boosting Algorithm bisa cukup sensitif terhadap noise dalam data.

  
## Evaluation
Untuk evaluasi pada machine learning model ini, metrik yang digunakan adalah mean squared error (MSE). Dimana metrik ini mengukur seberapa dekat garis pas dengan titik data. Akurasi menentukan tingkat kemiripan antara hasil prediksi dengan nilai yang sebenarnya (y_test). Mean squared error (MSE) mengukur error dalam model statistik dengan cara menghitung rata-rata error dari kuadrat hasil aktual dikurang hasil prediksi. Berikut formulan MSE :

![image](https://github.com/RR21-crypto/PROYEK-PERTAMA-KIRIM-SUBMISION_DAN_REVIEW/assets/81364035/57517790-286e-4658-861e-21d71f111dec)

![image](https://github.com/RR21-crypto/PROYEK-PERTAMA-KIRIM-SUBMISION_DAN_REVIEW/assets/81364035/af742e8a-091a-409b-8860-3c0e52b6d173)

dalam proyek ini saya mendpatkan hasil dengan melakukan perbandingan antara ketiga algoritma yaitu Random Forest,K-Nearest Neighbo, Boosting Algorithm. di dapatkan bahwa algoritma rainforest merupakan algoritma dengan hasil prediksi yang mendekati dengan nilai asal yaitu 1848.7	

![image](https://github.com/RR21-crypto/PROYEK-PERTAMA-KIRIM-SUBMISION_DAN_REVIEW/assets/81364035/a08be2a2-ff81-4a0f-9fa9-c1f4616b6f42)

dari gambar di atas dapat di lihat ,dari ketiga perkiraan peforma dari algoritam rain forest menunjukan ketepatan prediksi yang mendekati dengan nilai aslinya. dari pembahasan yan gpanjang ini tentu hal ini akan sangat berhubunga dengan pasar forex.Sebagai trader tentu saja kebutuhan ketepatan dalam memperkirakan nilai menadi hal utama dalam kasus ini. Apalagi seperti yang saya katakan , ditengah resesi global perlu adanya analisa data  yang banyak untuk memperkirakan harga pasar. Dengan adanya model ini di harapkan mempermudah kerja Trader yang ingin invest pada saham Russel 2000.
