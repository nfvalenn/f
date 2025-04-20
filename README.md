# 📚 Laporan Proyek Machine Learning - Nabila Febriyanti Valentin

![Foto Saya](https://raw.githubusercontent.com/nfvalenn/Submission_Proyek_Pertama/main/foto.jpeg)


## 🌐 Domain Proyek

Pendidikan merupakan fondasi utama dalam pengembangan sumber daya manusia. Di era digital saat ini, pendekatan berbasis data dapat dimanfaatkan untuk membantu memahami performa akademik siswa. Salah satu cara yang bisa dilakukan adalah membangun model prediksi menggunakan machine learning untuk mengetahui seberapa besar pengaruh faktor-faktor seperti jenis kelamin, latar belakang orang tua, dan status sosial terhadap nilai akademik siswa.

Dengan memiliki pemahaman tentang faktor-faktor yang mempengaruhi performa siswa, pendidik dan institusi dapat memberikan intervensi yang lebih tepat sasaran dan meningkatkan efektivitas pembelajaran.

**Referensi:**  
[Hasra, Asyarah W.N., Azainil. 2024. "Kepemimpinan Profesionalisme Kepala Sekolah Berbasis Servant Leadership dalam Perkembangan Manajemen Mutu Pendidikan](https://jer.or.id/index.php/jer/article/view/1478/839)

## Business Understanding
---
### Problem Statements
- Bagaimana pengaruh tingkat pendidikan orang tua terhadap performa akademik siswa?
- Apakah mengikuti kursus persiapan ujian berkorelasi positif dengan nilai ujian?
- Apakah terdapat perbedaan skor akademik berdasarkan gender?

### Goals
- Mengetahui hubungan antara latar belakang pendidikan orang tua dan nilai siswa.
- Menilai pengaruh kursus persiapan ujian terhadap peningkatan skor.
- Menganalisis perbedaan nilai antara siswa laki-laki dan perempuan.

### Solution Statements
- Membangun model regresi untuk memprediksi skor `writing score` siswa berdasarkan fitur-fitur demografis.
- Menggunakan tiga algoritma yaitu Linear Regression, Random Forest Regressor, dan Gradient Boosting Regressor.
- Memilih model terbaik berdasarkan performa R² Score, MAE, dan MSE.

## 📊 Data Understanding
---
Data yang digunakan pada proyek ini adalah Students Performance in Exams Dataset yang diunduh dari platform [Kaggle](https://www.kaggle.com/datasets/spscientist/students-performance-in-exams). Dataset ini berisi 1.000 data siswa yang mengikuti ujian pada tiga mata pelajaran, yaitu Matematika, Membaca, dan Menulis. Masing-masing siswa memiliki atribut demografis serta informasi terkait status kursus persiapan ujian dan jenis makan siang yang dikonsumsi. Data ini sering digunakan sebagai dataset latihan dalam membangun model prediktif di bidang pendidikan.

Dataset ini terdiri dari 8 kolom (fitur), yaitu:
| **Nama Fitur**                 | **Tipe**       | **Deskripsi**                                                              |
|-------------------------------|----------------|---------------------------------------------------------------------------|
| `gender`                      | Kategorikal    | Jenis kelamin siswa (`male` atau `female`)                                |
| `race/ethnicity`              | Kategorikal    | Kelompok etnis siswa (Group A–E)                                          |
| `parental level of education` | Kategorikal    | Pendidikan tertinggi yang diraih oleh orang tua                           |
| `lunch`                       | Kategorikal    | Jenis makan siang (`standard` atau `free/reduced`)                        |
| `test preparation course`     | Kategorikal    | Status mengikuti kursus persiapan ujian (`none` atau `completed`)        |
| `math score`                  | Numerik        | Nilai ujian matematika                                                    |
| `reading score`               | Numerik        | Nilai ujian membaca                                                       |
| `writing score`               | Numerik        | Nilai ujian menulis                                                       |
### Berikut adalah beberapa tahapan untuk memahami data:
- Data Loading
- Exploratory Data Analysis (EDA) - Deskripsi Variabel
- Exploratory Data Analysis (EDA) - Menangani Missing Value dan Outliers
- Exploratory Data Analysis (EDA) - Univariate Analysis
- Exloratory Data Analysis (EDA) - Multivariate Analysis 

### Data Loading
Pada bagian ini, dataset akan dibaca secara langsung dari folder dataset yang sudah di download melalui [Students Performance in Exams Dataset](https://www.kaggle.com/datasets/spscientist/students-performance-in-exams). Dataset yang digunakan adalah StudentsPerformance.csv yang berisi dataset untuk proses pelatihan model. 
Tabel 1. Data students performance dari Students Performance in Exams Dataset
![Tabel](https://raw.githubusercontent.com/nfvalenn/Submission_Proyek_Pertama/main/tabel%201.png)
Berdasarkan Tabel 1 informasi yang didapat dataset adalah sebagai berikut:
- Terdapat 1000 baris dalam dataset
- Terdapat 8 kolom yaitu: gender, race/ethnicity, lunch, dan sebagainya.

### Exploratory Data Analysis - Deskripsi Variabel
Exploratory data analysis atau sering disingkat EDA merupakan proses investigasi awal pada data untuk menganalisis karakteristik, menemukan pola, anomali, dan memeriksa asumsi pada data. Proses EDA akan melakukan deskripsi variabel untuk mengetahui informasi lebih lengkap dan mengecek informasi pada dataset.

Fungsi info() pada Exploratory Data Analysis - Deskripsi Variabel terlihat bahwa:
- Terdapat 5 kolom bertipe object. Kolom ini merupakan categorical features
- Terdapat 3 kolom dengan tipe data int64. Kolom ini merupakan fitur numerik.
- Pada hasil info() tidak terdapat nilai null/NaN.

Selanjutnya, karena semua kolom telah memiliki tipe data yang sesuai dilakukan proses pengecekan deskripsi statistik data menggunakan fitur describe().
Fungsi describe() memberikan informasi statistik pada masing-masing kolom, antara lain:
- Count adalah jumlah sampel pada data.
- Mean adalah nilai rata-rata.
- Std adalah standar deviasi.
- Min yaitu nilai minimum setiap kolom.
- 25% adalah kuartil pertama. Kuartil adalah nilai yang menandai batas interval dalam empat bagian sebaran yang sama.
- 50% adalah kuartil kedua, atau biasa juga disebut median (nilai tengah).
- 75% adalah kuartil ketiga.
- Max adalah nilai maksimum.

### Exploratory Data Analysis - Menangani Missing Value, Outliers
1. Identifikasi Missing Value
    Berdasarkan hasil analisis menggunakan fungsi isnull().sum() dan info(), diketahui bahwa tidak terdapat missing value pada dataset Students Performance. Semua fitur memiliki data yang lengkap untuk 1000 baris.
    ** foto ss missing value**
    Output yang dihasilkan menunjukan bahwa semua kolom memiliki nilai 0 untuk jumlah missing value. Oleh karena itu, tidak diperlukan penanganan khusus untuk missing value dalam proses data preparation.
2. Menghilang Outliers
    Outliers adalah sampel yang nilainya sangat jauh dari cakupan umum data utama. Terdapat beberapa metode untuk mendeteksi outliers, pada proyek ini digunakan metode IQR (Inter Quartile Range). IQR menggunakan konsep kuratil untuk menghilangkan outliers, kuartil dari suatu populasi adalah tiga nilai yang membagi distribusi data menjadi empat sebaran. Seperempat dari data berada di bawah kuartil pertama (Q1), setengah dari data berada dibawah kuartil kedua (Q2), dan tiga perempat dari kata berada di kuartil ketiga (Q3). Dengan demikian interquartile range atau IQR = Q3 - Q1.

    Hal pertama yang perlu dilakukan adalah membuat batas bawah dan batas atas. Untuk membuat batas bawah, kurangi Q1 dengan 1.5 * IQR. Kemudian, untuk membuat batas atas, tambahkan 1.5 * IQR dengan Q3.
    - Batas bawah = Q1 - 1.5*IQR
    - Batas atas = Q3 + 1.5*IQR
    
    Selanjutnya visualisasikan terlebih dahulu dataset dengan boxplot untuk mendeteksi outliers pada beberapa fitur numerik. Misal pada fitur 'Math Score', 'Reading Score', dan 'Writing Score' seperti terlihat pada Gambar1, Gambar2, dan Gambar 3 berikut ini.
    ....
    ...
    ...
    Setelah outliers terdeteksi, dilakukan penghapusan data yang mengandung nilai-nilai ekstrem tersebut. Proses ini dilakukan untuk semua fitur numerik yang relevan agar model prediktif yang dibangun menjadi lebih akurat dan stabil.
    Penghapusan outliers dilakukan menggunakan metode IQR dengan langkah-langkah berikut:
    1. Menghitung Q1 dan Q3 untuk masing-masing fitur.
    2. Menghitung IQR = Q3 - Q1.
    3. Menghapus data yang berada di luar batas bawah dan batas atas.

    Setelah proses ini, jumlah data mengalami pengurangan. Awalnya terdapat 1000 sampel, menjadi 988 sampel. Ini menandakan bahwa sebanyak 12 data merupakan outliers dan tidak digunakan dalam analisis selanjutnya.
    
    Setelah proses penghapusan outliers dilakukan, dilakukan pengecekan ulang dengan boxplot untuk memastikan bahwa distribusi data sudah bersih. Visualisasi ulang menunjukkan bahwa sebaran nilai pada ketiga fitur numerik tersebut menjadi lebih rapi dan tidak lagi mengandung nilai ekstrem.
    ....
    ....
    ....
    Pembersihan data dari outliers merupakan langkah penting dalam proses prapemrosesan data. Dengan menghilangkan data ekstrem, model yang akan dibangun menjadi lebih stabil, tidak bias, dan mampu menghasilkan prediksi yang lebih baik. Proses ini juga membuat visualisasi data lebih representatif terhadap kondisi sebenarnya.

### Exploratory Data Analysis - Univariate Analysis
Sebelum masuk ke tahap proses analisis data dengan teknik Univariate EDA. Pertama, dilakukan proses pembagian fitur pada dataset menjadi dua bagian, yaitu numerical features dan categorical features (non numerik). Lakukan analisis pada fitur kategori terlebih dahulu kemudian pada fitur numerik.
1. Categorical Features
    Untuk fitur kategori, pertama visualisasikan dalam bentuk plot dan data frame untuk menganalisis persentase dari masing - masing fitur. Gambar 7 memperlihatkan salah satu fitur bernama 'gender'.
    .....
    Berdasarkan Gambar7, diketahui bahwa beberapa fitur kategori memiliki persentase yang berbeda. Persentase ini menunjukkan jumlah kategori dari masing-masing fitur atau seberapa sering kategori itu muncul pada fitur tersebut.
2. Numerical Features
    Untuk fitur numerik bisa menggunakan histogram untuk melihat hubungan fitur numerik terhadap sampel. Hasilnya dapat dilihat pada Gambar 8.
    ....
    
### Exploratory Data Analysis - Multivariate Analysis
Multivariate EDA menunjukkan hubungan antara dua atau lebih variabel pada data. Multivariate EDA yang menunjukkan hubungan antara dua variabel biasa disebut sebagai bivariate EDA. Selanjutnya,untuk melihat hubungan tersebut dilakukan analisis data pada fitur kategori dan numerik.

1. Categorical Features
    Untuk fitur kategori, dilakukan pengamatan rata-rata gender terhadap fitur kategori. Gambar 9 memperlihatkan salah satu visualisasi dari fitur kategori yaitu 'Gender':
    ...
    Dengan mengamati rata-rata gender terhadap fitur kategori diatas, diperoleh insight yaitu bahwa beberapa fitur kategori memiliki pengaruh yang cukup tinggi terhadapa performa siswa. Misalkan pada fitur 'Gender' yang dapat dilihat pada Gambar 9, gender terbanyak dimiliki oleh perempuan.

2. Numerical Features
    Untuk mengamati hubungan antara fitur numerik, dilakukan Corellation matrix untuk melihat hubungan korelasi antar fitur. Koefisien korelasi berkisar antara -1 dan +1, dimana itu akan mengukur kekuatan hubungan antara dua variabel serta arahnya (positif atau negatif). Mengenai kekuatan hubungan antar variabel, semakin dekat nilainya ke 1 atau -1, korelasinya semakin kuat. Sedangkan, semakin dekat nilainya ke 0, korelasinya semakin lemah. Arah korelasi antara dua variabel bisa bernilai positif (nilai kedua variabel cenderung meningkat bersama-sama) maupun negatif (nilai salah satu variabel cenderung meningkat ketika nilai variabel lainnya menurun).
    ...
    Berdasarkan Gambar 9, terlihat bahwa terdapat korelasi yang cukup tinggi antar fitur numerik dalam dataset, khususnya antara:
    - reading score dan writing score dengan korelasi sebesar 0.95
    - math score dan reading score dengan korelasi sebesar 0.80
    - math score dan writing score dengan korelasi sebesar 0.78
    Hal ini menunjukan bahwa nilai dari reading score dan writing score memiliki hubungan yang sangat kuat, sehingga memungkinkan terjadi redundansi informasi jika keduanya digunakan sekaligus dalam model. Dengan demikian salah satu fitur dapat dipertimbangkan untuk dihapus guna menghindari multikolienaritas, tergantung pada hasil uji performa model.

## Data Preparation
---
Pada bagian ini, terdapat empat tahap persiapan data, yaitu:
- Encoding Fitur Kategori - One-Hot Encoding.
- PCA (Principal Component Analysis).
- Train-Test-Split.
- Standarisasi.

### Encoding Fitur Kategori
Proses encoding fitur kategori menggunakan teknik one-hot-encoding. Teknik ini adalah salah satu metode dalam proses encoding fitur (feature encoding) pada data kategorikal. Tujuannya adalah untuk mengubah variabel kategorikal menjadi representasi biner yang dapat digunakan dalam algoritma pembelajaran mesin. Dalam dataset terdapat beberapa variabel kategori, maka dilakukan proses encoding ini dengan fitur get_dummies. Dan menghasilkan dataset seperti terlihat pada Tabel 5.
....
### PCA (Principal Component Analysis)
Teknik reduksi (pengurangan) dimensi adalah prosedur yang mengurangi jumlah fitur dengan tetap mempertahankan informasi pada data. Teknik pengurangan dimensi yang digunakan pada proyek ini adalah PCA. PCA adalah teknik untuk mereduksi dimensi, mengekstraksi fitur, dan mentransformasi data dari “n-dimensional space” ke dalam sistem berkoordinat baru dengan dimensi m, di mana m lebih kecil dari n.

PCA bekerja menggunakan metode aljabar linier dengan mengasumsikan bahwa sekumpulan data pada arah dengan varians terbesar merupakan yang paling penting (utama). PCA umumnya digunakan ketika variabel dalam data memiliki korelasi yang tinggi. Korelasi tinggi ini menunjukkan data yang berulang atau redundant. Karena hal inilah, teknik PCA digunakan untuk mereduksi variabel asli menjadi sejumlah kecil variabel baru yang tidak berkorelasi linier, disebut komponen utama (PC). Komponen utama ini dapat menangkap sebagian besar varians dalam variabel asli. Sehingga, saat teknik PCA diterapkan pada data, PCA hanya akan menggunakan komponen utama dan mengabaikan sisanya.

Sebelum PCA diterapkan, dilakukan analisis visualisasi fitur numerik menggunakan pairplot seperti ditampilkan pada Gambar 7. Dari visualisasi tersebut terlihat bahwa:
- Terdapat hubungan korelasi yang cukup kuat antara fitur reading score dan writing score.
- Hubungan yang cukup kuat juga terlihat antara math score dengan reading score, serta math score dengan writing score.

Hubungan yang terlihat melalui distribusi dan pola penyebaran data pada scatter plot menunjukkan bahwa ketiga fitur ini mengandung informasi yang saling berkaitan. Oleh karena itu, PCA menjadi pilihan tepat untuk mereduksi fitur-fitur numerik tersebut agar model lebih efisien dan menghindari multikolinearitas. Langkah selanjutnya adalah mengimplementasikan kelas PCA dari library Scikit-learn untuk melakukan pengurangan dimensi dan menghasilkan fitur-fitur baru yang mewakili informasi dari fitur numerik awal.
....

Setelah dilakukan proses PCA, maka akan terdaat fitur baru bernama 'average score' yang merupakan hasil rata-rata dari fitur 'Math Score', 'Reading Score', dan 'Reading Score' seperti terlihat pada Tabel ..
..

### Train-Test-Split
Selanjutnya adalah membagi dataset menjadi data latih (train) dan data uji (test). Proses pembagian dataset menggunakan library sklearn yaitu train-test-split. Proporsi pembagian adalah 80:20. Dilakukan juga pemisahkan fitur dengan target (label) yaitu average score. Hasil pembagian dataset menghasilkan sampel untuk train dataset sebesar 790 dan sampel untuk test dataset sebesar 198 dari total keseluruhan dataset yaitu sebesar 988 buah sampel.
### Standarisasi
Algoritma machine learning memiliki performa lebih baik dan konvergen lebih cepat ketika dimodelkan pada data dengan skala relatif sama atau mendekati distribusi normal. Proses scaling dan standarisasi membantu untuk membuat fitur data menjadi bentuk yang lebih mudah diolah oleh algoritma.

Standardisasi adalah teknik transformasi yang paling umum digunakan dalam tahap persiapan pemodelan. Untuk fitur numerik tidak akan melakukan transformasi dengan one-hot-encoding seperti pada fitur kategori, tetapi akan menggunakan teknik StandarScaler dari library Scikitlearn. StandardScaler melakukan proses standarisasi fitur dengan mengurangkan mean (nilai rata-rata) kemudian membaginya dengan standar deviasi untuk menggeser distribusi. StandardScaler menghasilkan distribusi dengan standar deviasi sama dengan 1 dan mean sama dengan 0. Sekitar 68% dari nilai akan berada di antara -1 dan 1.

Untuk menghindari kebocoran informasi pada data uji, hanya akan diterapkan fitur standarisasi pada data latih. Kemudian, setelah itu pada tahap evaluasi akan dilakukan standarisasi pada data uji. Hasil dari proses standarisasi fitur numerik bisa dilihat pada Tabel 7.
----

## Modeling
---
Pada tahap ini, akan dikembangkan model machine learning dengan tiga algoritma. Kemudian, dilakukan evaluasi performa setiap algoritma mana yang memberikan hasil prediksi terbaik. Ketiga algoritma yang akan digunakan pada proyek ini antara lain:
- Random Forest
- Gradient Boosting Regressor
- Linear Regresion

1. Random Forest
Random Forest merupakan algoritma machine learning yang menggabungkan beberapa pohon keputusan untuk menghasilkan prediksi yang lebih akurat. Random Forest adalah metode ensemble learning yang menggunakan banyak pohon keputusan (decision trees) untuk melakukan prediksi. Hasil prediksi diambil berdasarkan rata-rata (untuk regresi) dari semua pohon yang dibuat. Cara kerja dari 'Random Forest' yaitu model membuat banyak pohon keputusan pada subset acak dari data pelatihan, kemudian setiap pohon mengambil keputusan secara independen yang mempunyai hasil akhir rata-rata dari semua prediksi pohon (untuk regresi). Teknik ini menggunakan bagging (Bootstrap Aggregation) untuk meningkatkan stabilitas dan akurasi model serta mengurangi overfitting. Parameter yang penting dalam model ini yaitu n_estimators, max_depth, min_samples_split, min_samples_leaf, dan random_state. Random Forest mempunyai kelebihan dan kekurangan sebagai berikut:
    a. Kelebihan:
        - Mampu menangani data dengan fitur kompleks.
        - Tidak mudah overfitting.
        - Bisa menangani missing value dan data dengan tipe berbeda.
    b. Kekurangan:
        - Interpretasi model sulit karena kompleksitasnya.
        - Waktu pelatihan bisa lebih lama dibanding model sederhana.
Proses pelatihan model dilakukan menggunakan algoritma Random Forest Regressor dari pustaka Scikit-learn. Model dilatih menggunakan data latih dan kemudian dilakukan prediksi terhadap data uji untuk mengevaluasi performanya. Evaluasi dilakukan menggunakan metrik R² Score dan Mean Absolute Error (MAE).
Berdasarkan hasil evaluasi, model Random Forest memberikan performa yang sangat baik dengan nilai R² Score sebesar 0.9993, yang menunjukkan bahwa model mampu menjelaskan lebih dari 99% variansi dari data target. Sementara itu, nilai MAE sebesar 0.1427 menunjukkan bahwa rata-rata kesalahan prediksi model sangat kecil, yang berarti prediksi yang dihasilkan sangat akurat dan mendekati nilai sebenarnya.

2. Gradient Boosting Regressor
Gradient Boosting Regressor adalah model ensemble yang menggabungkan beberapa pohon keputusan secara bertahap (sekuensial), di mana setiap pohon berikutnya berusaha memperbaiki kesalahan dari pohon sebelumnya. Model ini mempunyai cara kerja yang dimulai dari awal model (misalnya mean dari target). Kemudian membuat pohon yang memprediksi residual (selisih) dari model sebelumnya dan menambahkan hasil prediksi pohon tersebut ke model yang ada. Kemudian proses ini diulang hingga jumlah iterasi tertentu. Model ini mempunyai beberapa paramenter diantaranya yaitu: 
- n_estimators: jumlah boosting stages
- learning_rate: mengontrol kontribusi tiap pohon.
- max_depth: kedalaman maksimal tiap pohon.
- subsample: proporsi sampel data yang digunakan di setiap pohon.
- loss: fungsi loss yang digunakan (default = ‘squared_error’).

Model Gradient Boosting Regressor mempunya kelebihan dan kekurangan diantaranya yaitu:
a. Kelebihan:
    - Sangat akurat dan powerful untuk berbagai jenis data.
    - Bisa disesuaikan untuk mencegah overfitting melalui parameter tuning.
b. Kekurangan:
    - Lebih rawan overfitting jika tidak dituning dengan baik.
    - Proses pelatihan lebih lambat dibanding Random Forest.

Proses pelatihan model selanjutnya dilakukan menggunakan algoritma Gradient Boosting Regressor dari pustaka Scikit-learn. Model dibangun dengan parameter n_estimators=200 dan learning_rate=0.1, yang menunjukkan jumlah pohon dalam boosting stage dan kecepatan pembelajaran masing-masing pohon.

Setelah pelatihan selesai, dilakukan prediksi terhadap data uji, dan hasil evaluasi menunjukkan performa yang sangat baik. Model menghasilkan R² Score sebesar 0.9995, yang berarti model mampu menjelaskan lebih dari 99% variansi dalam data target. Selain itu, nilai Mean Absolute Error (MAE) yang diperoleh sebesar 0.1405, menandakan bahwa rata-rata kesalahan prediksi sangat kecil dan akurat.    

3. Linear Regresion
Linear Regression adalah model statistik yang memprediksi nilai target sebagai kombinasi linear dari fitur input. Model ini paling dasar dan umum digunakan untuk permasalahan regresi.
Cara Kerja:
- Mencari garis lurus (dalam bentuk persamaan linear) yang paling sesuai dengan data.
- Fungsi loss yang digunakan biasanya adalah Mean Squared Error (MSE).
- Menggunakan metode OLS (Ordinary Least Squares) untuk meminimalkan total error.

Parameter Penting:
- fit_intercept: apakah model perlu menghitung intercept.
- normalize: apakah fitur harus dinormalisasi sebelum regresi.
- n_jobs: jumlah CPU untuk komputasi paralel.

a. Kelebihan:
- Sangat cepat dan mudah diinterpretasikan.
- Cocok untuk data yang memiliki hubungan linear.
b. Kekurangan:
- Tidak cocok untuk data yang kompleks atau memiliki hubungan non-linear.
- Rentan terhadap outlier dan multikolinearitas antar fitur.

Model ketiga yang digunakan adalah Linear Regression, yaitu model regresi dasar yang mengasumsikan hubungan linear antara variabel input dan target. Pada implementasinya, fitur dan target terlebih dahulu dilakukan proses scaling agar model dapat bekerja optimal, terutama karena Linear Regression sensitif terhadap perbedaan skala antar fitur.

Setelah proses pelatihan dan prediksi dilakukan, model menunjukkan hasil yang sangat tinggi, dengan nilai R² Score sebesar 1.0, yang artinya model mampu menjelaskan 100% variansi dari data target. Sementara itu, nilai Mean Absolute Error (MAE) yang diperoleh sangat kecil, yaitu sebesar 8.12 × 10⁻¹⁶, yang hampir mendekati nol.

Hasil ini menunjukkan bahwa Linear Regression memberikan prediksi yang sangat presisi pada data yang telah diskalakan, meskipun perlu diperhatikan bahwa performa sempurna seperti ini bisa saja terjadi karena struktur data yang sederhana atau kemungkinan overfitting jika diuji pada data lain.

## Evaluasi Model
Metrik yang digunakan dalam proyek ini untuk mengevaluasi performa model adalah MSE (Mean Squared Error), MAE (Mean Absolute Error), dan R² Score. MSE mengukur rata-rata kuadrat selisih antara nilai aktual dengan nilai prediksi. Semakin kecil nilainya, semakin baik model dalam melakukan prediksi. MAE menghitung rata-rata selisih absolut antara nilai aktual dan nilai prediksi, yang menunjukkan seberapa jauh prediksi dari nilai sebenarnya. R² Score menunjukkan seberapa baik model menjelaskan variansi data target, dengan nilai maksimum 1.0 yang berarti model sangat baik.

Evaluasi dilakukan pada ketiga model: Linear Regression, Gradient Boosting, dan Random Forest. Hasil evaluasi metrik pada data train dan test ditampilkan pada Tabel 8.

Tabel 8. Hasil Evaluasi Model pada Data Train dan Test
...

Dari Tabel 8, dapat dilihat bahwa model Gradient Boosting dan Random Forest memiliki performa yang sangat baik dengan nilai R² mendekati 1 dan error yang sangat kecil pada data train maupun test. Sebaliknya, model Linear Regression menunjukkan performa yang buruk dengan nilai R² negatif, yang berarti prediksinya lebih buruk dibandingkan rata-rata nilai target.

Berdasarkan nilai-nilai tersebut, Gradient Boosting menjadi model dengan performa terbaik dalam proyek ini karena memiliki MSE dan MAE terkecil pada data uji, serta R² Score tertinggi. Sebagai pengujian lebih lanjut, dilakukan prediksi menggunakan satu baris data dari data uji, untuk melihat seberapa dekat prediksi masing-masing model terhadap nilai sebenarnya.

Tabel 9. Hasil Prediksi dari Ketiga Model pada Data Uji
y_true	prediksi_Linear Regression	prediksi_Gradient Boosting	prediksi_Random Forest
233000	222500.0	234852.0	234851.5
Dari Tabel 9 terlihat bahwa hasil prediksi model Random Forest dan Gradient Boosting sangat mendekati nilai aktual y_true. Model Random Forest menghasilkan prediksi sebesar 234851.5, hanya selisih kecil dari nilai sebenarnya yaitu 233000. Hal ini menguatkan bahwa model ensemble seperti Random Forest dan Gradient Boosting mampu menghasilkan prediksi yang sangat akurat dalam kasus ini.
