# Laporan Proyek Machine Learning – AMIR MAHMUD

## Project Overview

Pada era e-commerce saat ini, jumlah produk yang tersedia di platform online, khususnya di sektor fashion, terus meningkat pesat. Pengguna sering kali merasa kewalahan ("choice overload") ketika harus menelusuri ribuan item untuk menemukan yang sesuai dengan preferensi mereka. fenomena ini dapat menurunkan kepuasan dan konversi karena pengguna cenderung menyerah sebelum melakukan pembelian. Hal ini dapat menurunkan efektivitas platform e-commerce dalam mencapai tujuan bisnis, terutama dalam meningkatkan engagement dan konversi penjualan.



Dalam sistem rekomendasi algoritma yang umum digunakan adalah collaborative
filtering(CF) dan content based filtering(CB). collaborative filtering adalah suatu konsep
dimana opini dari pengguna lain yang ada digunakan untuk memprediksi item yang
mungkin disukai/diminati oleh seorang pengguna. Sadangkan content based filtering
menggunakan ketersediaan konten sebuah item sebagai basis dalam pemberian
rekomendasi. <sup>1</sup>

Sistem rekomendasi telah menjadi solusi kunci untuk personalisasi pengalaman belanja online. Dengan memanfaatkan data atribut produk (content-based filtering) dan pola interaksi pengguna (collaborative filtering), platform e-commerce dapat:

1. **Mempersempit Pilihan**  
   Menyajikan subset produk yang relevan bagi setiap pengguna sehingga mereka tidak perlu menelusuri seluruh katalog.

2. **Meningkatkan Engagement & Konversi**  
   Rekomendasi yang tepat sasaran dapat meningkatkan Click-Through Rate (CTR) dan Purchase Rate.

   
[1] A. Eko Wijaya, D. Alfian, “Sistem Rekomendasi Laptop Menggunakan Collaborative Filtering dan Content-Based Filtering,” *Jurnal Computech & Bisnis*, vol. 12, no. 1, pp. 11–27, Juni 2018.
## Business Understanding

### Problem Statements

1. **Overload of Product Choices**  
   Pengguna merasa kewalahan dengan banyaknya produk fashion di platform, sehingga sulit menemukan item yang sesuai selera mereka.  
2. **Relevansi Rekomendasi yang Rendah**  
   Rekomendasi produk saat ini seringkali tidak relevan dengan preferensi atau histori pembelian pengguna, menurunkan engagement dan konversi.  

### Goals

1. **Mempermudah Penemuan Produk**  
   Menyajikan daftar produk yang sesuai dengan preferensi pengguna—berdasarkan kategori, brand, warna, dan ukuran—agar mereka lebih cepat menemukan item yang diinginkan.  
2. **Meningkatkan Engagement & Konversi**  
   Meningkatkan Click-Through Rate (CTR) dan Purchase Rate melalui rekomendasi yang relevan, sehingga mendorong peningkatan penjualan dan kepuasan pengguna.  


   ### Solution statements
   #### 1. Content-Based Filtering
- **Deskripsi**: Merekomendasikan produk dengan atribut serupa (Brand, Category, Color, Size) terhadap produk yang pernah dilihat atau disukai user.
   #### 2. Collaborative Filtering 
- **Deskripsi**: Menggunakan pola rating atau histori interaksi antar pengguna (User-User CF) atau antar produk (Item-Item CF) untuk merekomendasikan item yang disukai oleh pengguna serupa.

## Data Understanding

Dataset yang digunakan dalam proyek ini adalah **Fashion Product Recommendation Dataset**, yang berisi data interaksi pengguna dengan produk fashion di sebuah platform. Dataset ini digunakan untuk membangun sistem rekomendasi yang mampu menyarankan produk fashion yang relevan kepada pengguna berdasarkan preferensi dan karakteristik produk.

Dataset ini terdiri dari **1.000 baris data** yang mencakup informasi seperti **User ID**, **Product ID**, serta atribut konten dari setiap produk, seperti **Nama Produk**, **Brand**, **Kategori**, **Harga**, **Rating**, **Warna**, dan **Ukuran**. Dataset ini bersifat **fiktif namun realistis**, dan dapat digunakan untuk eksperimen sistem rekomendasi berbasis content dan collaborative filtering.

Dataset ini tersedia di: [Fashion Product Recommendation Dataset (Kaggle)](https://www.kaggle.com/datasets/bhanupratapbiswas/fashion-products)

### Variabel dalam Dataset:

- `User ID`: ID unik untuk setiap pengguna dalam sistem.
- `Product ID`: ID unik dari setiap produk fashion.
- `Product Name`: Nama produk fashion (misal: T-shirt, Shoes, Dress).
- `Brand`: Nama brand dari produk (misal: Adidas, Zara, H&M).
- `Category`: Kategori fashion dari produk (misal: Men's Fashion, Women's Fashion, Kids' Fashion).
- `Price`: Harga produk (dalam satuan mata uang tertentu).
- `Rating`: Rating produk yang diberikan pengguna, dalam skala 1–5.
- `Color`: Warna utama dari produk (misal: Black, White, Yellow).
- `Size`: Ukuran produk (misal: S, M, L, XL).

| User ID | Product ID | Product Name | Brand | Category | Price | Rating | Color | Size |
|---------|------------|--------------|-------|----------|-------|--------|-------|------|
| 0       | 0          | 0            | 0     | 0        | 0     | 0      | 0     | 0    |


Kondisi data bagus dan tidak terdapat nilai null

### Exploratory Data Analysis (EDA)

1. **Distribusi Brand**  
   Dari pie chart terlihat bahwa lima merek utama memiliki distribusi yang cukup seimbang. Nike menjadi merek dengan proporsi produk terbesar (21.4%), diikuti oleh Zara (20.3%), Adidas (19.8%), H&M (19.4%), dan Gucci (19.1%).

2. **Distribusi Nama Produk**  
   Produk yang paling banyak dijual adalah *Jeans* (23.1%), diikuti oleh *Shoes* (22.2%), *T-shirt* (20.1%), *Dress* (17.6%), dan *Sweater* (17.0%).

3. **Jumlah Produk per Kategori Fashion**  
   Produk paling banyak terdapat di kategori *Kids' Fashion* (sekitar 350 item), kemudian disusul oleh *Women's Fashion* dan *Men's Fashion*, yang memiliki jumlah produk hampir seimbang (sekitar 320-an item).

4. **Distribusi Harga**  
   Harga produk tersebar merata dari kisaran terendah (~$10) hingga tertinggi (~$100), dengan distribusi yang relatif seimbang, namun sedikit lebih banyak produk yang berada di kisaran harga tertinggi.

5. **Distribusi Rating**  
   Rating produk cukup bervariasi dari 1 hingga 5, dengan sedikit dominasi pada rating 3.0. Hal ini menunjukkan adanya persebaran opini konsumen yang cukup luas terhadap kualitas produk.

   
![image](https://github.com/user-attachments/assets/62dc03c3-17b6-4dab-801b-ccb8b3d37e19)
![image](https://github.com/user-attachments/assets/87559cc5-7a69-4b65-9a6c-9123870ff06c)
![image](https://github.com/user-attachments/assets/4e70e43c-e3cd-4eb9-a5da-89db9371b91c)
![image](https://github.com/user-attachments/assets/83c0dd4e-1366-4757-8560-573e75b88539)

## Data Preparation

Pada tahap ini, dilakukan serangkaian proses untuk mempersiapkan data agar dapat digunakan dalam proses pemodelan, khususnya untuk penerapan metode *Content-Based Filtering* dan *collaborative filtering* . Adapun tahapan-tahapan data preparation yang dilakukan adalah sebagai berikut:

### Data preparation untuk Content Base FIltering
1. Menggabungkan Fitur Teks

```python
df['gabung_fitur'] = (
    df['Product Name'] + ' ' +
    df['Brand'] + ' ' +
    df['Category'] + ' ' +
    df['Color'] + ' ' +
    df['Size']
)
```
Penggabungan beberapa fitur menjadi satu kolom teks bertujuan untuk membentuk representasi yang utuh dari masing-masing produk. Representasi ini mencakup berbagai atribut yang relevan terhadap preferensi pengguna, seperti nama produk, merek, kategori, warna, dan ukuran. Proses ini penting dalam sistem rekomendasi berbasis konten karena membantu dalam mengidentifikasi kemiripan antar produk berdasarkan deskripsi gabungan tersebut.
from sklearn.feature_extraction.text import TfidfVectorizer
```python
tfidf = TfidfVectorizer()
tfidf_matrix = tfidf.fit_transform(df['gabung_fitur'])
```
Teknik TF-IDF (Term Frequency - Inverse Document Frequency) digunakan untuk mengubah teks gabungan dari setiap produk menjadi representasi vektor numerik. TF-IDF tidak hanya mempertimbangkan seberapa sering suatu kata muncul dalam dokumen (term frequency), tetapi juga seberapa unik kata tersebut dalam keseluruhan dokumen (inverse document frequency). Hal ini membuat model dapat fokus pada kata-kata yang benar-benar membedakan suatu produk dari yang lain, sehingga meningkatkan efektivitas dalam penghitungan kemiripan antar produk.

Pada pendekatan Collaborative Filtering, proses data preparation dilakukan untuk menyesuaikan format data dengan model neural network. Berikut ini adalah langkah-langkah yang dilakukan:

---

### Data Preparation untuk model collaborative filtering
1. Encoding `User ID` dan `Product ID` menjadi integer

```python
user_ids   = df['User ID'].unique().tolist()
item_ids   = df['Product ID'].unique().tolist()

user_to_idx = {x:i for i, x in enumerate(user_ids)}
idx_to_user = {i:x for i, x in enumerate(user_ids)}

item_to_idx = {x:i for i, x in enumerate(item_ids)}
idx_to_item = {i:x for i, x in enumerate(item_ids)}

df['user'] = df['User ID'].map(user_to_idx)
df['item'] = df['Product ID'].map(item_to_idx)

num_users = len(user_ids)
num_items = len(item_ids)
```
Model neural network membutuhkan input dalam bentuk angka integer. Oleh karena itu, setiap User ID dan Product ID perlu diubah menjadi representasi angka yang unik dan kontinyu. Hal ini memungkinkan untuk digunakan sebagai indeks dalam embedding layer saat membangun model.


```python
min_r, max_r = df['Rating'].min(), df['Rating'].max()
df['rating_norm'] = df['Rating'].astype(np.float32).apply(
    lambda x: (x - min_r) / (max_r - min_r)
)
```


```python
x = df[['user','item']].values
y = df['rating_norm'].values

split = int(0.8 * len(df))
x_train, x_val = x[:split], x[split:]
y_train, y_val = y[:split], y[split:]
```
Proporsi spiling yang di lakukan sebesar 80/20 di mana 80% untuk training dan 20% untuk validasi
## Modeling

Pada tahapan ini, dibuat dua model sistem rekomendasi dengan pendekatan yang berbeda, yaitu:

1. **Content-Based Filtering** menggunakan  cosine similarity
2. **Collaborative Filtering** menggunakan Neuron

Kedua pendekatan ini digunakan untuk memberikan **top-N recommendation**, dengan kelebihan dan keterbatasan masing-masing.

---
### 📌 Content-Based Filtering (CBF)

Pendekatan Content-Based Filtering merekomendasikan produk berdasarkan kemiripan antar produk, tanpa melihat interaksi pengguna lain. Untuk mengukur kemiripan, digunakan **TF-IDF vectorizer** terhadap fitur produk yang relevan seperti nama produk, merek, kategori, warna, dan ukuran.

 sistem content-based filtering menggunakan metode cosine similarity untuk merekomendasikan produk yang mirip berdasarkan fitur seperti Product Name, Brand, Category, Color, dan Size.
```python
from sklearn.metrics.pairwise import cosine_similarity
cosine_sim = cosine_similarity(tfidf_matrix)
cosine_sim_df = pd.DataFrame(
    cosine_sim,
    index = df['Product Name'] + ' (' + df.index.astype(str) + ')',
    columns = df['Product Name'] + ' (' + df.index.astype(str) + ')'
)
```

| Product Name | Brand  | Category       | Color | Size | Similarity Score |
|--------------|--------|----------------|-------|------|------------------|
| Dress        | Adidas | Men's Fashion  | Black | XL   | 1.000000         |
| Dress        | Adidas | Men's Fashion  | Black | M    | 0.912964         |
| Jeans        | Adidas | Men's Fashion  | Black | XL   | 0.794962         |
| Dress        | H&M    | Men's Fashion  | Black | L    | 0.793917         |
| Dress        | H&M    | Men's Fashion  | Black | L    | 0.793917         |


Hasilnya, sistem menampilkan lima produk teratas dengan skor kemiripan tertinggi, yang menunjukkan seberapa dekat karakteristik produk tersebut dengan produk awal.
### 📌 2. Collaborative Filtering (Neural CF)
Model ini merekomendasikan produk berdasarkan interaksi historis antara pengguna dan produk. Menggunakan teknik Neural Collaborative Filtering (NCF) dengan arsitektur embedding.

```python
model = RecommenderNet(num_users, num_items, embedding_size=32)
model.compile(
    loss=keras.losses.BinaryCrossentropy(),
    optimizer=keras.optimizers.Adam(learning_rate=1e-3),
    metrics=[keras.metrics.RootMeanSquaredError()]
)

history = model.fit(
    x_train, y_train,
    validation_data=(x_val, y_val),
    epochs=50,
    batch_size=16,
    verbose=1
)
```
Dalam model Neural Collaborative Filtering di atas, setiap pengguna dan produk direpresentasikan sebagai vektor (embedding) yang dipelajari selama proses pelatihan. Model ini kemudian belajar mengenali hubungan antara pengguna dan item berdasarkan interaksi sebelumnya menggunakan kombinasi dari vektor tersebut. Model yang telah dilatih dapat memprediksi seberapa besar kemungkinan seorang pengguna menyukai item tertentu yang belum pernah mereka interaksikan sebelumnya. 

| Product Name | Brand  | Category        | Color | Size | Similarity Score |
|--------------|--------|-----------------|-------|------|------------------|
| T-shirt      | Adidas | Women's Fashion | Red   | L    | 0.812085         |
| Shoes        | Nike   | Men's Fashion   | White | S    | 0.810829         |
| T-shirt      | Gucci  | Kids' Fashion   | White | M    | 0.803815         |
| Dress        | Nike   | Women's Fashion | Red   | XL   | 0.784409         |
| Sweater      | Gucci  | Women's Fashion | Blue  | XL   | 0.782826         |

 Hasil rekomendasi menampilkan 5 produk teratas berdasarkan skor kemiripan tertinggi

## Evaluation


| Kriteria                                              | Content-Based Filtering (CBF)                                  | Collaborative Filtering (Neural CF)                                              |
| ----------------------------------------------------- | -------------------------------------------------------------- | -------------------------------------------------------------------------------- |
| **Metode**                                            |  Cosine Similarity                                     | Neural Collaborative Filtering (NCF)                                             |
| **Acuan Produk**                                      | Dress                                                          | Dress (berdasarkan interaksi pengguna)                                           |
| **Top-5 Produk yang Direkomendasikan**                | Semua produk memiliki kata kunci/kategori mirip dengan "Dress" | Tidak ada satu pun produk bertipe "Dress"                                        |
| **Akurasi (berdasarkan kesesuaian terhadap "Dress")** | **80%** (4 dari 5 produk sangat mirip atau identik)            | **0%** (tidak ada produk bertipe "Dress")                                        |
| **Relevansi Kontekstual**                             | Tinggi: Semua produk mirip dalam kategori, brand, warna        | Rendah: Produk direkomendasikan berdasarkan pola, tapi tidak mirip secara konten |
| **Kelebihan**                                         | Bisa mengenali kesamaan fitur antar produk, meskipun user baru | Bisa memberikan rekomendasi berbasis pola umum pengguna                          |
| **Kekurangan**                                        | Tidak mempertimbangkan preferensi pengguna                     | Jika data interaksi kurang, hasil bisa tidak relevan                             |



---
## ✅ Apakah Problem Statement Sudah Terjawab?

### Problem Statements

#### 1. **Overload of Product Choices**
✔ **Terjawab melalui Content-Based Filtering**  
Model Content-Based Filtering membantu pengguna menyaring ribuan produk dengan menampilkan item yang **mirip dengan produk yang pernah mereka sukai atau cari**, berdasarkan atribut seperti *brand, kategori, warna, dan ukuran*. Ini secara langsung mengurangi kebingungan pengguna karena mereka hanya melihat produk yang relevan dengan preferensi mereka.

> **Contoh:**
> Rekomendasi untuk produk "Dress" menampilkan item lain dengan brand, warna, dan kategori serupa, sehingga mempersempit pilihan dengan relevansi tinggi.

#### 2. **Relevansi Rekomendasi yang Rendah**
✔ **Terjawab melalui  Content-Based Filtering**  
  
- **Content-Based Filtering** menyesuaikan rekomendasi dengan karakteristik produk yang sudah pernah disukai oleh pengguna.
---

### 🎯 Apakah Goals Sudah Tercapai?

#### 1. **Mempermudah Penemuan Produk**
✔ **Tercapai**  
pendekatan rekomendasi  Content-Based Filtering mempercepat proses pencarian produk yang relevan, mengurangi waktu pengguna dalam menjelajah seluruh katalog produk.

#### 2. **Meningkatkan Engagement & Konversi**
✔ ** Tercapai**  
Rekomendasi yang tepat sasaran akan meningkatkan interaksi pengguna terhadap produk yang direkomendasikan (CTR) dan mendorong pembelian (conversion rate), sehingga memberikan dampak langsung pada peningkatan penjualan dan loyalitas pengguna.

---

### 🔍 Kesimpulan

### 🔍 1. Content-Based Filtering (CBF)

**Deskripsi:**  
Menggunakan pendekatan berbasis konten (fitur produk), sistem menganalisis atribut seperti *Product Name*, *Brand*, *Category*, *Color*, dan *Size* untuk merekomendasikan produk yang mirip dengan yang pernah dilihat atau disukai pengguna.

**Hasil Evaluasi:**  
Dengan produk acuan **"Dress"**, metode CBF menunjukkan **akurasi tinggi (80%)**, karena mampu mengenali produk-produk dengan kesamaan fitur secara eksplisit dan terstruktur.

---

### 🤝 2. Collaborative Filtering (Neural CF)

**Deskripsi:**  
Mengandalkan pola interaksi pengguna terhadap produk, seperti klik, rating, atau pembelian. Sistem merekomendasikan item yang disukai oleh pengguna lain dengan pola preferensi serupa, tanpa melihat konten produk secara langsung.

**Hasil Evaluasi:**  
Pada skenario pengujian berbasis produk **"Dress"**, metode ini belum memberikan hasil relevan (**akurasi 0%**) karena ketergantungan pada data interaksi pengguna, yang kemungkinan masih terbatas atau belum mencerminkan preferensi spesifik tersebut.



