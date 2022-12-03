# vix-homecredit


### Problem Statement

Home Credit berupaya untuk memperluas inklusi keuangan bagi masyarakat yang belum tersentuh layanan perbankan dengan memberikan pengalaman meminjam yang positif dan aman. Untuk memastikan populasi yang kurang terlayani ini memiliki pengalaman pinjaman yang baik, 
Home Credit menggunakan berbagai data alternatif–termasuk telekomunikasi dan informasi transaksional–untuk memprediksi kemampuan pembayaran customer mereka. 
<br> Dengan mengklasifikasikan, memastikan bahwa customer mampu membayar kembali dan tidak ditolak serta pinjaman diberikan kepada customer dengan nilai pokok dan tanggal jatuh tempo pembayaran yang akan memberdayakan customer homecredit untuk berhasil pembayaran kembali.
<br>
<br>
### GOAL
Memberikan klasifikasi customer untuk memastikan bahwa customer mampu membayar kembali dan kemungkinan tidak mampu membayar kembali.
<br>
<br>
OBJECTIVE
Membuat model Machine Learning yang dapat memprediksi visitor yang memiliki potensi untuk melakukan pembayaran kembali, dengan cara membuatklasifikasi customer seperti Customer Mampu Membayar Kembali dan Customer Tidak Mampu Membayar Kembali. Segmentasi ini diharapkan menjadi bahan pertimbangan tim business agar lebih efektif dan efisien. 
<br>
<br>
### BUSINESS METRICS  
1. Meningkatkan perkiraan probabilitas (AUC)
2. Meningkatkan persentase customer yang mampu membayar kembali setelah menggunakan model yang dibuat.

### Datasheet
#### 1. Application_{train|test}.csv
Ini adalah tabel utama, dipecah menjadi dua file untuk Train (dengan TARGET) dan Test (tanpa TARGET). Data statis untuk semua aplikasi. Satu baris mewakili satu pinjaman dalam sampel data kami. The shape of data Train : (307511, 122) 
Testing data shape:  (48744, 121)
<br>
#### 2. Bureau.csv
Semua kredit klien sebelumnya yang diberikan oleh lembaga keuangan lain yang dilaporkan ke Credit Bureau.
<br>
#### 3. Bureau_Balance.csv
Saldo bulanan kredit sebelumnya di Biro Kredit. Tabel ini memiliki satu baris untuk setiap bulan riwayat setiap kredit sebelumnya yang dilaporkan ke Credit Bureau
<br>
#### 4. POS_CASH_Balance.csv
saldo bulanan dari POS (point of Sales) sebelumnya dan pinjaman tunai yang dimiliki pemohon dengan Home Credit. Tabel ini memiliki satu baris untuk setiap bulan riwayat setiap kredit sebelumnya di Home Credit (kredit konsumen dan pinjaman tunai) yang terkait dengan pinjaman dalam sampel data.
<br>
#### 5. Credit_Card_Balance.csv
saldo bulanan kartu kredit sebelumnya yang dimiliki pemohon dengan Home Credit. Tabel ini memiliki satu baris untuk setiap bulan riwayat setiap kredit sebelumnya di Home Credit (kredit konsumen dan pinjaman tunai) yang terkait dengan pinjaman dalam sampel data.
<br>
#### 6. Previous_Application.csv
Semua aplikasi sebelumnya untuk pinjaman Home Credit dari klien yang memiliki pinjaman dalam sampel. Ada satu baris untuk setiap aplikasi sebelumnya yang terkait dengan pinjaman dalam sampel data.
<br>
#### 7. Installments_Payments.csv
Riwayat pembayaran untuk kredit yang dicairkan sebelumnya di Home Credit terkait dengan pinjaman dalam sampel data.
<br>
<br>
### Analisis data eksploratif
![image](https://user-images.githubusercontent.com/26893435/205452395-7408f934-22d7-4e2f-be89-688852307733.png)<br>
Data terlihat miring dan tidak seimbang 
91,9% (Pinjaman dilunasi-0) dan 8,07% (Pinjaman tidak dilunasi-1)
<br>
![image](https://user-images.githubusercontent.com/26893435/205452446-b9be080d-17ff-46f9-a1a1-2f678f4ce0e2.png)<br>
Mayoritas customer mengambil pinjaman tunai sebesar 90.5% daripada pinjaman bergulir hanya 9.52%
<br>
![image](https://user-images.githubusercontent.com/26893435/205452494-ac84c0dd-44f6-474e-b9a7-7763c5f54bf5.png)<br>
Rentang usia customer antara 21 -29 tahun
Dengan distribusi terbanyak diantara 27 – 60 tahun
<br>
![image](https://user-images.githubusercontent.com/26893435/205452543-6f167e52-4b9e-4843-ba3d-b6815ccc9a96.png) <br>
Di antara para pemohon , Student(mahasiswa) dan Bussinessman (pengusaha) menunjukkan hasil positif 100% dalam membayar kembali pinjaman. Working (pekerja) adalah kelompok yang tinggi gagal bayar
<br>
![image](https://user-images.githubusercontent.com/26893435/205452596-cb4b5963-3d9b-4246-85f4-e25b22b0bc5a.png)<br>
Orang dengan gelar akademik (sarjana) lebih mungkin untuk melunasi kredit
<br>
![image](https://user-images.githubusercontent.com/26893435/205452642-430b156e-bcd2-4ac0-b482-19cbd30ae2b4.png)
Pemohon dengan masa kerja kurang dari 2 tahun lebih besar kemungkinannya untuk tidak membayar kembali pinjamannya.
<br>
<br>
### Data Prepocessing dan Feature Engineering
Pada proses ini dilakukan : <br>
1.Join data-data <br>
 a. Bureau data to Application data<br>
 b. Previous Application data to Application Bureau data<br>
c. POS_CASH_balance data to application_bureau_prev_data<br>
d. Installments Payments data to application_bureau_prev_data<br>
e. Credit card balance data dengan application_bureau_prev data<br>
2.Membagi data akhir menjadi data train, valid dan test.<br>
3.Featurizing the data<br>
4. Selection of features menggunakan LightGBM Classifier<br>
![image](https://user-images.githubusercontent.com/26893435/205452901-0612fa0a-923e-4dce-871b-d960a1e513b2.png)
<br> 
Grafik diatas menunjukkan 20 feature yang memberikan dampak paling besar
<br>
### Machine Learning Models
#### Logistic Regression
![image](https://user-images.githubusercontent.com/26893435/205453002-6e2ad5b3-a98b-4a76-85ad-b89735a8538b.png)
<br>
Kurva ROC untuk Logistic Regression dengan AUC=0,759
<br>
#### Random Forest
![image](https://user-images.githubusercontent.com/26893435/205453028-ad1a68b6-1896-4e0e-8ecb-8d2b7c645314.png)
<br>
Kurva ROC untuk Random Forest dengan AUC 0.749
<br>
#### Light GBM 
![image](https://user-images.githubusercontent.com/26893435/205453078-cd055378-1cf7-4cd1-840b-78e6b77619dc.png)
<br>
Kurva ROC untuk Light GBM dengan AUC 0.783
<br><br><br>
![image](https://user-images.githubusercontent.com/26893435/205453133-3803bcdf-a021-4908-b4d4-773415875311.png)
<br>
Dari ketiga model di atas dapat dilihat bahwa 'LightGBM' memiliki nilai terbaik sebesar 0.783



















