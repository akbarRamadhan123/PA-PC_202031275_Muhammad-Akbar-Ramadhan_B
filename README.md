
# Mean Filtering dan Median Filtering

## 1. Mean Filtering
Mean Filtering merupakan salah satu image smooting yang digunakan untuk mengurangi noise pada gambar.Mean Filtering salah satu filter yang bekerja dengan menggantikan intensitas nilai pixel dengan rata-rata dari nilai pixel tersebut dengan nilai pixel-pixel tetangganya. Menurut Usman (2005:61) salah satu filter linier adalah filter rata-rata (Filter Mean) dari intensitas pada beberapa pixel lokal dimana setiap pixel akan digantikan nilainya dengan rata-rata dari nilai intensitas pixel tersebut dengan pixel-pixel tetangganya, dan jumlah pixel tetangga yang dilibatkan tergantung pada filter yang dirancang.Mean Filter adalah mengganti nilai pixel pada posisi (x,y) dengan nilai rata-rata pixel yang berada tetangga disekitarnya. Luasan jumlah pixel tetangga ditentukan sebagai masking/kernel/window yang berukuran misalkan 2x2, 3x3, 4x4, dan seterusnya. Kemudian akan dilakukan mean filter untuk citra M dengan menggunakan matriks kernel (3x3). Pixel m(2,2) = 3, akan diubah menjadi Selain mean filtering yang merupakan proses filter linier, terdapat pula pendekatan filter pembobotan (weighted filter).Referensi (https://media.neliti.com/media/publications/150036-ID-analisa-perbandingan-metode-filter-gauss.pdf)

untuk mean sendiri dibuat melalui manual dengan menggunakan rumus mean filtering 
![Mean Filtering](https://epochabuse.com/wp-content/uploads/2021/01/arithmetic-mean-filter-formula.png)
X = Nilai rata-rata(Mean)

n = Jumlah data i

x = Nilai ke -i

i = Nilai Awal

Mean filtering yang digunakan untuk efek smoothing ini merupakan jenis spatial filtering, yang dalam prosesnya mengikutsertakan piksel-piksel disekitarnya.

## 2. Median Filtering
Menurut Rinaldi Munir (2004:126) menjelaskan filter median sebagai suatu jendela yang memuat sejumlah pixel ganjil. Jendela digeser titik demi titik pada seluruh daerah citra. Pada setiap pergeseran dibuat jendela baru. Titik tengah dari jendela ini diubah dengan nilai median dari jendela tersebut.

Median filter mengganti nilai suatu piksel dengan
median nilai tingkat keabuan dari pixel tetangga (nilai
asli piksel digunakan juga pada saat perhitungan nilai
median tersebut). Media filter ini cukup popular
karena beberapa tipe gangguan acak (seperti salt
noise, pepper noise. Teknik ini mampu mengurangi gangguan yang lebih baik dibandingkan dengan model linear smooting dengan ukuran yang sama. 

Median filter mengubah suatu titik dengan tingkat
keabuan yang berbeda menjadi lebih mirip dengan
tetangganya. Selain itu juga median filter mengganti
nilai cluster pixel terisolasi, yang lebih terang atau
gelap dibandingkan dengan pixel tetangganya serta luasannya kurang dari n2/2, dengan nilai median dari
masking nxn. Sehingga dapat dikatakan bahwa noise
yang dihilangkan akan memiliki nilai sama dengan
intensitas median tetangganya. Untuk Rumus dari median filtering sendiri yaitu 
![alt text](https://media.cheggcdn.com/media/0d6/0d605372-6b05-4bff-a017-b80cb83247d3/php3jARek.png)

Median filtering mengambil area tertentu pada
citra sesuai dengan ukuran mask yang telah
ditentukan (umumnya 3×3), kemudian dilihat setiap
nilai pixel pada area tersebut, dan nilai tengah pada
area diganti dengan nilai median (Dwayne, 2000).
Cara memperoleh nilai median adalah: nilai keabuan
dari titik-titik pada matriks diurutkan dari nilai
terkecil hingga yang terbesar, kemudian ditentukan
nilai yang berada di tengah dari deret piksel.

Referensi : (https://media.neliti.com/media/publications/150036-ID-analisa-perbandingan-metode-filter-gauss.pdf)

## 3. Proses Mean Filtering dengan manual
Untuk melakukan Mean Filtering disini menggunakan bahasa pemrograman python dengan menggunakan bantuan library opencv dan numpy untuk mempermudah proses smooting gambar. Langkah pertama yaitu masukkan gambar yang akan di olah 

import cv2 
import numpy as np 

###  membaca gambar

img = cv2.imread('sample.png', 0) 

### Mendapatkan jumlah baris dan kolom dari gambar
m, n = img.shape 

### Mengembangkan masker filter rata-rata (3, 3)
mask = np.ones([3, 3], dtype = int) 
mask = mask / 9

### Melingkarkan Mask 3X3 di atas gambar
img_new = np.zeros([m, n]) 
  
for i in range(1, m-1): 
    for j in range(1, n-1): 
        temp = img[i-1, j-1]*mask[0, 0]+img[i-1, j]*mask[0, 1]+img[i-1, j + 1]*mask[0, 2]+img[i, j-1]*mask[1, 0]+ img[i, j]*mask[1, 1]+img[i, j + 1]*mask[1, 2]+img[i + 1, j-1]*mask[2, 0]+img[i + 1, j]*mask[2, 1]+img[i + 1, j + 1]*mask[2, 2] 
         
img_new[i, j]= temp 
          
img_new = img_new.astype(np.uint8) 
cv2.imwrite('blurred.tif', img_new) 

Dari Proses diatas untuk melakukan mean secara manual cukup sulit karena harus melakukan masking pada gambar secara manual.

## 4. Proses Median Filtering
Untuk proses Median Filtering disini akan menggunakan Library OpenCV sebelumnya import dulu library OpenCV dan matplotlib

### import Library
import cv2
import matplotlib.pyplot as plt

### Upload Gambar dari perangkat
img = cv2.imread("IMG_8688.jpg")
img = cv2.cvtColor(img, cv2.COLOR_BGR2RGB)

### Penggunaan Filter mean (kernel size : ukuran blur kernel)
mf = cv2.blur(img, ksize = (5,5))

### Menampilkan Hasil Penggunaan Mean Filtering pada gambar
plt.figure()
plt.imshow(mf)
plt.title("Mean Filtered image")
plt.axis("OFF")

### Membuat Median Filter pada gambar
mb = cv2.medianBlur(img2, ksize = 3)

### Menampilkan Hasil Penggunaan Median Filtering pada Gambar
plt.figure()
plt.imshow(mb)
plt.title("Median Filtered image")
plt.axis("OFF")

Dari proses diatas diketahui bahwa dengan menggunakan library openCV lebih mudah dibanding dengan manual karena pada library openCV sudah dilakukan proses terlebih dahulu sehingga ketika ingin menggunakan median filtering kita tinggal memanggil fungsinya saja.

Referensi Jurnal:
1. https://www.researchgate.net/publication/335946897_IMAGE_SMOOTHING_MENGGUNAKAN_MEAN_FILTERING_MEDIAN_FILTERING_MODUS_FILTERING_DAN_GAUSSIAN_FILTERING

2. https://media.neliti.com/media/publications/150036-ID-analisa-perbandingan-metode-filter-gauss.pdf 

3. https://media.neliti.com/media/publications/323774-image-smoothing-menggunakan-mean-filteri-5a96e231.pdf
