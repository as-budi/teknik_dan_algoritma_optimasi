---
marp: true
theme: gaia
_class: lead
paginate: true
backgroundColor: #fff
backgroundImage: url('../bg.png')

---

# _PARTICLE SWARM OPTIMIZATION_ (PSO)

📧 agungsetiabudi@ub.ac.id

---

#### _Particle Swarm Optimization_ (PSO)
- **Particle Swarm Optimization (PSO)** adalah algoritma optimasi yang terinspirasi oleh perilaku sosial dari burung yang mencari makanan. 
- PSO digunakan untuk menyelesaikan masalah optimasi dengan cara mengelola sekelompok solusi kandidat yang disebut "partikel".
- Setiap partikel memiliki posisi dan kecepatan di ruang pencarian, dan mereka berinteraksi satu sama lain untuk menemukan solusi optimal.

---
#### Konsep Dasar PSO

1. **Inisialisasi**: Setiap partikel diinisialisasi dengan posisi dan kecepatan acak di ruang pencarian. 
2. **Evaluasi**: Nilai fitness dari setiap partikel dihitung menggunakan fungsi tujuan yang ingin dioptimalkan.

---
#### Konsep Dasar PSO
3. **Update Posisi dan Kecepatan**:
   - Setiap partikel memiliki dua nilai penting: posisi terbaik yang pernah dicapai (pBest) dan posisi terbaik global yang dicapai oleh seluruh partikel (gBest).
   - Kecepatan dan posisi partikel diperbarui dengan rumus:
     $
     v_{i} = w \cdot v_{i} + c_1 \cdot r_1 \cdot (pBest_{i} - x_{i}) + c_2 \cdot r_2 \cdot (gBest - x_{i})
     $
     $
     x_{i} = x_{i} + v_{i}
     $

---
#### Konsep Dasar PSO
   Di mana:
   - $v_{i}$: kecepatan partikel $i$
   - $x_{i}$: posisi partikel $i$
   - $w$: koefisien inersia
   - $c_1, c_2$: koefisien akselerasi
   - $r_1, r_2$: bilangan acak antara 0 dan 1
   - $pBest_{i}$: posisi terbaik partikel $i$
   - $gBest$: posisi terbaik global

---
#### Konsep Dasar PSO
4. **Iterasi**: Langkah evaluasi dan pembaruan diulang sampai kriteria berhenti tercapai (misalnya, jumlah iterasi maksimum atau konvergensi).

---
#### Contoh Penerapan PSO

Misalkan kita ingin meminimalkan fungsi berikut:
$
f(x) = x^2 - 4x + 4
$
Ini adalah fungsi kuadrat dengan titik minimum di $x = 2$.

---
#### 1. Inisialisasi
   - Jumlah partikel: 3
   - Posisi awal (random): $x_1 = 0, x_2 = 4, x_3 = 5$
   - Kecepatan awal (random): $v_1 = 0.5, v_2 = -0.5, v_3 = 0.3$
   - $pBest$: posisi awal sama dengan posisi awal
   - $gBest$: posisi terbaik di antara semua partikel

---
#### 2. Evaluasi:
   - Hitung nilai fungsi untuk setiap partikel:
     - $f(x_1) = f(0) = 4$
     - $f(x_2) = f(4) = 0$
     - $f(x_3) = f(5) = 1$

   - Jadi, $pBest_1 = 0, pBest_2 = 4, pBest_3 = 5$ dan $gBest = 4$.

---
#### 3. Update Kecepatan dan Posisi
- Misalkan kita menggunakan $w = 0.5$, $c_1 = 1.5$, $c_2 = 1.5$, dan $r_1, r_2$ diambil acak sebagai 0.2 dan 0.6.
   - Untuk partikel 1:
     $
     v_1 = 0.5 \cdot 0.5 + 1.5 \cdot 0.2 \cdot (0 - 0) + 1.5 \cdot 0.6 \cdot (4 - 0) = 3.85
     $
     $
     x_1 = 0 + 3.85 = 3.85
     $

   - Untuk partikel 2:
     $
     v_2 = 0.5 \cdot (-0.5) + 1.5 \cdot 0.2 \cdot (4 - 4) + 1.5 \cdot 0.6 \cdot (4 - 4) = -0.25
     $
     $
     x_2 = 4 - 0.25 = 3.75
     $
---
#### 3. Update Kecepatan dan Posisi
   - Untuk partikel 3:
     $
     v_3 = 0.5 \cdot 0.3 + 1.5 \cdot 0.2 \cdot (5 - 5) + 1.5 \cdot 0.6 \cdot (4 - 5) = -0.75
     $
     $
     x_3 = 5 - 0.75 = 4.25
     $

---
#### 4. Evaluasi ulang
   - Hitung nilai fungsi lagi:
     - $f(x_1) = f(3.85) = 0.0225$
     - $f(x_2) = f(3.75) = 0.0625$
     - $f(x_3) = f(4.25) = 0.0625$

   - Update $pBest$ dan $gBest$:
     - $pBest_1 = 3.85, pBest_2 = 4, pBest_3 = 4.25$
     - $gBest$ tetap $4$.

---
#### 5. Iterasi
Proses diulang hingga konvergen.
