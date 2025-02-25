---
marp: true
theme: gaia
_class: lead
paginate: true
backgroundColor: #fff
backgroundImage: url('background.png')

---

# Pengantar Teknik dan Algoritma Optimasi

📧 agungsetiabudi@ub.ac.id

---
### **Latar Belakang Mengapa Dibutuhkan Teknik Optimasi**  

Teknik optimasi diperlukan untuk menyelesaikan berbagai permasalahan kompleks di dunia nyata yang memiliki sumber daya terbatas dan banyak variabel yang harus dipertimbangkan. Berikut adalah beberapa alasan utama mengapa optimasi sangat dibutuhkan:

---

### **1. Keterbatasan Sumber Daya**  
Dalam banyak kasus, sumber daya seperti waktu, tenaga, bahan baku, dan dana terbatas, sehingga perlu dicari solusi terbaik yang **memaksimalkan manfaat** atau **meminimalkan biaya**.  
**Contoh:**  
- Perusahaan logistik perlu **menentukan rute pengiriman barang** yang paling hemat bahan bakar dan waktu.
- Rumah sakit harus **menjadwalkan tenaga medis** agar layanan tetap optimal dengan jumlah staf terbatas.

---

### **2. Kompleksitas Permasalahan**  
Banyak permasalahan dunia nyata memiliki **terlalu banyak kemungkinan solusi** sehingga tidak bisa diselesaikan dengan metode coba-coba (brute force). Optimasi membantu menemukan solusi yang paling baik dalam waktu yang wajar.  
**Contoh:**  
- Dalam **machine learning**, memilih **kombinasi hyperparameter terbaik** untuk meningkatkan akurasi model.
- Dalam **perancangan sirkuit elektronik**, menentukan **layout optimal** agar efisien dalam konsumsi daya.

---

### **3. Persaingan dan Efisiensi Industri**  
Dalam dunia bisnis dan manufaktur, perusahaan harus selalu mencari cara untuk meningkatkan efisiensi dan daya saing. Optimasi membantu dalam:  
- **Mengurangi waktu produksi dan biaya operasional.**  
- **Meningkatkan kualitas produk dan layanan.**  
**Contoh:**  
- Perusahaan e-commerce perlu mengoptimalkan **penempatan gudang** agar biaya pengiriman lebih murah.
---  
- Startup fintech menggunakan **algoritma optimasi portofolio investasi** untuk mendapatkan keuntungan maksimal dengan risiko minimal.

---

### **4. Pengambilan Keputusan yang Lebih Baik**  
Optimasi membantu dalam **pengambilan keputusan berbasis data** dengan mempertimbangkan berbagai variabel dan kendala.  
**Contoh:**  
- Pemerintah menggunakan optimasi untuk **menentukan distribusi bantuan sosial** agar lebih merata dan tepat sasaran.  
- Operator transportasi menggunakan **optimasi rute kendaraan umum** agar penumpang terlayani lebih baik dengan jumlah armada terbatas.

---

### **5. Perkembangan Teknologi dan AI**  
Dengan berkembangnya **Artificial Intelligence (AI) dan Internet of Things (IoT)**, optimasi semakin penting untuk:  
- **Memproses big data dengan lebih efisien.**  
- **Mengembangkan sistem otomatisasi yang lebih cerdas.**  
**Contoh:**  
    - **Optimasi jaringan sensor IoT** untuk meningkatkan efisiensi deteksi lokasi bus sekolah menggunakan BLE beacon.  
    - **Optimasi konsumsi daya pada perangkat Edge AI** agar perangkat lebih hemat energi dan tetap akurat dalam inferensi.

---

### **Teknik dan Algoritma Optimasi**
- Optimasi adalah proses mencari solusi terbaik dari sekumpulan solusi yang memungkinkan. 
- Tujuan utama optimasi adalah memaksimalkan atau meminimalkan suatu fungsi objektif sesuai dengan kendala yang ada.
---

### **Teknik Optimasi**
Teknik optimasi dapat dikategorikan menjadi beberapa jenis utama:

1. **Optimasi Klasik**  
   - **Optimasi Analitik**: Digunakan untuk mencari solusi optimal dengan diferensiasi, seperti **metode turunan pertama** dan **metode lagrange**.  
   - **Metode Numerik**: Digunakan jika solusi analitik sulit ditemukan, seperti **Metode Newton-Raphson** dan **Metode Gradien**.
---
2. **Optimasi Heuristik**  
   - Teknik yang mencoba menemukan solusi yang baik dalam waktu yang wajar tanpa menjamin solusi optimal.  
   - Contoh: **Simulated Annealing, Tabu Search**.

3. **Optimasi Metaheuristik**  
   - Algoritma berbasis pencarian global yang sering digunakan dalam optimasi kompleks.  
   - Contoh: **Genetic Algorithm (GA), Particle Swarm Optimization (PSO), Ant Colony Optimization (ACO)**.
---
4. **Optimasi Berbasis Pembelajaran Mesin**  
   - Menggunakan teknik pembelajaran mesin untuk menemukan solusi terbaik.  
   - Contoh: **Bayesian Optimization, Deep Reinforcement Learning**.

---

### Bahan Kajian
1. Optimasi Linear, Non-Linear, dan Dynamic Programming
2. Optimasi Diskrit (Graf & Network Theory)
3. Metode Heuristic (Local Search)
4. Metode Metaheuristic (Algoritma Evolusioner.Swarm, Ant & Bee Colony)
5. Optimasi Multi-Objektif (Konsep Pareto)
6. Teknologi & Alat Pendukung Optimasi
---

#### **Refresh**
1. Berapakah nilai optimum dari fungsi berikut:  $y = x^2 + 4x +2$
2. Sebuah pabrik menghasilkan dua jenis produk A dan B dengan keuntungan masing-masing Rp700 dan Rp500 per unit. Bahan baku yang tersedia adalah 100 kg, dan waktu produksi yang tersedia adalah 240 jam. Produk A membutuhkan 2 kg bahan baku dan 4 jam, sedangkan produk B membutuhkan 1 kg bahan baku dan 3 jam. Berapakan jumlah produk A dan B yang harus diproduksi agar keuntungan maksimum?
---
3. Misalkan suatu perusahaan memiliki **fungsi biaya produksi** yang bergantung pada dua variabel, yaitu jumlah unit **Produk A ($x$)** dan **Produk B ($y$)**.  

    Fungsi biaya produksi yang harus diminimalkan adalah:  
$C(x, y) = 3x^2 + 4y^2 + 2xy - 6x - 8y + 10$  
Tentukan jumlah **Produk A ($x$)** dan **Produk B ($y$)** yang meminimalkan biaya produksi.