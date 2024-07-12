# Praktikum UAS Pengolahan Citra Digital B

# Authors
Nama  : Muhammad Rafi Al Anbiya

NIM   : 202231089

# Teori Pendukung mengenai Filtering Citra

Filtering citra adalah teknik dalam pengolahan citra digital yang digunakan untuk memperbaiki kualitas gambar, menghilangkan noise, dan mengekstraksi fitur tertentu. Filtering melibatkan penerapan kernel atau filter pada citra asli.

## Jenis-jenis Filter:

1. Mean Filter (Filter Rata-rata):

Mengurangi noise dengan menghitung rata-rata piksel dalam jendela filter.

Menghasilkan citra yang lebih halus.

2. Median Filter:

Mengganti piksel dengan nilai median dari jendela filter.

Efektif menghilangkan noise salt-and-pepper.

3. Gaussian Filter:

Menggunakan fungsi Gaussian untuk memberikan bobot lebih besar pada piksel pusat.

Menghaluskan citra dengan menjaga tepi lebih baik daripada mean filter.

4. Sobel Filter:

Menghitung gradien intensitas untuk deteksi tepi.

Menggunakan kernel Sobel untuk mendeteksi tepi horizontal dan vertikal.

5. Laplacian Filter:

Menghitung kedua turunan kedua dari citra.

Menekankan area dengan perubahan intensitas yang cepat (tepi).



## Aplikasi Filtering Citra:


1. Penghapusan Noise:

Menggunakan mean, median, atau Gaussian filter untuk mengurangi noise.

2. Peningkatan Kualitas:

Meningkatkan kualitas visual citra.

3. Deteksi Tepi:

Menggunakan Sobel, Laplacian, atau Canny edge detection untuk menemukan tepi.

4. Segmentasi Citra:

Membantu dalam memisahkan objek dalam citra.

## Teori pendukung yang terkait dengan filtering citra berdasarkan program yang saya buat

1. Median Filtering
Median Filtering adalah teknik filtering non-linear yang digunakan untuk mengurangi noise dalam citra. Ini bekerja dengan mengganti setiap piksel dengan nilai median dari semua piksel di sekitarnya dalam jendela filter. Median filtering sangat efektif dalam menghilangkan noise salt-and-pepper.

Dalam program saya di atas:

Gambar asli (img) difilter menggunakan cv2.medianBlur dengan kernel 9x9.

Hasilnya ditampilkan berdampingan dengan gambar asli untuk perbandingan.

2. Gray Conversion
Mengonversi citra berwarna menjadi grayscale adalah langkah umum dalam pengolahan citra untuk menyederhanakan komputasi dan analisis. Grayscale mengurangi citra menjadi satu kanal dengan intensitas cahaya.

Dalam program saya di atas:

Gambar berwarna (img) dikonversi menjadi grayscale (img_gray).

3. Mean Filtering
Mean Filtering adalah teknik filtering linear yang digunakan untuk menghaluskan citra dan mengurangi noise. Ini bekerja dengan mengganti setiap piksel dengan rata-rata nilai piksel di sekitarnya dalam jendela filter. Mean filtering dapat menghasilkan citra yang lebih halus, tetapi juga dapat mengaburkan tepi.

Dalam program saya di atas:

Mean filtering diterapkan secara manual dengan menghitung rata-rata nilai piksel di sekitarnya dalam jendela 3x3.

Hasilnya disimpan dalam output1 dan dibandingkan dengan citra asli (copyCitra1).

4. Visualisasi

Matplotlib digunakan untuk memvisualisasikan citra sebelum dan sesudah filtering. Visualisasi sangat penting untuk memahami efek dari setiap teknik filtering yang diterapkan.

Dalam program saya di atas:

plt.subplots digunakan untuk membuat subplot yang menampilkan citra asli dan citra yang difilter (median dan mean).


## Langkah Langkah Pengerjaan

```python
import cv2
import matplotlib.pyplot as plt #untuk memvisualisasi data
import numpy as np #untuk membaca angka 
```

cv2 adalah OpenCV, library untuk pengolahan citra.

matplotlib.pyplot adalah modul dari Matplotlib untuk visualisasi data dalam bentuk grafik.

numpy adalah library untuk komputasi numerik dengan array dan matriks.

```python
img = cv2.imread("fotooo.JPEG")
```
cv2.imread("fotooo.JPEG") membaca gambar dari file.

```python
img.shape # membuat variabel dalam baris dan kolom dalam shape citra
```
img.shape mendapatkan dimensi gambar (baris, kolom, kanal warna).

```python
[baris, kolom] = img.shape[:2]
```
[baris, kolom] = img.shape[:2]: Menyimpan height dalam variabel baris dan width dalam variabel kolom.

```python
img = cv2.cvtColor(img, cv2.COLOR_BGR2RGB)
```
OpenCV Default Format: OpenCV membaca gambar dalam format BGR (Blue, Green, Red).
Konversi Warna: cv2.cvtColor adalah fungsi untuk mengonversi ruang warna gambar.
Parameter cv2.COLOR_BGR2RGB: Menentukan bahwa konversi yang dilakukan adalah dari BGR ke RGB.

```python
img_median = img.copy()
img_median_after = cv2.medianBlur(img_median, 9)

fig, axis = plt.subplots(1, 2, figsize = (10, 10))
ax = axis.ravel()

ax[0].imshow(img, cmap='gray')
ax[0].set_title('citra asli')

ax[1].imshow(img_median_after, cmap='gray')
ax[1].set_title('after filter median')
plt.show()
```
codingan diatas ini mengilustrasikan proses penggunaan median filter pada sebuah gambar menggunakan Python dan OpenCV. Pertama, gambar asli dibaca dan disalin untuk mempertahankan keaslian data. Kemudian, filter median diterapkan dengan kernel berukuran 9x9 untuk mengurangi noise yang mungkin hadir, seperti noise salt-and-pepper. Hasil dari proses filtering ini kemudian ditampilkan dalam sebuah subplot menggunakan Matplotlib, di mana subplot pertama menampilkan gambar asli dalam skala warna abu-abu, sementara subplot kedua menampilkan gambar setelah diterapkan filter median dengan judul yang sesuai untuk membedakan antara keduanya. Ini memungkinkan pengamat untuk memvisualisasikan dan membandingkan perbedaan sebelum dan sesudah penerapan filter median dengan jelas.

```python
img_gray = cv2.cvtColor(img, cv2.COLOR_BGR2GRAY)
```
img_gray = cv2.cvtColor(img, cv2.COLOR_BGR2GRAY) berfungsi untuk mengonversi sebuah gambar dari format BGR (Blue, Green, Red) ke grayscale (skala keabuan) menggunakan library OpenCV dan Python. Proses ini penting dalam pengolahan citra karena mengubah gambar berwarna menjadi representasi yang hanya menggunakan satu kanal warna (intensitas keabuan) daripada tiga kanal (RGB). Dengan mengurangi kompleksitas warna, citra grayscale mempermudah analisis citra, terutama untuk teknik-teknik seperti deteksi tepi, segmentasi objek, atau pengenalan pola. Hasil dari konversi ini, disimpan dalam variabel img_gray, dapat digunakan untuk berbagai tujuan analisis lebih lanjut sesuai dengan kebutuhan aplikasi pengolahan citra.

```pyhton
plt.imshow(img_gray, cmap='gray')
```
plt.imshow(img_gray, cmap='gray') digunakan dalam Matplotlib untuk menampilkan gambar yang sudah dikonversi menjadi grayscale. Fungsi plt.imshow() digunakan untuk menampilkan data gambar dalam bentuk plot, dengan parameter utama img_gray yang merupakan variabel yang menyimpan citra grayscale. Pengaturan cmap='gray' pada fungsi imshow() menunjukkan bahwa gambar akan ditampilkan dalam skala keabuan (grayscale), di mana setiap piksel direpresentasikan sebagai tingkat keabuan yang berkisar dari hitam hingga putih.

```python
copyCitra1 = img_gray.copy().astype(float)

m1, n1 = copyCitra1.shape
output1 = np.empty([m1, n1])

print("shape copy citra 1 : ", copyCitra1.shape)
print("shape output citra 1 : ", output1.shape)

print("m1 : ", m1)
print("n1 : ", n1)
print()
```
Program diatas ini dimulai dengan membuat salinan dari gambar grayscale img_gray menggunakan img_gray.copy(). Kemudian, salinan tersebut dikonversi menjadi tipe data float dengan .astype(float), yang berguna untuk memastikan keakuratan dalam operasi pengolahan citra yang memerlukan perhitungan numerik presisi tinggi.

Setelah salinan copyCitra1 dibuat, program mengambil dimensi gambar tersebut menggunakan copyCitra1.shape dan menyimpannya dalam variabel m1 dan n1. Variabel output1 diinisialisasi sebagai array kosong menggunakan np.empty([m1, n1]), yang akan digunakan untuk menampung hasil dari proses pengolahan citra yang akan dilakukan selanjutnya.

Hasil cetakannya menampilkan informasi mengenai dimensi gambar (copyCitra1.shape) dan dimensi array output (output1.shape), serta nilai m1 dan n1 yang menunjukkan jumlah baris dan kolom dari gambar yang sedang diproses.

```python
for baris in range (0, m1-1) :
    for kolom in range (0, n1-1) :
        a1 = baris
        b1 = kolom
        jumlah = copyCitra1[a1-1, b1-1] + copyCitra1[a1-1, b1] + copyCitra1[a1-1, b1+1] +\
            copyCitra1[a1, b1-1] + copyCitra1[a1, b1] + copyCitra1[a1, b1+1] +\
            copyCitra1[a1+1, b1-1] + copyCitra1[a1+1, b1] + copyCitra1[a1+1, b1+1]
        output1[a1, b1] = 1/9 * jumlah
```
program diatas ini merupakan proses untuk melakukan operasi filtering rata-rata (mean filtering) pada gambar grayscale yang direpresentasikan oleh array copyCitra1. Proses ini dilakukan dengan mengiterasi melalui setiap piksel dalam gambar menggunakan nested loop (loop bersarang) yang mengambil nilai baris dan kolom dari gambar yang sudah disiapkan sebelumnya.

Di setiap iterasi, nilai a1 dan b1 merepresentasikan indeks baris dan kolom saat ini dalam iterasi. Untuk setiap piksel pada posisi (a1, b1), dilakukan perhitungan untuk menghitung nilai rata-rata intensitas keabuan di sekitar piksel tersebut. Ini dilakukan dengan menjumlahkan intensitas keabuan dari piksel itu sendiri dan delapan piksel tetangganya, yang direpresentasikan oleh nilai jumlah.

Setelah nilai rata-rata dihitung, hasilnya kemudian disimpan kembali ke dalam array output1 pada posisi yang sesuai (a1, b1). 


```python
fig, axis = plt.subplots(1,2, figsize=(10,10))
ax = axis.ravel()

ax[0].imshow(copyCitra1, cmap='gray')
ax[0].set_title("Citra Asli")

ax[1].imshow(output1, cmap='gray')
ax[1].set_title("Citra setelah Mean")
plt.show()
```
program diatas ini digunakan untuk menampilkan dua gambar dalam satu jendela menggunakan Matplotlib. Pertama, plt.subplots(1, 2, figsize=(10, 10)) membuat sebuah figure dengan satu baris dan dua kolom, yang berarti kita akan memiliki dua subplot. ax = axis.ravel() mengubah array dari dua axis (sumbu) menjadi satu dimensi untuk kemudahan mengaksesnya.

Pada ax[0].imshow(copyCitra1, cmap='gray'), gambar asli (copyCitra1) ditampilkan dalam skala abu-abu (grayscale) di subplot pertama (ax[0]). Kemudian, ax[0].set_title("Citra Asli") menambahkan judul "Citra Asli" pada subplot tersebut.

Pada ax[1].imshow(output1, cmap='gray'), gambar hasil proses (dalam hal ini setelah penerapan filter mean atau rata-rata) ditampilkan dalam skala abu-abu di subplot kedua (ax[1]). ax[1].set_title("Citra setelah Mean") menambahkan judul "Citra setelah Mean" pada subplot ini.

Terakhir, plt.show() digunakan untuk menampilkan jendela output dengan kedua subplot (gambar asli dan gambar hasil setelah filter mean) di dalamnya. 















