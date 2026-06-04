# Proyek Akhir UAS Kalkulus Integral Berbasis Pemrograman
### Topik: Pemodelan Laju Produksi Multi-Fase (Misi 3)

**Kelompok MBG — Universitas Negeri Yogyakarta**

| Nama | NIM | Peran |
|------|-----|-------|
| Irham Kadarusman | 25051130056 | Koordinator Proyek |
| Klarizto Armanero Wibowo | 25051130068 | Modeling Lead |
| Hanu Hermawan | 25051130083 | Symbolic Lead |
| Labib Nur Hidayat | 25051130044 | Numeric Lead |
| Roihan Anwar | 25051130047 | Validation Lead |
| Rafif Athallah Pratama | 25051130051 | Visualization & Reporting Lead |

---

## Deskripsi Proyek

Proyek ini memodelkan laju produksi $P(t)$ sebuah pabrik selama 1 shift kerja (8 jam) menggunakan fungsi *piecewise* (multi-fase), lalu menghitung akumulasi total produksi $Q$ (dalam satuan unit) secara **analitik** (SymPy) maupun **numerik** (NumPy), dilengkapi validasi error dan visualisasi.

---

## Model Matematis

Fungsi laju produksi dibagi menjadi 3 fase:

| Fase | Rentang Waktu | Fungsi $P(t)$ | Keterangan |
|------|--------------|---------------|------------|
| 1 — Ramping Up | $0 \le t \le 2$ | $P_1(t) = 50t$ | Akselerasi linear |
| 2 — Optimal | $2 < t \le 6$ | $P_2(t) = 100$ | Kapasitas penuh konstan |
| 3 — Cooling Down | $6 < t \le 8$ | $P_3(t) = 100 - 50(t-6)$ | Deselerasi linear |

Total produksi dihitung dengan:

$$Q = \int_{0}^{8} P(t)\,dt = \int_{0}^{2} 50t\,dt + \int_{2}^{6} 100\,dt + \int_{6}^{8}(100 - 50(t-6))\,dt$$

---

## Dependensi

Pastikan Python sudah terinstall, lalu install library berikut:

```bash
pip install sympy numpy matplotlib jupyter
```

| Library | Versi Minimum | Kegunaan |
|---------|--------------|---------|
| `sympy` | ≥ 1.12 | Solusi simbolik / analitik (Bagian C) |
| `numpy` | ≥ 1.24 | Solusi numerik & metode trapesium (Bagian D) |
| `matplotlib` | ≥ 3.7 | Visualisasi kurva dan area per fase (Bagian F) |
| `jupyter` | ≥ 1.0 | Menjalankan file `.ipynb` |

---

## Cara Penggunaan

**1. Clone atau download repositori ini**

```bash
git clone <url-repo>
cd <nama-folder>
```

**2. Install dependensi**

```bash
pip install sympy numpy matplotlib jupyter
```

**3. Jalankan Jupyter Notebook**

```bash
jupyter notebook UAS_KalkulusIntegral_Kelompok2.ipynb
```

**4. Jalankan seluruh sel secara berurutan**

Di menu Jupyter, pilih **Kernel → Restart & Run All** untuk menjalankan semua bagian sekaligus, atau jalankan tiap sel satu per satu dari atas ke bawah (Shift+Enter).

> Tidak ada input manual yang diperlukan. Seluruh parameter sudah terdefinisi di dalam notebook.

---

## Struktur Notebook

| Bagian | Penanggung Jawab | Isi |
|--------|-----------------|-----|
| A | Klarizto | Deskripsi masalah dan satuan variabel |
| B | Klarizto | Model matematis fungsi *piecewise* |
| C | Hanu | Solusi simbolik / analitik dengan SymPy |
| D | Labib | Solusi numerik dengan NumPy (metode trapesium, $n=1.000$ dan $n=100.000$) |
| E | Roihan | Validasi: *absolute error* dan *relative error* |
| F | Rafif | Visualisasi kurva $P(t)$ dan area per fase (Matplotlib) |
| G | Rafif | Interpretasi hasil dan kesimpulan |
| H | Rafif | Pernyataan kontribusi anggota |

---

## Ringkasan Hasil

### Total Produksi

| Metode | Hasil |
|--------|-------|
| Analitik (SymPy) | **600 unit** |
| Numerik $n=1.000$ (NumPy trapesium) | **600.000000 unit** |
| Numerik $n=100.000$ (NumPy trapesium) | **600.000000 unit** |

### Kontribusi Per Fase

| Fase | Rentang | Produksi |
|------|---------|----------|
| Fase 1 — Ramping Up | Jam 0–2 | 100 unit |
| Fase 2 — Optimal | Jam 2–6 | 400 unit |
| Fase 3 — Cooling Down | Jam 6–8 | 100 unit |
| **Total** | **0–8 jam** | **600 unit** |

### Analisis Error

| Resolusi | Absolute Error | Relative Error |
|----------|---------------|---------------|
| $n = 1.000$ | ~0.00000000 | ~0.00000000% |
| $n = 100.000$ | ~0.00000000 | ~0.00000000% |

Error bernilai nol karena fungsi *piecewise* seluruhnya terdiri dari segmen **linear**. Metode trapesium bekerja sempurna pada fungsi linear — luas trapesium numerik berimpit tepat dengan luas analitik. Selain itu, titik patahan fungsi ($t=2$ dan $t=6$) jatuh tepat pada titik simpul *grid sampling* di kedua resolusi, sehingga tidak ada galat diskretisasi.

---

## Lisensi

Proyek ini dibuat untuk keperluan akademik UAS Kalkulus Integral — Universitas Negeri Yogyakarta. Tidak untuk didistribusikan tanpa izin.