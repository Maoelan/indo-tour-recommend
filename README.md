# Laporan Proyek Akhir Machine Learning - Maulana Muhammad

## Parawisata - Rekomendasi Destinasi Wisata Turis di Indonesia

![indonesia-travel-attraction-landmarks-tourism-traditional-culture-91162722](https://user-images.githubusercontent.com/58927608/229541740-616aef88-1faa-4d1c-8859-d34a30e9f412.jpg)
[Sumber Gambar](https://www.dreamstime.com/stock-illustration-indonesia-travel-attraction-landmarks-tourism-traditional-culture-image91162722)

Pariwisata di Indonesia merupakan sektor ekonomi penting di Indonesia. Pada tahun 2009, pariwisata menempati urutan ketiga dalam hal penerimaan devisa setelah komoditas minyak dan gas bumi serta minyak kelapa sawit. Berdasarkan data tahun 2016, jumlah wisatawan mancanegara yang datang ke Indonesia sebesar 11.525.963 juta lebih atau tumbuh sebesar 10,79% dibandingkan tahun sebelumnya.
  
Berdasarkan data dari Badan Pusat Statistik, sebelas provinsi yang paling sering dikunjungi oleh para turis adalah Bali sekitar lebih dari 3,7 juta disusul, DKI Jakarta, Daerah Istimewa Yogyakarta, Jawa Timur, Jawa Barat, Sumatra Utara, Lampung, Sulawesi Selatan, Sumatra Selatan, Banten dan Sumatra Barat.

Sekitar 59% turis berkunjung ke Indonesia untuk tujuan liburan, sementara 38% untuk tujuan bisnis. Singapura dan Malaysia adalah dua negara dengan catatan jumlah wisatawan terbanyak yang datang ke Indonesia dari wilayah ASEAN. Sementara dari kawasan Asia (tidak termasuk ASEAN) wisatawan Tiongkok berada di urutan pertama disusul Jepang, Korea Selatan, Taiwan dan India. Jumlah pendatang terbanyak dari kawasan Eropa berasal dari negara Britania Raya disusul oleh Belanda, Jerman dan Prancis.

## Business Understanding

Pariwisata atau turisme adalah suatu perjalanan yang dilakukan untuk rekreasi atau liburan dan juga persiapan yang dilakukan untuk aktivitas ini. Sedangkan seorang wisatawan atau biasa disebut tirus merupakan seorang yang melakukan perjalanan setidaknya paling tidak sejauh 80 km dari tempat tinggalnya. Parawisata di Indonesia merupakan sektor penting karena sektor ini merupakan salah satu penyumpang devisa negara yang paling besar. Untuk para wisatawan atau turis melakukan wisata di Indonesia merupakan hal yang menyenangkan karena banyaknya wisata di Indonesia seakan tidak ada habisnya. Karena keanekaragaman wisata di Indonesia sangat banyak, ini juga dapat menimbulkan masalah, karena wisatawan atau turis yang ingin melakukan perjalanan wisata menjadi bingung untuk memulai dari mana. Oleh karena itu dibuatlah sistem rekomendasi untuk merekomendasikan wisatawan atau turis berdasarkan informasi masa lalu yaitu berupa tempat wisata yang pernah dikunjungi dan rekomendasi berdasarkan rating dari tempat wisata.

### Problem Statement

Menjelaskan pernyataan masalah latar belakang:
- Berdasarkan data wisatawan atau turis, bagaimana membuat sistem rekomendasi yang dipersonalisasi dengan teknik *content-based filtering?*
- Dengan data rating dari wisatawan atau turis, bagaimana cara untuk merekomendasikan destinasi wisata lain yang mungkin disukai oleh wisatawan atau turis yang tidak pernah mengunjungi tempat tersebut?

### Goals

Menjelaskan tujuan dari pernyataan masalah:
- Menghasilkan rekomendasi destinasi parawisata yang dipersonalisasi untuk wisatawan atau turis dengan *content-based filtering*.
- Menghasilkan rekomendasi destinasi wisata yang sesuai dengan preferensi wisatawan atau turis yang belum pernah dikunjungi sebelumnya dengan *collaborative filtering*.

    ### Solution statements
    - Menggunakan *cosine similarity* untuk melakukan rekomendasi *content-based filtering* dengan mencari kemaripan antar data.
    - Membuat class RecommenderNet dengan keras Model Class untuk melakukan rekomendasi menggunakan *collaborative filtering* berdasarkan rating wisatawan atau turis. 

## Content Based Filtering - Berdasarkan data wisatawan atau turis yang telah berkunjung ke tempat serupa sebelumnya 

## Data Understanding
Dataset : [Indonesia Tourism Destination](https://www.kaggle.com/datasets/aprabowo/indonesia-tourism-destination)

**Overview**

- Nama dataset : Indonesia Tourism Destination
- Jumlah file terdiri dari :
  - package_tourism.csv
  - tourism_rating.csv
  - tourism_with_id.csv
  - user.csv
- Jumlah kolom terdiri dari :
  - package_tourism.csv : 7
  - tourism_rating.csv : 3
  - tourism_with_id.csv : 12
  - user.csv : 3
- Jumlah data terdiri dari : 
  - package_tourism.csv : 100
  - tourism_rating.csv : 10000
  - tourism_with_id.csv : 437
  - user.csv : 300
- Usability : 8.24
- License : Data files © Original Authors (A_PRABOWO)
- Date Updated : 21 July 2021

### Variabel-variabel pada CO2 Emission by Vehicles dataset adalah sebagai berikut:
*   Variabel pada package_tourism.csv
    *   Package : Paket destinasi wisata
    *   City : Kota pada paket destinasi wisata
    *   Place_Tourism1 : Tempat destinasi wisata pertama
    *   Place_Tourism2 : Tempat destinasi wisata kedua
    *   Place_Tourism3 : Tempat destinasi wisata ketiga
    *   Place_Tourism4 : Tempat destinasi wisata keempat
    *   Place_Tourism5 : Tempat destinasi wisata kelima
*   Variabel pada tourism_rating.csv
    *   User_Id : Id wisatawan atau turis
    *   Place_Id : Id tempat wisata
    *   Place_Ratings : Rating tempat wisata
*   Variabel pada tourism_with_id.csv
    *   Place_Id : Id tempat wisata
    *   Place_Name : Nama tempat wisata
    *   Description : Deskripsi tempat wisata
    *   Category : Kategori tempat wisata
    *   City : Kota tempat wisata berada
    *   Price : Harga tempat wisata
    *   Rating : Rating tempat wisata
    *   Time_Minutes : Lama waktu berwisata
    *   Coordinate : Koordinat tempat wisata
    *   Lat : Latitude tempat wisata
    *   Long : Panjang dari tempat wisata
    *   Unamed: 11 : Data tanpa penjelasan
    *   Unamed: 12 : Data tanpa penjelasan
*   Variabel pada user.csv
    *   User_Id : Id dari user
    *   Location : Lokasi user
    *   Age : Umur user
    
### Data Preprocessing

**Data Analysis**

- Menentukan file.csv yang akan digunakan untuk sistem rekomendasi, file yang digunakan diantaranya :
  - tourism_with_id.csv pada variabel tourism
  - tourism_rating.csv pada variabel rating
- Kemudian cek jumlah fitur numerik dan kategori pada tourism, diperoleh informasi numerik terdiri dari 8 fitur, dan kategori terdiri dari 5 fitur, diantaranya sebagai berikut :
  - Numerik :
    - Place_Id : int64
    - Price : int64
    - Rating : float64
    - Time_Minutes : float64
    - Lat : float64
    - Long : float64
    - Unnamed: 11 : float64
    - Unnamed: 12 : float 64
  - Kategori :
    - Place_Name : object
    - Description : object
    - Category : object
    - City : object
    - Coordinate : object 
- Karena pada sistem rekomendasi ini hanya merekomendasikan tempat wisata berdasarkan tempat wisata yang telah dikunjungi sebelumnya, maka fitur selain Place_Id, Place_Name dan Category akan dihapus.
- Kemudian cek jumlah fitur numerik dan kategori pada rating, diperoleh informasi numerik 3 fitur sedangkan kategori tidak ada, diantaranya sebagai berikut :
- Numerik :
  -  User_Id : int64
  -  Place_Id : int64
  -  Place_Ratings : int64
-  Kemudian melihat distribusi data dari rating

   |       |      User_Id |     Place_Id | Place_Ratings |
   |:-----:|-------------:|-------------:|--------------:|
   | count | 10000.000000 | 10000.000000 |  10000.000000 |
   |  mean |   151.292700 |   219.416400 |      3.066500 |
   |  std  |    86.137374 |   126.228335 |      1.379952 |
   |  min  |     1.000000 |     1.000000 |      1.000000 |
   |  25%  |    77.000000 |   108.750000 |      2.000000 |
   |  50%  |   151.000000 |   220.000000 |      3.000000 |
   |  75%  |   226.000000 |   329.000000 |      4.000000 |
   |  max  |   300.000000 |   437.000000 |      5.000000 |

   Terlihat pada tabel distribusi, dapat dipastikan tidak terdapat bahwa terdapat data duplikat pada fitur User_Id, data duplikat ini akan diproses pada proses data preparation.
- Kemudian menggabungkan fitur Category dan Place_Name pada tourism ke dalam variabel rating.
- Kemudian cek data null pada variabel all_tourism yang berisi fitur-fitur yang telah digabung sebelumnya.

**Univariate Exploratory Data Analysis**
- Melakukan teknik EDA menggunakan univariate analysis dengan memvisualisasikan data untuk memahami satu persatu data pada fitur yang telah diolah sebelumnya.
  - Fitur Place_Ratings
   
    ![image](https://user-images.githubusercontent.com/58927608/229636612-44a0cbc7-5628-4df6-91c0-4381a1559bca.png)
    
    Dapat dilihat pada visualisasi diatas, masing-masing rating memiliki persentase yang hampir mirip, berikut merupakan persentase dan jumlah sample secara spesifik dari visualisasi diatas diurutkan dari yang terbanyak hingga terendah :
    - Rating 4 : 2106 sample, 21.1%
    - Rating 3 : 2096 sample, 21.0%
    - Rating 2 : 2071 sample, 20.7%
    - Rating 5 : 2021 sample, 20.2%
    - Rating 1 : 1706 sample, 17.1%
  
  - Fitur Category
    
    ![image](https://user-images.githubusercontent.com/58927608/229637643-11ee4916-1d40-4fc4-b142-2592e1343635.png)
    
    Terlihat bahwa 50% dari keseluruhan data berada pada Category Taman Hiburan dan Budaya, berikut merupakan presentase dan jumlah sample spesifik dari fitur Category diurutkan dari terbesar hingga terendah :
    - Taman Hiburan : 3053 sample, 30.5%
    - Budaya : 2683 sample, 26.8%
    - Cagar Alam : 2415 sample, 24.2%
    - Bahari : 1079 sample, 10.8%
    - Pusat Perbelanjaan : 385 sample, 3.8%
    - Tempat Ibadah : 385 sample, 3.8%

  - Fitur Place_Name
    Untuk fitur Place_Name disini hanya menampilkan banyak tempat wisata. Diperoleh bahwa banyak tempat wisata yang akan digunakan untuk sistem rekomendasi adalah sebanyak 437.
  
## Data Preparation
Teknik Data preparation yang dilakukan terdiri dari:
 - Menghapus data duplikat pada Place_Id yang sudah ditunjukkan pada bagian Data Preprocessing
 - Membuat dictionary untuk data baru yang berisi fitur place_id, place_category dan place_name

**Proses Data Preparation**
- Cek apakah ada data null pada data all_tourism
- Kemudian cek banyak data pada all_tourism, diperoleh informasi bahwa banyak data sekarang adalah 437
- Setelah itu buat variabel baru preparation yang berisi data dari all_tourism
- Kemudian hapus nilai duplikat pada fitur Place_Id
- Membuat variabel baru untuk membuat dictianory, seperti berikut :
  - `place_id = preparation['Place_Id'].tolist()`
  - `place_category = preparation['Category'].tolist()`
  - `place_name = preparation['Place_Name'].tolist()`
- Kemudian menggabungkan variabel baru tersebut ke dalam tourism_recommend 

**Mengapa perlu dilakukan data prepration?** 
- Untuk menghilangkan data duplikat, karena dapat menyebabkan bias pada data
- Dibuatnya tourism_recommend untuk menampung fitur-fitur yang hanya akan digunakan untuk rekomendasi

## Modeling

**TF-IDF Vectorizer**
- Sebelum mengembangkan sistem rekomendasi dengan content-based filtering, masukkan data preparation ke variabel baru yaitu cf.
- Kemudian membuat sistem rekomendasi berdasarkan tempat wisata yang telah dikunjungi sebelummnya, menggunakan TF-IDF Vectorizer dengan fungsi `tfidfvectorizer()` dari sklearn. Tahap ini terdiri dari inisialisasi TfidfVectorizer, kemudian perhitungan idf pada place_name dan mapping array dari fitur index ke fitur nama.
- Lakukan fitting dan transformasi fitur place_name dalam bentuk matriks.
- Mengubah vektor tf-dif dalam bentuk matrix dengan `fungsi todense()`

**Cosine Similarity**
- Selanjutnya membuat dataframe untuk melihat tf-idf matrix dengan kolom berisi place_name dan baris place_category, ini digunakan untuk melihat korelasi antar place_name dengan category.
- Kemudian menghitung derajat kesamaan (similarity degree) antar place_name menggunakan cosine_similarity dari sklearn.

**Mendapatkan rekomendasi**
- Membuat fungi tourism_recommendations dengan parameter sebagai berikut : 
  - nama_tempat : nama tempat wisata
  - similarity_data : dataframe similarity sebelumnya
  - items : fitur untuk mendefinisikan kemiripan dari plaec_name dan place_category
  - k : banyak rekomendasi yang diberikan
- Kemudian menemukan rekomendasi yang mirip dengan Pantai Baron, berikut merupakan output yang dihasilkan :
 
  |   |       place_name | place_category |
  |--:|-----------------:|---------------:|
  | 0 |     Pantai Ancol |         Bahari |
  | 1 |    Pantai Marina |         Bahari |
  | 2 |    Pantai Congot |         Bahari |
  | 3 |     Pantai Drini |         Bahari |
  | 4 | Pantai Ngrenehan |         Bahari |

**Kelebihan dan kekurangan algoritma yang digunakan**
Kelebihan *content-based filtering*
- Kemapuan untuk merekomendasikan item yang bersifat personal dan baru bagi user
Kekurangan *content-based filtering*
- Terbatas pada rekomendasi pad item-item yang mirip sehingga tidak ada kesempatan untuk mendapatkan item yang diluar kemiripan

**Mengapa menggunakan model tersebut?**
- Karena sistem rekomendasi ini menampilkan rekomendasi berdasarkan tempat wisata yang telah dikunjungi pada wisatawan atau turis sebelumnya, sehingga menampilkan rekomendasi yang mirip pada wisata sebelumnya.

## Evaluation
- Metrik evaluasi yang digunakan adalah recommender system precision. Disini precision merupakan jumlah item yang direkomendasikan yang relevan.
**Formula Mean Squared Error dan cara Mean Squared Error bekerja**
Rumus yang digunakan untuk recommender system precision sebagai berikut :

![image](https://user-images.githubusercontent.com/58927608/229649814-1d36551c-687b-4118-b4df-a6f100433bb3.png)

**Bagaimana cara Mean Squared Error bekerja?**
Cara kerjanya adalah dengan membagi nilai item yang relevan dengan nilai jumlah item yang direkomendasikan, misalnya berikut

  |   |       place_name | place_category |
  |--:|-----------------:|---------------:|
  | 0 |     Pantai Ancol |         Bahari |
  | 1 |    Pantai Marina |         Bahari |
  | 2 |    Pantai Congot |         Bahari |
  | 3 |     Pantai Drini |         Bahari |
  | 4 | Pantai Ngrenehan |         Bahari |

Fitur yang relevan pada tabel diatas adalah 5 dengan jumlah total top-N adalah 5, apabila dimasukkan kedalam rumus maka akan menjadi seperti berikut :
 releven/jumlah item rekomendasi = 5/5 = 1 berarti precisionnya adalah 100%

REFERENSI :
  
  [Parawisata Indonesia](https://id.wikipedia.org/wiki/Pariwisata_di_Indonesia)
  [Parawisata](https://id.wikipedia.org/wiki/Pariwisata)
