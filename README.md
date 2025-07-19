# Implementasi Neural Style Transfer Menggunakan VGG19

Laporan proyek ini mendemonstrasikan implementasi algoritma **Neural Style Transfer** untuk menggabungkan konten dari lukisan **Mona Lisa** dengan gaya artistik dari lukisan karya **Pablo Picasso** menggunakan model VGG19 dan TensorFlow.

---

### **Disusun oleh:**

| Nama                         | NIM          |
| :---------------------       | :----------- |
| Nero Caesar Suprobo          | 442023611083 |
| Muhammad Mishbahul Muflihin  | 442023611074 |
| Muhammad Haekal              | 442023611089 |
| Mhd Nurdin Al-Kahfi          | 442023611067 |
| Muhammad Akmal Najib Gunawan | 442023611062 |

**Teknik Informatika**
**Universitas Darussalam Gontor**
**2025**

---

## **1. Latar Belakang**

Neural Style Transfer (NST) adalah teknik *computer vision* yang memungkinkan pembuatan karya seni baru dengan menggabungkan dua gambar: gambar konten dan gambar gaya. Teknik ini memanfaatkan *Convolutional Neural Networks* (CNN), khususnya model **VGG19**, untuk memisahkan representasi konten dan gaya dari sebuah gambar. Proyek ini bertujuan untuk mengimplementasikan NST untuk mentransfer gaya lukisan Picasso ke struktur lukisan Mona Lisa.

---

## **2. Metodologi**

#### **Arsitektur Model: VGG19**
Kami menggunakan arsitektur **VGG19** yang telah dilatih sebelumnya pada dataset ImageNet sebagai *feature extractor* statis.
* **Fitur Konten**: Diekstraksi dari lapisan konvolusi tingkat menengah (`block5_conv2`) untuk menangkap struktur objek utama.
* **Fitur Gaya**: Diekstraksi dari beberapa lapisan konvolusi (`block1_conv1` hingga `block5_conv1`). **Matriks Gram** dari *feature maps* lapisan-lapisan ini digunakan untuk merepresentasikan tekstur dan pola visual.

#### **Loss Function**
Proses optimisasi bertujuan untuk meminimalkan *total loss* yang merupakan gabungan dari:
1.  **Content Loss**: *Mean Squared Error* (MSE) antara fitur konten gambar hasil dengan gambar konten asli.
2.  **Style Loss**: MSE antara Matriks Gram gambar hasil dengan gambar gaya asli.

**Total Loss** = `alpha * content_loss + beta * style_loss`

---

## **3. Implementasi**

#### **Library yang Digunakan**
* **TensorFlow & Keras**: Untuk memuat model VGG19 dan menjalankan proses optimisasi.
* **NumPy**: Untuk operasi numerik.
* **Pillow (PIL)** & **Matplotlib**: Untuk memanipulasi dan memvisualisasikan gambar.

#### **Proses Optimisasi**
1.  Inisialisasi gambar output (misalnya, dari gambar konten atau *noise*).
2.  Secara iteratif, hitung *total loss*.
3.  Gunakan optimizer (misalnya, **Adam**) untuk menghitung gradien dari *loss* terhadap piksel gambar output.
4.  Perbarui piksel gambar output untuk meminimalkan *loss*.
5.  Ulangi proses selama beberapa iterasi hingga hasilnya konvergen.

---

## **4. Hasil dan Evaluasi**

Evaluasi performa model ini bersifat kualitatif dan subjektif, dinilai berdasarkan visual.

| Hasil Akhir |
| :---: |
| ![Hasil Style Transfer](dataset/Result.png) |

Hasil akhir menunjukkan bahwa model berhasil mempertahankan struktur wajah Mona Lisa sambil mengadopsi palet warna, tekstur, dan goresan kuas yang khas dari gaya Picasso.

---

## **5. Kesimpulan**

Proyek ini berhasil mengimplementasikan Neural Style Transfer menggunakan VGG19. Model ini mampu memisahkan dan merekonstruksi fitur konten dan gaya secara efektif. Meskipun prosesnya intensif secara komputasi, hasilnya menunjukkan potensi besar dari *deep learning* untuk aplikasi kreatif.

#### **Saran Pengembangan**
* Menggunakan metode *Fast Neural Style Transfer* untuk performa *real-time*.
* Mengeksplorasi kontrol spasial untuk menerapkan gaya pada area tertentu saja.
* Mengembangkan aplikasi untuk mentransfer gaya pada video.

---

## **6. Cara Menjalankan Kode**

1.  **Clone repositori ini:**
    ```bash
    git clone [https://github.com/username/neural-style-transfer-vgg19.git](https://github.com/username/neural-style-transfer-vgg19.git)
    cd neural-style-transfer-vgg19
    ```

2.  **Install semua library yang dibutuhkan:**
    ```bash
    pip install -r requirements.txt
    ```

3.  **Jalankan script Python:**
    ```bash
    python style_transfer.py --content path/to/content_image.jpg --style path/to/style_image.jpg
    ```
