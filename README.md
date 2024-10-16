# Simulasi Pembelajaran Penguatan pada Agen Basket Menggunakan Q-Learning dan TD(λ)

Repositori ini berisi kode Python yang mengimplementasikan simulasi permainan basket sederhana di mana agen AI belajar memainkan permainan menggunakan dua metode pembelajaran penguatan:
1. **Q-Learning**
2. **TD(λ)** (Temporal Difference dengan Traces Eligibilitas)

Simulasi ini bertujuan untuk melatih agen agar memaksimalkan skornya dalam lingkungan grid dengan menghindari lawan dan menembak bola ke keranjang.

## Daftar Isi
- [Instalasi](#instalasi)
- [Deskripsi Lingkungan](#deskripsi-lingkungan)
- [Algoritma Pembelajaran](#algoritma-pembelajaran)
  - [Q-Learning](#q-learning)
  - [TD(λ)](#tdλ)
- [Pencatatan Data](#pencatatan-data)
- [Visualisasi](#visualisasi)
- [Cara Menjalankan Simulasi](#cara-menjalankan-simulasi)
- [Pengembangan di Masa Depan](#pengembangan-di-masa-depan)
- [Grafik Kinerja](#grafik-kinerja)

## Instalasi

Untuk menjalankan proyek ini, Anda perlu menginstal beberapa dependensi Python. Pastikan Python versi 3.x telah terinstal di sistem Anda. Berikut adalah dependensi yang diperlukan:
- **NumPy:** Untuk operasi matriks dan vektor.
- **Pygame:** Untuk visualisasi lingkungan simulasi.
- **Matplotlib:** Untuk plotting hasil belajar agen.
- **TensorFlow (opsional):** Untuk pencatatan data menggunakan TensorBoard.

Instal semua dependensi dengan perintah berikut:

```bash
pip install numpy pygame matplotlib tensorflow
