# Google Play Store Analytics
<img src="https://raw.githubusercontent.com/fafilia/capstone-UIFlask/master/full_capstone.png">

## Introduction
Projek ini dikembangkan sebagai salah satu capstone project dari Algoritma Academy Data Analytics Specialization. Deliverables yang diharapkan adalah dapat membangun sebuah aplikasi web sederhana (dashboard) menggunakan framework Flask. Capstone ini akan fokus pada tampilan user interface Flask. 

## Data Summary
Data yang digunakan pada capstone project ini adalah data hasil scraping dari Google Playstore App. Data Google Playstore App terdiri dari beberapa variabe dengan rincian sebagai berikut:
- `App` : Nama aplikasi                
- `Category` : Kategori aplikasi
- `Rating` : Rating keseluruhan yang diberikan oleh user aplikasi(ketika di scrap)
- `Reviews` : Jumlah review yang diberikan oleh user aplikasi(ketika di scrap)
- `Size` : Ukuran aplikasi(ketika di scrap)           
- `Installs` : Jumlah user yang menginstall/mendownload aplikasi(Ketika di scrap)     
- `Type` : Tipe aplikasi (berbayar/gratis)       
- `Price` : Harga aplikasi (ketika di scrap)        
- `Content Rating` : Kelompok usia aplikasi ini ditargetkan - Children / Mature 21+ / Adult   
- `Genres` : Genre aplikasi.        
- `Last Updated` : Tanggal kapan aplikasi terakhir diperbarui di Play Store (ketika discrap) 
- `Current Ver` : Versi aplikasi saat ini tersedia di Play Store (ketika discrap)   
- `Android Ver` : Minimum versi Android yang diperlukan (ketika discrap) 

## Dependencies
- Flask
- Matplotlib
- Pandas
- Numpy

## Rubrics
Pada capstone ini, diharapkan untuk dapat membangun sebuah aplikasi Flask yang fokus pada tampilan user interface. Beberapa bagian yang harus diperhatikan adalah sebagai berikut:

### 1. Setting Repository Github dan Environment
- Repository 

a. Membuat repository baru di Github

b. Clone repository tersebut ke local dengan git clone
- Environment 

a. Created virtual environment called "capstone-flask"

Hal pertama yang harus dilakukan adalah melakukan pengaturan environment conda. Untuk menyiapkan conda environment dan kernel, gunakan command berikut:
```
conda create -n capstone-flask python=3.10
conda activate capstone-flask

conda install ipykernel
python -m ipykernel install --user --name capstone-flask
```

b. Install packages: pandas, flask, matplotlib, dan numpy

Seluruh dependecies telah di-export ke dalam file requirements.txt. Oleh karena itu untuk melakukan install packages, dapat menggunakan perintah berikut:
```
pip install -r requirements.txt --user
```

### 2. Data Preproses and Exploratory Data Analysis
Pada tahap praproses ini, diminta untuk melakukan praproses data seperti menghapus data yang duplikat, mengubah tipe data dan memodifikasi nilai data.
```
playstore.Category(subset ="App", keep = 'first', inplace=True) 
playstore.drop([10472], inplace=True)
# Buang tanda koma(,) dan tambah(+) kemudian ubah tipe data menjadi integer
playstore.Category = playstore.Category.astype('category')
playstore.Installs = playstore.apply(lambda x: x.replace(',',''))
playstore.Installs = playstore.apply(lambda x: x.replace('+'.''))
```
### 3. Data Wrangling
- Pada tahap ini akan dilakukan grouping dan agregasi data. Data wrangling digunakan untuk menyiapkan data yang tepat sesuai analisis yang diminta. Pada capstone ini terdapat objek dictionary dengan nama `stats`. Sebagai gambaran pada objek `stats` terdapat variabel `rev_tablel` dimana harus melakukan grouping dan agregasi data yang digunakan untuk membuat data table. Output:
<img src="https://raw.githubusercontent.com/fafilia/capstone-UIFlask/master/table_rev.PNG" width=400>

### 4. Data Visualization
- Membuat atau menduplikasi bar plot yang menggambarkan top 5 Category pada Google Playstore
- Membuat atau menduplikasi scatter plot yang menggambarkan sebaran aplikasi jika dilihat berdasarkan Review, Rating, dan jumlah aplikasi yang terinstall.
- Membuat atau menduplikasi histogram plot untuk melihat distribusi ukuran aplikasi 
- Membuat 1 plot tambahan bebas yang dapat merepresentasikan insight di dalam data

### 5. Build Flask App
Mengacu pada poin ke empat Data Visualization di atas, selain membuat plot baru, harus mendemonstrasikan bagaimana cara merender plot tersebut pada aplikasi Flask dan menampilkannya pada templates / halaman html. Yang perlu diperhatikan adalah pada bagian `app.py`:
```
render_templates('index.html', stats=stats, result=result, result1=result1, result2=result2, result3=result3, result4=result4)
```
dan pada `templates/index.html` perlu memanggil source plot.png tempat menyimpan gambar plot tersebut.
```
<img src="data:image/png;base64,{{ result2 }}" height="450" width=500>
```
