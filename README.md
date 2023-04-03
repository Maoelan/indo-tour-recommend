# Laporan Proyek Machine Learning - Maulana Muhammad

## Lingkungan - CO2 Emission

![image](https://user-images.githubusercontent.com/58927608/228171528-d61cf498-1ff7-4206-8caa-9d53f7f98fa5.png)

CO2 *emissions* atau emisi karbon merupakan proses karbon dioksida ke atmosfer yang terjadi secara alami maupun dipicu aktivitas manusia, seperti deforestasi, konsumsi listrik, hingga kegiatan industri manufaktur. Senyawa ini adalah salah satu hasil dari pembakaran yang perlu dibuang. Gas buang berupa karbondioksida ini merupakan emisi yang kebanyakan saat ini dihasilkan kendaraan yang perlu diujikan dalam proses uji emisi. C02 *emission* ini sangat berpengaruh terhadap percepatan pemanasan global.
  
Pelepas senyawa karbon CO2 ke lapisan atmosfer bumi akan memberikan dampat pada lingkungan, kesehatan, dan ekonomi, yang cukup terlihat sekarang yaitu pada lingkungan seperti ada peningkatan suhu bumi pertahun yang berakibat salju dikutub dan cangkupan glesternya akan berkurang dan menyebabkan peningkatan permukaan air laut sehingga masalah ini harus diselesaikan untuk mencegah hal tersebut terjadi dalam jangka dekat.

## Business Understanding

CO2 *Emission* atau emisi karbon merupakan proses pelepasan karbon ke atmosfer. Senyawa karbon merupakan hasil pembakaran yang perlu dibuang. Saat ini kebanyak penghasil emisi karbon merupakan kendaraan sehari-hari yang menghasilkan karbon dari pembakaran bahan bakar yang dilepaskan begitu saja ke atmosfer bumi. Bayangkan berapa banyak karbon yang dilepaskan dalam sehari oleh kendaraan. Kendaraan roda empat menghasilkan rata-rata 200 g/km karbon CO2. Itu dalam hitungan km, bagaimana dengan penggunaan kendaraan roda empat dalam sehari? ditambah seluruh penduduk bumi sekarang tidak terlepas dari kendaraan. Karena itu dibuatlah sistem untuk memprediksi penghasilan karbon CO2 untuk mengukur berapa banyak kendaraan roda empat mengeluarkan karbon dalam hitungan g/km.

### Problem Statements

Menjelaskan pernyataan masalah latar belakang:
- Dari banyaknya fitur, fitur apa yang memiliki pengaruh pada penghasilan CO2 *emission*?
- Berapa banyak CO2 *emission* yang dihasilkan pada fitur yang berpengaruh dengan CO2 *emission*?

### Goals

Menjelaskan tujuan dari pernyataan masalah:
- Mengetahui fitur yang berkorelasi dengan CO2 *emission*.
- Membuat model machine learning yang dapat memprediksi CO2 *emission*.

    ### Solution statements
    - Menggunakan 5 algoritma berbeda untuk menentukan hasil prediki terbaik yaitu Linear Regressor, Decision Tree Regressor, K-Nearest Neighbor, Random Forest Regressor, dan Adaptive Boosting.
    - Melakukan improvement pada ke 4 baseline yaitu Decison Tree Regressor, K-Nearest Neighbor, Random Forest Regressor, dan Adaptive Boosting menggunakan hyperparameter tunning. 

## Data Understanding
Dataset : [CO2 Emission by Vehicles](https://www.kaggle.com/datasets/debajyotipodder/co2-emission-by-vehicles).

**Overview**

- Nama dataset : CO2 Emission by Vehicles
- Format dataset : CSV
- Jumlah kolom : 12
- Jumlah data : 7385

Informasi lain :
   - Dataset ini merupakan penelitian detail tentang bagaiman emisi CO2 yang dihasilkan oleh kendaraan dengan fitur yang berbeda. Dataset ini diambil dari website open data pemerintah Canada yang mencangkup data selama periode 7 tahun.

### Variabel-variabel pada CO2 Emission by Vehicles dataset adalah sebagai berikut:
*   Make : Perusahaan yang membuat kendaraan
*   Model : Model dari kendaraan
*   Vehicle Class : Kelas dari kendaraan berdasarkan utilitas, kapasitas dan berat 
*   Engine Size (L) : Ukuran dari mesin dalam satuan liter (L)
*   Cylinders : Jumlah silinder kendaraan (ruang naiknya piston)
*   Transmission : Tipe transmisi dengan jumlah gigi kendaraan
    *   A = Otomatis
    *   AM = Manual Otomatis
    *   AS = Otomatis dengan pilihan shift
    *   AV = Variabel kontinu
    *   M = Manual
    *   X = Angka dari gigi
*   Fuel Type : Tipe bahan bakar
    *   X = Bensin Reguler
    *   Z = Bensin Premium
    *   D = Disel
    *   E = Ethanol (E85)
    *   N = Gas Natural
*   Fuel Consumption City (L/100 km) : Jumlah konsumsi bahan bakar dijalanan kota dalam satuan (L/100 km)
*   Fuel Consumption City (L/100 km) : Jumlah konsumsi bahan bakar dijalanan raya dalam satuan (L/100 km)
*   Fuel Consumption Comb (L/100 km) : Jumlah konsumsi bahan bakar (55% kota. 45% jalan raya) dalam satuan (L/100 km)
*   CO2 Emissions(g/km) : Emisi knalpot karbon dioksida dalam gram/kilometer (g/km) dari gabungan berkendara pada jalanan kota dan jalan raya

### Exploratory Data Analysis
**Deskripsi Variabel** 
- Mengecek banyak fitur categorical dan numerik, diperoleh informasi:
   - Terdapat 5 fitur dengan tipe categorical atau object yaitu Make, Model, Vehicle Class, Transmission, dan Fuel Type
   - Terdapat 7 feature dengan tipe numeric terdiri dari 4 float64 yaitu Engine Size(L), Fuel Consumption City (L/100 km), Fuel Consumption Hwy (L/100 km), Fuel Consumption Comb (L/100 km), dan 3 bertipe int64 yaitu Cylinders, Fuel Consumption Comb (mpg) dan CO2 Emissions(g/km)
- Menghapus data yang dianggap tidak terlalu penting, terdiri dari 3 data categorical yaitu Make, Model dan Vehicle Class.

**Missing Value & Outlier** 
- Mengecek missing value dan data yang dianggap memiliki kejanggalan.

|       | Engine Size(L) |  Cylinders  | Fuel Consumption City (L/100 km) | Fuel Consumption Hwy (L/100 km) | Fuel Consumption Comb (L/100 km) | Fuel Consumption Comb (mpg) | CO2 Emissions(g/km) |
|:-----:|:--------------:|:-----------:|:--------------------------------:|:-------------------------------:|:--------------------------------:|:---------------------------:|:-------------------:|
| count |   7385.000000  | 7385.000000 |            7385.000000           |           7385.000000           |            7385.000000           |         7385.000000         |     7385.000000     |
|  mean |    3.160068    |   5.615030  |             12.556534            |             9.041706            |             10.975071            |          27.481652          |      250.584699     |
|  std  |    1.354170    |   1.828307  |             3.500274             |             2.224456            |             2.892506             |           7.231879          |      58.512679      |
|  min  |    0.900000    |   3.000000  |             4.200000             |             4.000000            |             4.100000             |          11.000000          |      96.000000      |
|  25%  |    2.000000    |   4.000000  |             10.100000            |             7.500000            |             8.900000             |          22.000000          |      208.000000     |
|  50%  |    3.000000    |   6.000000  |             12.100000            |             8.700000            |             10.600000            |          27.000000          |      246.000000     |
|  75%  |    3.700000    |   6.000000  |             14.600000            |            10.200000            |             12.600000            |          32.000000          |      288.000000     |
|  max  |    8.400000    |  16.000000  |             30.600000            |            20.600000            |             26.100000            |          69.000000          |      522.000000     |

- Dari tabel diatas, dapat dikatakan tidak memiliki missing value tetapi pada data terlihat apabila data memiliki kejanggalan pada kuartil ketiga dengan nilai maksimum dan diduga kalau data ini merupakan outlier.
- Melakukan visualisasi data dengan boxplot pada tipa numerik untuk mengecek apakah data tersebut merupakan outlier atau tidak dan didapatkan hasil kalau data tersebut merupakan data outlier.
   - Untuk mengetahui apakah data dapat dikatakan outlier dapat dilihat pada gambar berikut:
     
     ![image](https://user-images.githubusercontent.com/58927608/228157066-4aee842b-6e88-4731-b11d-8f1c949ee4a6.png)
     
   - Pada gambar terlihat, apabila data melebihi rentang Minimum atau Maximum, maka dapat dikatakan outlier.
- Menghapus data outlier menggunakan IQR method.
   - Outlier merupakan rentang nilai yang melebihi batas Minimum dan Maximum. Berdasarkan hasil dari visualisasi boxplot yang dilakukan dapat dilihat:
   
        ![image](https://user-images.githubusercontent.com/58927608/228157124-650aefda-af38-4462-b41a-f274a46758ea.png)
        
        ![image](https://user-images.githubusercontent.com/58927608/228157170-80437432-0ed3-4bc1-a721-a43d0622a637.png)
        
        ![image](https://user-images.githubusercontent.com/58927608/228157249-d4220475-7878-4a6f-8d21-31bd0789de95.png)   
        
        ![image](https://user-images.githubusercontent.com/58927608/228157724-a17904ea-a7fc-4412-b98a-590a38e82c38.png)
        
        ![image](https://user-images.githubusercontent.com/58927608/228157400-ad9aeefb-5c16-4c5d-ba99-58d1b262c234.png)
        
        ![image](https://user-images.githubusercontent.com/58927608/228157442-1a45d0d9-b4f3-49d0-a087-2d4d2ea9b3f8.png)
        
        ![image](https://user-images.githubusercontent.com/58927608/228157481-faacbe76-8e5b-4907-b81f-7e90a86230a8.png)
        
    - Berdasarkan gambar diatas dapat disimpulkan bahwa semua fitur mulai dari Engine Size(L), Cylinders, Fuel Consumption City(L/100 km), Fuel Consumption Hwy(L/100 km), Fuel Consumption Comb(mpg), dan CO2 Emission(g/km) memiliki data outlier karena ada data yang diluar rentang nilai maximum. 
    - Setelah dipastikan ada data outlier, selanjutnya menerapakan IQR Method untuk menghapus outlier tersebut.

**Univariate Analysis** 
- Melakukan teknik EDA menggunakan unvariate analysis dengan memvisualisasikan data untuk memahami satu persatu data pada fitur yang tersedia pada dataset.
  
  **Fitur Kategori** 
  
  ![image](https://user-images.githubusercontent.com/58927608/228160138-38f8f530-7d5e-4705-a5c8-7b6045ead6b8.png)
  
  Pada visualisasi diatas dapat disimpulkan:
     - Terdapat 27 kategori feature untuk transmission
     - Transmisi AS (Otomatis dengan pilihan shift) sebanyak 43.6%
     - Transmisi A (Otomatis) sebanyak 23.8%
     - Transmisi M (Manual) sebanyak 17%
     - Transmisi AM (Manual Otomatis) sebanyak 8.2%
     - Transmisi AV (Variabel kontinu) sebanyak 7.2%
  
  ![image](https://user-images.githubusercontent.com/58927608/228160794-52015618-d73b-455c-afb8-729e13cc7c09.png)

  Pada visualisasi diatas dapat disimpulkan:
     - Pada Fuel Type terdapat 5 jenis variabel yaitu X, Z, E, D dan N. Dapat disimpulkan bahwa sebagian besar kendaraan menggunakan Fuel Type X dan Z yaitu Bensin Reguler dan Bensin Premium dengan persentase 94.1%
  
  **Fitur Numerik**
  
  ![image](https://user-images.githubusercontent.com/58927608/228162227-6ae7b5a0-5d79-4b18-8479-97f47d760ee5.png)
  
   Pada visualisasi diatas dapat disimpulkan:
     - Peningkatan CO2 Emission sebanding dengan peningkatan jumlah sample. Dapat terlihat pada histogram feature "CO2 Emission" grafik mengalami peningkatan dengan semakin banyaknya sample.
     - Kadar CO2 Emission yang dihasilkan 2x dari batas normal yaitu 522 g/km.
     - Setengah kadar CO2 Emission berada pada kisaran 246 g/km.
     - Kebanyakan kadar C02 Emission terdapat pada quartil ke-1 sampai ke-3.
     - Distribusi CO2 Emission miring kekanan (left-skewed) yang berarti nilai median (nilai tengah) terdapat pada quartile ke-3 dan lebih besar dari nilai rata-rata.

**Multivariate Analysis** 
- Melakukan teknik EDA menggunakan multivariate analysis dengan memvisualisasikan data untuk memahami hubungan antar dua fitur atau lebih.

  **Fitur Kategori**
  
  ![image](https://user-images.githubusercontent.com/58927608/228162916-dbcf3bf5-0a9b-4a22-885b-f3e10a701790.png)
  
  Pada visualisasi diatas dapat disimpulkan:
  - Rentang CO2 Emission(g/km) pada tiap tipe transmission berkisar pada 140 - 300, dapat dilihat distribusi data tidak mengalami penurunan maupun peningkatan yang membuktikan kalau fitur transmission memiliki dampak kecil terhadap CO2 Emission(g/km).
  - Rentang CO2 Emission(g/km) pada Fuel Type berada diatas 200 sampai dengan 250, dimana tiap Fuel Type memiliki kemiripan dan rentang yang tidak terlalu berselisih jauh yang membuktikan kalau fitur Fuel Type memiliki dampat kecil terhadap CO2 Emission(g/km).
  
  **Fitur Numerik**
  
  ![image](https://user-images.githubusercontent.com/58927608/228163751-1b714897-821b-4f7d-afcb-c42ed0c3afbd.png)
  
  Pada visualisasi diatas dapat disimpulkan:
  - Pola sebaran data pada grafik pairplot diatas terlihat bahwa semua feature memiliki korelasi yang tinggi terhadap feature CO2 Emission(g/km).
  - Engine Size(L) : Positive Correlation.
  - Cylinders : Positive Correlation.
  - Fuel Consumption City (L/100 km) : Positive Correlation.
  - Fuel Consumption Hwy (L/100 km) : Positive Correlation.
  - Fuel Consumption Comb (L/100 km) : Positive Correlation.
  - Fuel Consumption Comb (mpg) : Negative Correlation.
  
  Kemudian cek skor korelasi menggunakan corr()
  
  ![image](https://user-images.githubusercontent.com/58927608/228163854-c3bb9cb2-b1ec-4356-80ba-2ce8e23342b4.png)
  
  Pada visualisasi diatas dapat disimpulkan:
  - Terbukti apabila rata-rata feature memiliki korelasi dengan CO2 Emissions yang rata-rata skor korelasi diatas 0.8 untuk positive correlation, dan -0.9 untuk negative correlation, sehingga tidak ada feature yang perlu dihapus.

## Data Preparation
Teknik Data preparation yang dilakukan terdiri dari:
 - Label encoding
 - OneHot encoding
 - Reduksi dimensi dengan PCA
 - Train-test-split data

**Proses Data Preparation**

**Encoding Fitur Kategori**
- Mengubah fitur categorical menjadi data numerik, pertama adalah fitur Transmission kalan diubah menggunakan LabelEncoder.
- Fitur Fuel Type diubah menggunakan OneHotEncoder.

**Reduksi Dimensi dengan PCA**
- Mengecek korelasi antara ketiga fitur yaitu Fuel Consumption City (L/100 km), Fuel Consumption Hwy (L/100 km), Fuel Consumption Comb (L/100 km) untuk menentukan apakah fitur ini dapat dilakukan reduksi dimensi dengan PCA.

  ![image](https://user-images.githubusercontent.com/58927608/228165397-a4e47ab5-6a10-4592-938f-841adbd91825.png)
  
  Pada pairplot diatas terlihat kalau ketiga feature yaitu Fuel Consumption City (L/100 km), Fuel Consumption Hwy (L/100 km) dan Fuel Consumption Comb (L/100 km) memiliki korelasi yang cukup tinggi sehingga dapat dilakukan proses reduksi dimensi

- Setelah diketahui ketiga fitur tersebut berkorelasi dilakukan reduksi dimensi dengan PCA, membuat fitur baru yaitu Fuel Consumption untuk menggantikan ketiga fitur tersebut.

**Train-test-split**
- Sebelum dilakukan train-test-split, langkah awal adalah memisahkan antara feature dan label, variabel x digunakan untuk menampung feature yang tediri dari:
  - Engine Size(L)
  - Cylinders
  - Transmission
  - Fuel Consumption Comb (mpg)
  - Fuel_Type_D
  - Fuel_Type_E
  - Fuel_Type_N
  - Fuel_Type_X
  - Fuel_Type_Z
  - Fuel Consumption
- Dan variabel x digunakan untuk menampung label yaitu
  - CO2 Emissions(g/km)
- Kemudian melakukan train-test-split, data train dan test dibagi menjadi rasio 80:20.
  Setelah dilakukan splitting data, dari total 6826 data setelah dilakukan splitting data, data terbagi menjadi 5460 train dan 1366 test.
  
**Standarisasi**
- Melakukan standarisasi dengan MinMaxScaler.

  |       | Engine Size(L) | Cylinders | Transmission | Fuel Consumption Comb (mpg) |
  |:-----:|:--------------:|:---------:|:------------:|:---------------------------:|
  | count |    5460.0000   | 5460.0000 |   5460.0000  |          5460.0000          |
  |  mean |     0.3990     |   0.4785  |    0.5498    |            0.3786           |
  |  std  |     0.2274     |   0.3016  |    0.2776    |            0.1943           |
  |  min  |     0.0000     |   0.0000  |    0.0000    |            0.0000           |
  |  25%  |     0.2075     |   0.2000  |    0.3077    |            0.2258           |
  |  50%  |     0.3962     |   0.6000  |    0.5769    |            0.3548           |
  |  75%  |     0.5094     |   0.6000  |    0.6923    |            0.5161           |
  |  max  |     1.0000     |   1.0000  |    1.0000    |            1.0000           |

- Dari tabel diatas terlihat bahwa min dari data yaitu 0 dan max dari data yaitu 1, karena standarisasi MinMaxScaler menghasilkan distribusi data yang ada pada rentang 0 dan 1.

**Mengapa perlu dilakukan data prepration?** 
- Perlu dilakukan proses encoding pada data categorical adalah agar data dapat diproses oleh model, karena model lebih dapat memproses data bertipe numerik.
- Diperlukannya reduksi dimensi adalah agar menyederhanakan model dan mencegah terjadinya overfitting.
- Perlu dilakukan train-test-split agar hasil prediksi dapat lebih akurat pada data baru.
- Perlu dilakukan standarisasi agar model lebih mudah memproses data.

## Modeling
Model machine learning yang digunakan untuk masalah ini terdiri dari 5 model yaitu:
- LinearRegression : tidak memiliki parameter
- DecisionTreeRegressor dengan parameter sebagai berikut:
    * `max_depth = 10` : kedalaman pohon
    * `random_state = 20` : digunakan untuk random generator
- K-Nearest Neighbor dengan parameter sebagai berikut:
    * `n_neighbors = 7` : jumlah tetangga yang digunakan untuk mengukur jarak
- RandomForestRegressor dengan parameter sebagai berikut:
    * `n_estimators = 50` : jumlah tree pada forest
    * `max_depth = 15` : kedalaman pohon
    * `random_state = 55` : digunakan untuk random generator
    * `n_jobs = -1` : jumlah job yang digunakan secara pararel
- Adaptive Boosting dengan parameter sebagai berikut:
    * `learning_rate = 0.9` : bobot pada regressor pada masing-masing iterasi
    * `random_state = 50` : digunakan untuk random generator
    * `n_estimators = 10` : jumlah base estimator yang ingin digunakan dalam data

**Kelebihan dan kekurangan algoritma yang digunakan**
- LinearRegression:
    * Kelebihan : Mengetahui hubungan antar variabel independen dan dependen.
    * Kekurangan : Pada dunia nyata tidak banyak masalah yang menunjukkan hubungan yang jelas antar variabel independen dan dependen.
- DecisionTreeRegressor:
    * Kelebihan : Mudah dalam pembuatan dan dimasukkan dalam rangkaian pohon keputusan.
    * Kekurangan : Tidak baik digunakan pada kasus-kasus kompleks karena akan membuat gambaran tree membingungkan.
- K-Nearest Neighbor:
    * Kelebihan : Mudah diterapkan pada proses regresi, dan model mudah beradaptasi.
    * Kekurangan : Apabila dataset berukuran besar maka akan tidak berfungsi dengan baik.
- RandomForestRegressor:
    * Kelebihan : Dapat mengatasi noise dan missing value dan dapat mengatasi data dalam jumlah yang terbilang besar.
    * Kekurangan : Interpretasi yang sulit dan membutuhkan hyperparameter tunning model yang tepat agar tepat untuk data.
- RandomForestRegressor:
    * Kelebihan : Dapat mengatasi noise dan missing value dan dapat mengatasi data dalam jumlah yang terbilang besar.
    * Kekurangan : Interpretasi yang sulit dan membutuhkan hyperparameter tunning model yang tepat agar tepat untuk data.
- Adaptive Boosting:
    * Kelebihan : Hasil dari pemodelan dapat lebih akurat karena mengkombinasikan beberapa model.
    * Kekurangan : Dapat mengurangi kemampuan interpretasi model karena meningkatnya kompleksitas model.

**Mengapa menggunakan model tersebut?**
- LinearRegression karena dapat melakukan generalisasi pada pola data, dan melakukan perhitungan pararel sehinggan proses training lebih cepat.
- DecisionTreeRegressor karena mampu memproses pengambilan keputusan yang kompleks menjadi lebih simpel dan mudan diinterpretasikan.
- K-Nearest Neighbor karena titik data akan diklasifikasikan berdasarkan kesamaan antar kelompok data yang berdekatan.
- RandomForestRegressor karena terbuat dari beberapa decision tree yang digabungkan sehingga mendapatkan hasil prediksi yang lebih stabil.
- Adaptive Boosting karena memilai prediksi model dan meningkatkan bobot sample dengan kesalahan yang dibuat pada model sebelumnya.

## Evaluation
- Metrik evaluasi yang digunakan disini adalah Mean Squared Error. Mean Squared Error disini dapat dikatakan adalah sebuah metrik yang mengukur seberapa besar error pada nilai aktual dan nilai hasil prediksi.
- Hasil yang diperoleh dari metrik ini apabila diurutkan dari error terkecil sampai terbesar adalah sebagai berikut:
    
    ![image](https://user-images.githubusercontent.com/58927608/228170034-f17c1ff9-5164-4751-80af-c1f6226b6a75.png)
    
    |                       |    train |     test |
    |:---------------------:|---------:|---------:|
    |       LinearRegressor | 0.013481 | 0.014259 |
    | DecisionTreeRegressor | 0.004165 | 0.010623 |
    |                   KNN | 0.007251 | 0.011366 |
    |          RandomForest | 0.002074 | 0.009687 |
    |              Boosting | 0.080138 | 0.078409 |
  
  Dapat disimpulkan dari hasil diatas RandomForestRegressor merupakan paling akurat memprediksi data dengan selisih   
  error terkecil dibandingkan dengan model lainnya dan Adaptive Boosting memiliki error yang paling tinggi diantara 
  kelima model yang digunakan

**Formula Mean Squared Error dan cara Mean Squared Error bekerja** 

formula Mean Squared Error :

![image](https://user-images.githubusercontent.com/58927608/228169779-4e707c1d-ab14-4dcd-bc14-a9b99b152cc3.png)


**Bagaimana cara Mean Squared Error bekerja?**

Cara kerjanya adalah dengan melakukan pengurangan nilai data aktual dengan nilai prediksi dan hasilnya akan dikuadratkan dan dijumlahkan secara keseluruhan kemudian dibagi dengan banyak data yang ada.

REFERENSI :
  
  [Irreversible climate change due to carbon dioxide emissions](https://www.pnas.org/doi/full/10.1073/pnas.0812721106) 

  [Climate Change: Atmospheric Carbon Dioxide](https://www.climate.gov/news-features/understanding-climate/climate-change-atmospheric-carbon-dioxide) 

  [CO2, the greenhouse effect and global warming: from the pioneering work of Arrhenius and Callendar to today’s Earth System Models](https://reader.elsevier.com/reader/sd/pii/S0160932716300308?token=926B8C03B6AF557DFA13E43DFAE380301F452C9AE0BD0ACA7B7345D65C02F0CE8AAC54E8BBC1904F448064BE28D0BBFD&originRegion=eu-west-1&originCreation=20230327151603) 
  
  [CO2 emission sources, greenhouse gases, and the global warming effect](https://www.researchgate.net/profile/Kelvin-Yoro/publication/343508726_CO2_emission_sources_greenhouse_gases_and_the_global_warming_effect/links/5f44aa2692851cd30227cffd/CO2-emission-sources-greenhouse-gases-and-the-global-warming-effect.pdf)
  
  [Evaluating the potential impact of global warming on the UAE residential buildings–A contribution to reduce the CO2 emissions](https://d1wqtxts1xzle7.cloudfront.net/83972358/j.buildenv.2009.04.00620220412-1-1hp1tf-libre.pdf?1649794475=&response-content-disposition=inline%3B+filename%3DEvaluating_the_potential_impact_of_globa.pdf&Expires=1679989093&Signature=UfA03vy6IFVY-RuXxGeBXztbCv9CfTcyNeI3RJB~FvJk-GMBgY31spiFZhCKS1TQGTSUaY0pi3S9YfcxxvPn8JKBJh2H6UCwGwRarfx7FXVww0ERWViCrHgn4ioRQ4Z-~Lx07x36mx6xiC0QZfb5hCdWbBDFmPcNVRN5p9hIqlIEGKfCqm-OLoFi1w80uSWdAe4wX1mpjrs7gEgxLzYqI~IpyA0-Q-M7i6VaEDsCiNi6R7JWVGHUl0ME~5rKo9uGuHN7C-c6-e0LxGHAAUK3bIWsVdL~cH9agZPgNgT7WA5DHjz~CyF~ivFIuOL4GKfQCy-aNe-RsLCuu0iCKbjMvA__&Key-Pair-Id=APKAJLOHF5GGSLRBV4ZA)
