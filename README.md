# Laporan Proyek Akhir Kelas Machine Learning Terapan - Putri Nur Aini Mahfudz
---
## Domain Proyek

Domain untuk proyek *machine learning* ini adalah bidang literasi. Proyek yang dibangun adalah sistem rekomendasi buku menggunakan *collaborative filtering*.

## **Latar Belakang**

Di zaman digital ini, hal yang menjadi tuntutan perkembangan globalisasi adalah literasi. Kemajuan zaman dan cara berliterasi harus seimbang. Terutama bagi generasi mellenial atau yang dikenal sebagai generasi digital. Di era digital harus memberikan sumbangan berupa kesadaran akan pentingnya pengetahuan yang mendalam [1].

Pada zaman yang dipenuhi oleh penerapan teknologi ini harusnya dapat lebih mudah dan cepat dalam meningkatan budaya literasi di setiap tempat, salah satunya dengan membaca buku melalui perpustakaan online. Agar user memiliki pengalaman pengguna yang baik dalam menggunakan perpustakaan online, maka perlu  diterapkan salah satu hasil produk dari *machine learning* yaitu sistem rekomendasi untuk memudahkan user memilih buku yang diminati untuk dibaca.

Oleh karena itu, saya berniat untuk membuat sistem rekomendasi buku yang kelak bisa diterapkan pada aplikasi semacam perpustakaan online.


## Business Understanding

### Problem Statements
Berdasarkan latar belakang di atas, berikut ini rumusan masalah yang dapat diselesaikan pada proyek ini:
- Bagaimana cara melakukan pengolahan data pada dataset Books.csv, Ratings.csv, dan Users.csv agar dapat digunakan pada model *machine learning*?
- Bagaimana cara membuat model *machine learning* untuk merekomendasikan buku dengan menggunakan *collaborative filtering*?

### Goals
Tujuan dari proyek ini adalah:
- Mengetahui cara melakukan pengolahan terhadap dataset Books.csv, Ratings.csv, dan Users.csv.
- Mengetahui cara membuat model *machine learning* untuk merekomendasikan buku dengan menggunakan *collaborative filtering*.

### Solution Statements
Pada proyek ini, saya akan membuat sistem rekomendasi dengan menggunakan *collaborative filtering*.

*Collaborative Filtering* adalah sebuah metode yang merekomendasikan item berdasarkan kemiripan user dalam hal memilih atau memberi nilai kepada item.


## Data Understanding

Dataset yang digunakan pada proyek ini diambil dari https://www.kaggle.com/datasets/arashnic/book-recommendation-dataset. 

Dataset ini terdiri atas 3 file, yaitu Books.csv, Ratings.csv, dan Users.csv.

Dalam dataset ini terdapat 3 file csv, di antaranya:

1. Books.csv

    Penjelasan mengenai variabel yang ada pada dataset Books.csv adalah sebagai berikut: 

    - ISBN: merupakan kode ISBN dari buku
    - Book-Title: merupakan judul dari buku
    - Book-Author: merupakan author atau penulis dari buku
    - Year-Of-Publication: merupakan tahun terbit dari buku  
    - Publisher: merupakan publisher atau penerbit dari buku  
    - Image-URL-S: merupakan URL yg menunjukkan foto buku berukuran small
    - Image-URL-M: merupakan URL yg menunjukkan foto buku berukuran medium
    - Image-URL-L: merupakan URL yg menunjukkan foto buku berukuran large


2. Ratings.csv

    Penjelasan mengenai variabel yang ada pada dataset Ratings.csv adalah sebagai berikut:

    - User-ID: merupakan id dari user
    - ISBN: merupakan kode ISBN dari buku
    - Book-Rating: merupakan rating buku yang diberikan user (rentang 1-10)


3. Users.csv

     Penjelasan mengenai variabel yang ada pada dataset Users.csv adalah sebagai berikut:

    - User-ID: merupakan id dari user
    - Location: merupakan lokasi dari user
    - Age: merupakan usia atau umur dari user
  

Berikut adalah tahapan yang diperlukan untuk memahami dataset sebelum dilakukan *preparation*
- meload dataset 
- melihat isi dari dataset Books.csv, Ratings.csv, dan Users.csv, dan melakukan eksplorasi pada ke-tiga data tersebut.


## Data Preparation

Berikut adalah tahapan yang dilakukan dalam proses data *preparation*:
- menggabungkan dataset books, ratings, dan users.
- melihat jumlah baris dan kolom pada dataset yang telah digabungkan.
- mengecek jumlah data kosong pada setiap kolom.
- mengecek apakah ada data yang terduplikat.
- melihat visualisasi distribusi rating buku (ternyata data rating tidak seimbang).
- menghapus kategori yang tidak diperlukan pada kolom. kategori yang dihapus adalah rating dengan nilai 0 pada kolom Book-Rating.
- mengecek visualisasi distribusi rating buku yang sudah ditangani data tidak seimbangnya.
- Menghapus data yang mempunyai nilai null.
- melakukan encoding, di antaranya adalah: menyandikan (encode) fitur 'User-ID' dan fitur 'ISBN' ke dalam indeks integer, memetakan ‘User-ID’ dan ‘ISBN’ ke dataframe yang berkaitan, kemudian mengecek beberapa hal dalam data seperti jumlah user, jumlah isbn, kemudian mengubah nilai rating menjadi float.
- melakukan pengacakan data. hal ini dilakukan agar distribusi data menjadi acak.
- membagi dataset menjadi dua bagian. 80% untuk data training, dan 20% untuk data validasi.


## Modeling

Setelah melakukan data *preparation*, langkah selanjutnya yang dilakukan adalah membuat model *machine learning*.

Saya menggunakan metode *collaborative filtering* dalam menyusun sistem rekomendasi ini, yang dibuat berdasarkan rating buku yang ditelah diberikan oleh user.

Pada tahap ini, model menghitung skor kecocokan antara user dan ISBN dengan teknik embedding.

Pertama, lakukan proses embedding terhadap data user dan ISBN. 

Kemudian melakukan operasi perkalian dot product antara embedding user dan ISBN. 

Selain itu, dapat juga menambahkan bias untuk setiap user dan ISBN. Skor kecocokan ditetapkan dalam skala [0,1] dengan fungsi aktivasi sigmoid.

Lalu membuat class RecommenderNet dengan keras Model class.

Proses compile terhadap model menggunakan Binary Crossentropy untuk menghitung loss function, Adam sebagai optimizer, dan RMSE sebagai metrics evaluation.

Model yang telah dibangun menghasilkan top-10 rekomendasi buku berikut ini: 

![Top10](https://user-images.githubusercontent.com/99728385/195653136-6400dd3b-d7c3-4411-9e41-76e385da261f.PNG)


Kelebihan dari metode ini adalah hasil rekomendasi yang beragam dan bersifat relevan dan baru, sedangkan kekurangan dari metode ini yaitu tidak dapat menghasilkan rekomendasi dikarenakan tidak adanya informasi preferensi untuk pengguna baru dan item baru *(cold-start problem)*.


## Evaluation

Setelah membangun model *machine learning*, kemudian dilakukan evaluasi kinerja model yang dihasilkan dengan menggunakan menggunakan metrik RMSE (Root Mean Square Error).

Didapatkan metrik RMSE sebagai berikut, agar lebih mudah dimengerti maka dapat ditampilkan dengan visualisasi:

![metrikRMSE](https://user-images.githubusercontent.com/99728385/195653070-401bd62a-c05d-43e6-88d2-bd5065a517f0.PNG)


## Referensi
[1] Ginting, Eva Susanti, "Penguatan Literasi di Era Digital", *Prosiding Seminar Nasional PBSI-III*, Tahun 2020.
