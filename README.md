# Tugas 1 Big Data: ETL dengan KNIME
*05111740000107 - Shella Agustio Nainggolan <br>

![alt text](https://github.com/shellaagn/Big-Data-ETL-dengan-KNIME/blob/master/img/workflow.JPG "workflow")
***
## 1. Business Understanding <br>
   Dataset berjudul **“Students Performance in Exams”** dan diambil dari [kaggle.com](https://www.kaggle.com/spscientist/students-performance-in-exams/data#) <br>
   
   Dataset ini berisi beberapa hal yang dianggap memengaruhi performa seorang murid, mulai dari jenis kelamin, ras, tingkat edukasi orang tua, kelas persiapan sebelum ujian, hingga makan siang mereka. Ada 3 buah nilai yang dilihat sebagai contoh, yaitu nilai matematika, menulis, dan membaca.
   
   Dalam penerapannya, dataset ini bisa digunakan untuk meneliti hal-hal apa saja yang sebenarnya memengaruhi performa seorang murid dalam studinya. Ada kemungkinan tingkat edukasi orangtua juga memengaruhi edukasi anaknya, atau murid yang mendapat makan siang yang lebih sedikit akan memiliki performa lebih buruk karena susah berkonsentrasi. Dengan memproses data pada dataset ini, muncul berbagai pertanyaan dan proses yang dapat dilakukan, seperti:
   - Apa saja yang memengaruhi tingkat performa seorang murid?
   - Parameter apa yang *tidak* memengaruhi performa seorang murid?
   - Murid dengan parameter seperti apakah yang cenderung memiliki nilai lebih baik?
   - Bisakah dilakukan prediksi mengenai nilai yang akan didapat seorang murid?
   <a/><br>
## 2. Data Understanding <br>
   Dataset ini memiliki total 1000 data murid dengan 8 kolom parameter.
   Kolom yang ada, antara lain: 
   - **gender**: jenis kelamin murid. Terbagi atas *(female)* dan *(male)*
   - **race/ethnicity**: murid dibagi menjadi 5 kelompok, *(group A, group B, group C, group D, group E)*. Tidak dijelaskan secara rinci atas dasar apa pembagian tersebut dilakukan.
   - **parental level of education**: tingkat edukasi orang tua murid. Dibagi atas *(some high school)*, *(high school)*, *(some college)*, *(bachelor's degree)*, *(master's degree)*, dan *(associate's degree)*
   - **lunch**: menggambarkan makan siang murid. Terbagi atas *(standard)* dan *(free/reduced)*
   - **test preparation course**: menjelaskan kelas yang diambil murid sebelum melakukan tes. Terdiri atas *(none)*, yaitu yang tidak mengambil kelas sama sekali, serta *(completed)*, yaitu yang mengikuti semua kelas.
   - **math score**: nilai numerik matematika
   - **reading score**: nilai numerik membaca
   - **writing score**: nilai numerik menulis
  <a/><br>
## 3. Data Preparation: Splitting<br>
  Proses Split Dataset dapat dilakukan dengan node **Column Splitter** <br>
  ![alt text](https://github.com/shellaagn/Big-Data-ETL-dengan-KNIME/blob/master/img/split-file1.JPG "split file") <br>
  ![alt text](https://github.com/shellaagn/Big-Data-ETL-dengan-KNIME/blob/master/img/column-split.JPG "column splitter") <br>
  
  Dataset dibagi menjadi 2, yaitu kolom *(gender, race/ethnicity, parental level of education, lunch, test preparation course)* dan kolom *(math score, reading score, writing score)* <br>
  ![alt text](https://github.com/shellaagn/Big-Data-ETL-dengan-KNIME/blob/master/img/split-top.JPG "split top") <br>
  ![alt text](https://github.com/shellaagn/Big-Data-ETL-dengan-KNIME/blob/master/img/split-bottom.JPG "split bottom") <br>
  
  Hasil dari *split* tersebut kemudian dipisahkan ke dalam bentuk file CSV dan Database. <br>
  ![alt text](https://github.com/shellaagn/Big-Data-ETL-dengan-KNIME/blob/master/img/split-file2.JPG "split file") <br>
  <br>
## 4. Modelling: Join<br>  
  # a. Database
  Untuk memasukkan ke dalam Database, KNIME harus tersambung dengan database localhost MySQL. Hal ini bisa dilakukan menggunakan node **MySQL Connector** <br>
  ![alt text](https://github.com/shellaagn/Big-Data-ETL-dengan-KNIME/blob/master/img/connect-to-database.JPG "connect to database") <br>
  ![alt text](https://github.com/shellaagn/Big-Data-ETL-dengan-KNIME/blob/master/img/db-connection.JPG "connect to database") <br>
  
  Setelah tersambung ke database, data hasil split bisa dimasukkan melalui node **DB Writer**<br>
  ![alt text](https://github.com/shellaagn/Big-Data-ETL-dengan-KNIME/blob/master/img/write-split-to-db.JPG "db writer") <br>
  
  # b. CSV
  Untuk memasukkan data ke dalam bentuk CSV, bisa digunakan **CSV Writer** dengan pengaturan sebagai berikut: <br>
  ![alt text](https://github.com/shellaagn/Big-Data-ETL-dengan-KNIME/blob/master/img/split-csv.JPG "csv writer") <br>
  Yang nantinya akan menghasilkan file *split_csv.csv* <br>
  <br>
  Setelah data di-split ke dalam dua format yang berbeda, data tersebut masih bisa digabungkan kembali menggunakan node **Joiner.** <br>
  ![alt text](https://github.com/shellaagn/Big-Data-ETL-dengan-KNIME/blob/master/img/join-file.JPG "joiner") <br>
  ![alt text](https://github.com/shellaagn/Big-Data-ETL-dengan-KNIME/blob/master/img/join-config.JPG "joiner") <br>
  <br>
## 5. Evaluation<br>
   Proses Join akan menghasilkan tabel berisi data utuh seperti bentuk awal dataset. <br>
  ![alt text](https://github.com/shellaagn/Big-Data-ETL-dengan-KNIME/blob/master/img/joined-table.JPG "joiner") <br>

## 6. Deployment<br>
  Data yang sudah digabungkan kembali menggunakan Joiner akan disimpan ke dalam dua bentuk format, yaitu CSV dan Database. <br>
  
  Penyimpanan file ke dalam bentuk CSV bisa menggunakan **CSV Writer** dan akan disimpan dalam file *output_csv.csv* <br>
  ![alt text](https://github.com/shellaagn/Big-Data-ETL-dengan-KNIME/blob/master/img/write-end-csv.JPG "csv") <br>
  
  Penyimpanan ke dalam Database dilakukan dengan node **DB Writer**
  ![alt text](https://github.com/shellaagn/Big-Data-ETL-dengan-KNIME/blob/master/img/write-end-db.JPG "db") <br>
  ![alt text](https://github.com/shellaagn/Big-Data-ETL-dengan-KNIME/blob/master/img/write-end-db-res.JPG "db") <br>
  
***


