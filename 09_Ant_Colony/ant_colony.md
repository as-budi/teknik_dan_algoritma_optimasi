---
marp: true
theme: gaia
_class: lead
paginate: true
backgroundColor: #fff
backgroundImage: url('../bg.png')

---

# 🐜 Ant Colony Optimization (ACO)

📧 agungsetiabudi@ub.ac.id

---

### 1. **Pendahuluan**

- Ant Colony Optimization (ACO) adalah *metaheuristic optimization algorithm* yang diinspirasi oleh perilaku sosial semut dalam mencari jalur terpendek menuju sumber makanan.
- Diperkenalkan oleh **Marco Dorigo** pada awal 1990-an, ACO terutama efektif dalam menyelesaikan masalah optimasi kombinatorial seperti *Traveling Salesman Problem (TSP)*, *vehicle routing*, *scheduling*, dan lain-lain.

---

### 2. **Inspirasi Biologis: Perilaku Semut**

- Semut asli menggunakan **feromon** untuk menandai jalur menuju makanan.
- Semakin banyak semut melewati suatu jalur, semakin kuat jejak feromon yang terbentuk, sehingga jalur tersebut lebih mungkin dipilih semut lain.
- Mekanisme ini menciptakan umpan balik positif dan memungkinkan koloni menemukan rute optimal tanpa supervisi terpusat.

---

### 3. **Prinsip Dasar ACO**

* **Artificial Ants** adalah agen sederhana yang menjelajahi ruang solusi.
* Mereka membangun solusi parsial secara probabilistik berdasarkan dua informasi:

  * **Jejak feromon**: $\tau_{ij}$, representasi historis preferensi terhadap tepi antara node $i$ dan $j$.
  * **Heuristic information**: $\eta_{ij}$, representasi pengetahuan lokal, seperti $1/d_{ij}$ untuk jarak.
---
* Setelah membangun solusi, semut memperkuat jalur yang baik dengan **menambah feromon**, dan seiring waktu feromon juga **menguap** (evaporasi).

---

### 4. **Langkah-langkah Algoritma ACO Umum**

1. **Inisialisasi:**

   * Set nilai awal feromon $\tau_{ij} = \tau_0$.
   * Tentukan parameter: jumlah semut, koefisien evaporasi $\rho$, eksponen feromon $\alpha$, dan eksponen heuristik $\beta$.

2. **Konstruksi Solusi:**
   Setiap semut membangun solusi dengan probabilitas memilih elemen (misalnya kota $j$ dari $i$):

   $$
   P_{ij} = \frac{\tau_{ij}^\alpha \cdot \eta_{ij}^\beta}{\sum_{k \in N_i} \tau_{ik}^\alpha \cdot \eta_{ik}^\beta}
   $$

   di mana $N_i$ adalah kandidat langkah berikutnya dari $i$.
---
3. **Evaluasi dan Pembaruan Feromon:**

   * Feromon di setiap jalur diperbarui berdasarkan kualitas solusi:

     $$
     \tau_{ij} \leftarrow (1 - \rho)\cdot\tau_{ij} + \sum_{k=1}^m \Delta\tau_{ij}^k
     $$

     dengan $\Delta\tau_{ij}^k = \frac{Q}{L_k}$ jika semut $k$ menggunakan tepi $(i, j)$, di mana $L_k$ adalah panjang solusi dan $Q$ adalah konstanta.

4. **Pengulangan:**

   * Ulangi proses hingga kriteria penghentian terpenuhi (jumlah iterasi, waktu, atau konvergensi solusi).

---

### 5. **Parameter Penting**

| Parameter    | Deskripsi                                                                  |
| ------------ | -------------------------------------------------------------------------- |
| $\alpha$     | Pengaruh feromon dalam pemilihan jalur                                     |
| $\beta$      | Pengaruh heuristik (bias lokal)                                            |
| $\rho$       | Laju evaporasi feromon                                                     |
| $Q$          | Konstanta penguat feromon                                                  |
| Jumlah semut | Biasanya disamakan dengan jumlah elemen dalam solusi (misal kota pada TSP) |

---

### 6. **Contoh Aplikasi: Traveling Salesman Problem (TSP)**

* Tujuan: Menemukan urutan kunjungan ke kota yang meminimalkan total jarak.
* Setiap semut membangun tur kota.
* Jejak feromon disimpan pada setiap pasangan kota.
* Setelah seluruh semut menyelesaikan tur, feromon diperbarui sesuai total jarak tempuh.
* Semut lebih cenderung memilih jalur pendek yang sering digunakan oleh semut lain.

---

### 7. **Kelebihan dan Kekurangan**

#### ✅ Kelebihan:

* Adaptif, paralel, dan berbasis populasi.
* Cocok untuk masalah diskrit dan kombinatorial.
* Mudah digabungkan dengan teknik lain (misalnya local search, greedy).
---
#### ❌ Kekurangan:

* Rentan terhadap konvergensi dini (premature convergence).
* Butuh tuning parameter yang hati-hati.
* Waktu komputasi bisa tinggi untuk masalah besar.

---

### 8. **Variasi ACO**

Beberapa varian populer:

* **Ant System (AS)** – versi dasar dari ACO.
* **Ant Colony System (ACS)** – penguatan hanya dari semut terbaik, eksploitasi lebih besar.
* **Max-Min Ant System (MMAS)** – batasan nilai feromon untuk mencegah konvergensi dini.

---
### 🔄 **ACO Dapat Digunakan untuk Masalah Kontinyu, tetapi...**

Secara **asli dan umum**, **Ant Colony Optimization (ACO)** dirancang untuk **masalah optimasi kombinatorial**, seperti:

* Traveling Salesman Problem (TSP)
* Vehicle Routing Problem (VRP)
* Job Scheduling
* Quadratic Assignment Problem (QAP)
---
- Namun, **ACO telah diperluas dan dimodifikasi** agar bisa digunakan untuk **masalah optimasi kontinyu**, terutama sejak pertengahan 2000-an. Versi ini sering disebut:

- **Continuous Domain Ant Colony Optimization (CACO atau ACOR – Ant Colony Optimization for Continuous Domains)**

---

### 🔍 **Perbedaan Pendekatan pada Masalah Kontinyu**

Karena tidak ada "jalan" atau "urutan diskrit" dalam domain kontinyu, pendekatan ACO klasik perlu dimodifikasi:

1. **Solusi direpresentasikan sebagai vektor real**

Contoh solusi:

$$
\mathbf{x} = [x_1, x_2, ..., x_n] \in \mathbb{R}^n
$$

---
2. **Distribusi probabilistik digunakan sebagai pengganti feromon diskrit**

* Misalnya menggunakan **Gaussian Kernel** untuk menghasilkan solusi baru:

  $$
  x_i^{(new)} \sim \sum_{k=1}^{m} w_k \cdot \mathcal{N}(x_i^{(k)}, \sigma_k^2)
  $$

  Artinya, solusi baru dibangkitkan dari distribusi normal berbobot dari solusi lama.
---
3. **Pembaruan feromon = pembaruan distribusi probabilistik**

* Distribusi diarahkan agar memusat ke solusi terbaik sejauh ini.
* Mirip dengan strategi dalam **Estimation of Distribution Algorithms (EDA)**.

---

Berikut adalah **contoh lengkap penggunaan Ant Colony Optimization (ACO) untuk menyelesaikan masalah Traveling Salesman Problem (TSP)** menggunakan **matriks jarak simetris**, lengkap dengan:

* Konstruksi solusi oleh semut
* Perhitungan probabilitas
* Evaporasi dan update feromon
* Tabel feromon sebelum dan sesudah iterasi

---

#### 📌 **Studi Kasus: TSP 4 Kota**

- Diberikan 4 kota: A, B, C, D
- Matriks jarak antar kota (simetris):

  |   | A  | B | C | D  |
  | - | -- | - | - | -- |
  | A | 0  | 2 | 9 | 10 |
  | B | 2  | 0 | 6 | 4  |
  | C | 9  | 6 | 0 | 8  |
  | D | 10 | 4 | 8 | 0  |

---

#### ⚙️ **Parameter ACO**

* Jumlah semut = 2
* $\alpha = 1$, $\beta = 2$
* $\rho = 0.5$ (evaporasi 50%)
* $Q = 100$
* Feromon awal: $\tau_{ij} = 1$ untuk semua $i \neq j$
* Heuristik $\eta_{ij} = 1/d_{ij}$

---

#### 📋 **Langkah 1: Matriks Heuristik $\eta_{ij}$**

|   | A     | B     | C     | D     |
| - | ----- | ----- | ----- | ----- |
| A | -     | 0.5   | 0.111 | 0.1   |
| B | 0.5   | -     | 0.167 | 0.25  |
| C | 0.111 | 0.167 | -     | 0.125 |
| D | 0.1   | 0.25  | 0.125 | -     |

---

#### 📋 **Langkah 2: Feromon Awal $\tau_{ij}$**

Semua $\tau_{ij} = 1$, untuk $i \neq j$

---

#### 🧭 **Langkah 3: Semut 1 Mulai dari Kota A**

##### **Langkah 3.1: Pilihan kota dari A: B, C, D**

- Bobot kombinasi (ingat: $\tau_{ij}^\alpha \cdot \eta_{ij}^\beta$):

  | Kota      | $\tau$ | $\eta$ | $\eta^2$ | $\tau \cdot \eta^2$ |
  | --------- | ------ | ------ | -------- | ------------------- |
  | B         | 1      | 0.5    | 0.25     | 0.25                |
  | C         | 1      | 0.111  | 0.0123   | 0.0123              |
  | D         | 1      | 0.1    | 0.01     | 0.01                |
  | **Total** |        |        |          | **0.2723**          |

---
$$
P_{ij} = \frac{\tau_{ij}^\alpha \cdot \eta_{ij}^\beta}{\sum_k \tau_{ik}^\alpha \cdot \eta_{ik}^\beta}
$$

$$
P_{A \rightarrow B} = \frac{1 \cdot (0.5)^2}{(0.5)^2 + (0.111)^2 + (0.1)^2} = \frac{0.25}{0.25 + 0.0123 + 0.01} \approx 0.918
$$
- Dengan cara yang sama diperoleh probabilitas semua kota:
  * $P_{A \rightarrow B} = 0.25 / 0.2723 \approx \textbf{0.918}$
  * $P_{A \rightarrow C} = 0.0123 / 0.2723 \approx \textbf{0.045}$
  * $P_{A \rightarrow D} = 0.01 / 0.2723 \approx \textbf{0.037}$

Jadi kemungkinan besar semut memilih **A → B**

---
##### **Langkah 3.2: dari B ke (C, D)**

- Bobot:

  | Kota      | $\eta^2$ | $\tau \cdot \eta^2$ |
  | --------- | -------- | ------------------- |
  | C         | 0.0279   | 0.0279              |
  | D         | 0.0625   | 0.0625              |
  | **Total** |          | **0.0904**          |

- Probabilitas:
  * $P_{B \rightarrow C} = 0.0279 / 0.0904 \approx \textbf{0.309}$
  * $P_{B \rightarrow D} = 0.0625 / 0.0904 \approx \textbf{0.691}$ (**Pilih D**)

---

##### **Langkah 3.3: dari D ke (C)**
- Sisa kota: C
- ➡️ Probabilitas 100% ke C
- Dari C kembali ke asal (A)
- Misal urutan penuh: **A → B → D → C → A**
- Total jarak:
  * (A–B = 2), (B–D = 4), (D–C = 8), (C–A = 9)
  * **Total = 23**

---
#### **Rekap semut 1**
| Langkah | Pilihan Kota                     | Probabilitas |
| ------- | -------------------------------- | ------------ |
| A → ?   | B: **0.918**, C: 0.045, D: 0.037 | → **B**      |
| B → ?   | D: **0.691**, C: 0.309           | → **D**      |
| D → ?   | C: 1.0                           | → **C**      |
| C → A   | kembali ke asal                  |              |

---
#### **Langkah 4: Semut 2 (Mulai dari Kota C)**

##### **Langkah 4.1: dari C ke (A, B, D)**

- Heuristik:
  * $\eta_{CA} = 1/9 \approx 0.111$
  * $\eta_{CB} = 1/6 \approx 0.167$
  * $\eta_{CD} = 1/8 = 0.125$

---
- Bobot (ingat: semua $\tau_{ij} = 1$):

  | Kota      | $\eta^2$ | $\tau \cdot \eta^2$ |
  | --------- | -------- | ------------------- |
  | A         | 0.0123   | 0.0123              |
  | B         | 0.0279   | 0.0279              |
  | D         | 0.0156   | 0.0156              |
  | **Total** |          | **0.0558**          |
---
- Probabilitas:
  * $P_{C \rightarrow B} = 0.0279 / 0.0558 ≈ \textbf{0.5}$
  * $P_{C \rightarrow D} = 0.0156 / 0.0558 ≈ \textbf{0.28}$
  * $P_{C \rightarrow A} = 0.0123 / 0.0558 ≈ \textbf{0.22}$
  - 🧭 **Pilih B**

---

##### **Langkah 4.2: dari B ke (A, D)**

- Heuristik:
  * $\eta_{BA} = 1/2 = 0.5$
  * $\eta_{BD} = 1/4 = 0.25$

- Bobot:
  | Kota      | $\eta^2$ | $\tau \cdot \eta^2$ |
  | --------- | -------- | ------------------- |
  | A         | 0.25     | 0.25                |
  | D         | 0.0625   | 0.0625              |
  | **Total** |          | **0.3125**          |
---

- Probabilitas:
  * A: 0.25 / 0.3125 = **0.8**
  * D: 0.0625 / 0.3125 = **0.2**
  - 🧭 **Pilih A**

---

##### **Langkah 4.3: dari A ke D**

- Sisa: hanya D
- ➡️ Probabilitas = 1
- kembali ke asal C
- Rute Semut 2: C → B → A → D → C
- Jarak:
  * (C–B = 6), (B–A = 2), (A–D = 10), (D–C = 8)
  * **Total = 26**

---

#### 📊 **Update Feromon Setelah Iterasi 1**

- ⚙️ Parameter
  - $Q = 100$
  - $\rho = 0.5$
- 🧪 Evaporasi (semua feromon awal 1 → jadi 0.5)

---

#### 📥 Tambahan Feromon:
- **Semut 1:** (A–B–D–C–A), L = 23

$$
\Delta \tau = \frac{100}{23} ≈ 4.35
$$
- Edges:
  - A–B, B–D, D–C, C–A
---
- **Semut 2:** (C–B–A–D–C), L = 26

$$
\Delta \tau = \frac{100}{26} ≈ 3.85
$$

- Edges:
  - C–B, B–A, A–D, D–C

---

#### 📘 **Tabel Feromon Setelah Iterasi 1**

| Edge | Evaporated | Semut 1 | Semut 2 | Total $\tau_{ij}$ |
| ---- | ---------- | ------- | ------- | ----------------- |
| A–B  | 0.5        | 4.35    | 3.85    | **8.7**           |
| B–D  | 0.5        | 4.35    | –       | **4.85**          |
| D–C  | 0.5        | 4.35    | 3.85    | **8.7**           |
| C–A  | 0.5        | 4.35    | –       | **4.85**          |
| C–B  | 0.5        | –       | 3.85    | **4.35**          |
| A–D  | 0.5        | –       | 3.85    | **4.35**          |

---

#### 📋 **Matriks Feromon Simetris $\tau_{ij}$ Setelah Iterasi 1**

|   | A    | B    | C    | D    |
| - | ---- | ---- | ---- | ---- |
| A | –    | 8.7  | 4.85 | 4.35 |
| B | 8.7  | –    | 4.35 | 4.85 |
| C | 4.85 | 4.35 | –    | 8.7  |
| D | 4.35 | 4.85 | 8.7  | –    |

- Setelah mendapatkan matriks feromon yang baru maka langkah-langkah diulang kembali dengan matriks feromon yang baru.
---

#### ✅ **Ringkasan**

* Semut 1 memberi penguatan besar pada jalur pendek A–B–D–C–A (L = 23)
* Semut 2 memberi penguatan pada C–B–A–D–C (L = 26)
* Feromon terbesar kini di A–B dan D–C (masing-masing 8.7)
* Jalur pendek makin disukai di iterasi selanjutnya





