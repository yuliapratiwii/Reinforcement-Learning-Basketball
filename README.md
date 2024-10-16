
# Basketball AI Simulation with Q-Learning and TD(λ)
## UTS Kelompok 4
- Ioshi Junika Fandha (G1A021026)
- Yulia Pratiwi (G1A021029)
- Mareta Aliana (G1A021038)

Repositori ini berisi kode Python yang mengimplementasikan simulasi permainan basket sederhana di mana agen AI belajar memainkan permainan menggunakan dua metode pembelajaran penguatan:
1. **Q-Learning**
2. **TD(λ)** (Temporal Difference dengan Traces Eligibilitas)

Simulasi ini bertujuan untuk melatih agen agar memaksimalkan skornya dalam lingkungan grid dengan menghindari lawan dan menembak bola ke keranjang.

## Daftar Isi
- [Instalasi](#instalasi)
- [Environment](#environment)
- [Algoritma Pembelajaran](#algoritma-pembelajaran)
  - [Q-Learning](#1-q-learning)
  - [TD(λ)](#2-tdλ)
- [Logging](#logging)
- [Visualisasi](#visualisasi)
- [How To Run](#how-to-run)
- [Grafik](#grafik)

## Instalasi

Untuk menjalankan proyek ini, Anda perlu menginstal beberapa dependensi Python. Pastikan Python versi 3.x telah terinstal di sistem Anda. Berikut adalah dependensi yang diperlukan:
- **Python 3.x:** 
- **NumPy:** 
- **Pygame:** 
- **Matplotlib:** 
- **TensorFlow (opsional):**
  
Instal semua dependensi dengan perintah berikut:

```
pip install numpy pygame matplotlib tensorflow
```
## Environment
Lingkungan basket diimplementasikan dalam kelas BasketballEnv. Lingkungan ini adalah grid world di mana:

◆ Agen (robot) dapat bergerak dalam empat arah (atas, bawah, kiri, kanan).<br>

◆ Agen dapat menggiring bola ketika berada dekat dengan bola dan mencoba menembak ketika berada dekat dengan keranjang.<br>

◆ Terdapat lawan yang ditempatkan secara acak di grid yang menghalangi pergerakan agen.<br>

◆ Tujuan agen adalah menggiring bola ke arah keranjang dan menembak, dengan tujuan untuk memaksimalkan skor.<br>

## Algoritma Pembelajaran 
### 1. Q-Learning
Q-Learning adalah algoritma pembelajaran penguatan tanpa model (model-free) yang belajar dari interaksi agen dengan lingkungan. Tujuan dari Q-Learning adalah untuk membangun Q-Table, yang berisi nilai (Q-value) yang mengindikasikan seberapa baik sebuah aksi di suatu state. Nilai ini diperbarui setiap kali agen melakukan aksi, menggunakan persamaan Bellman.

#### Parameter Utama Q-Learning:
🔧 α (Alpha): Learning rate, menentukan seberapa cepat agen belajar.<br>

🔧 γ (Gamma): Discount factor, mengukur seberapa jauh agen memperhitungkan reward masa depan.<br>

🔧 ε (Epsilon): Eksplorasi vs Eksploitasi, mengendalikan apakah agen mencoba aksi baru atau mengambil aksi terbaik yang diketahui.<br>

Eksplorasi vs Eksploitasi: Agen menggunakan strategi epsilon-greedy untuk memutuskan apakah akan mencoba tindakan baru (eksplorasi) atau mengambil tindakan terbaik yang diketahui (eksploitasi).

Proses Q-Learning:
1. Pada awalnya, Q-Table diinisialisasi dengan nilai acak atau nol.
2. Agen mengambil tindakan berdasarkan Q-Table (dengan beberapa derajat eksplorasi).
3. Q-value diperbarui berdasarkan reward yang diterima dan state selanjutnya.
4. Seiring waktu, agen memperbaiki Q-Table-nya, yang digunakan untuk memaksimalkan reward dalam jangka panjang.
### 2. TD(λ)
TD(λ) adalah pengembangan dari metode Temporal Difference (TD) yang menggunakan eligibility traces untuk melacak pengaruh dari status-aksi yang telah dikunjungi. Hal ini mempercepat pembelajaran dengan memanfaatkan informasi dari beberapa langkah sebelumnya (multi-step).

#### Proses TD(λ):
1. Algoritma ini menggabungkan pendekatan TD dan Monte Carlo dengan memperbarui Q-values berdasarkan trace (jejak) dari status dan aksi yang sering dikunjungi.
2. Setiap state-action pair memiliki eligibility trace yang bertindak seperti "memori", dan trace ini diperbarui setiap kali state tersebut dikunjungi.
#### Parameter TD(λ):
λ (Lambda): Mengendalikan kecepatan decay dari eligibility traces. Nilai λ = 1 berarti semua jejak dipertimbangkan (serupa dengan Monte Carlo), sedangkan λ = 0 hanya memperbarui satu langkah terakhir (seperti TD Learning murni).<br>


Contoh penerapan dalam kode:
```
td = TDLambda(alpha=0.1, gamma=0.9, lambd=0.9, epsilon=0.95, epsilon_decay=0.99, epsilon_min=0.01)
td.learn(10000, 50)
```
## Logging
Jika mengaktifkan logging, hasil pembelajaran agen dicatat menggunakan TensorFlow. Ini termasuk:
* Reward per Episode: Reward yang diterima agen di setiap episode.
* Rata-rata Reward: Rata-rata reward di setiap episode.<br.
  
Data ini dapat divisualisasikan menggunakan TensorBoard atau dengan plotting menggunakan Matplotlib.
## Visualisasi
Rendering dilakukan menggunakan library Pygame. Ketika render=True diberikan ke instance Q-Learning atau TD(λ), lingkungan akan menampilkan representasi grafis dari agen, bola, dan lawan secara real-time.

## How to Run
Untuk menjalankan simulasi, eksekusi fungsi main() di skrip. Fungsi ini menjalankan algoritma Q-Learning untuk 9100 episode dengan 50 langkah per episode.
```
python robot-basket.py
```
#### Argumen Utama:
🧠 alpha: Learning rate.
🧠 gamma: Discount factor.
🧠 epsilon: Tingkat eksplorasi.
🧠 epsilon_decay: Tingkat penurunan epsilon setelah setiap episode.
🧠 epsilon_min: Nilai minimum epsilon.
🧠 render: Aktifkan/Nonaktifkan rendering grafis.
🧠 logging: Aktifkan/Nonaktifkan pencatatan untuk TensorBoard.

## Grafik
Di bawah ini adalah grafik yang menunjukkan perkembangan reward rata-rata per episode selama proses pembelajaran.
![Grafik Analisis](https://github.com/yuliapratiwii/Reinforcement-Learning-Basketball/blob/master/Image/Grafik.png)

Grafik ini menunjukkan peningkatan reward rata-rata seiring berjalannya episode, yang mengindikasikan bahwa agen belajar meningkatkan performa dalam mencetak skor.
