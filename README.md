# NUMERA — Numerical Methods Application

<div align="center">

```
███╗   ██╗██╗   ██╗███╗   ███╗███████╗██████╗  █████╗
████╗  ██║██║   ██║████╗ ████║██╔════╝██╔══██╗██╔══██╗
██╔██╗ ██║██║   ██║██╔████╔██║█████╗  ██████╔╝███████║
██║╚██╗██║██║   ██║██║╚██╔╝██║██╔══╝  ██╔══██╗██╔══██║
██║ ╚████║╚██████╔╝██║ ╚═╝ ██║███████╗██║  ██║██║  ██║
╚═╝  ╚═══╝ ╚═════╝ ╚═╝     ╚═╝╚══════╝╚═╝  ╚═╝╚═╝  ╚═╝
```

**Numerical Methods Application**

*Aplikasi pembelajaran metode numerik yang interaktif berbasis Python + Streamlit*

</div>

---

## 1. Deskripsi

**NUMERA** adalah aplikasi web interaktif yang membantu pengguna memahami dan menyelesaikan permasalahan numerik melalui implementasi beberapa metode numerik secara visual dan terstruktur.

Aplikasi ini dirancang untuk mendukung pembelajaran, simulasi, dan penulisan jurnal ilmiah di bidang komputasi numerik.

---

## 2. Tujuan

- Memberikan pemahaman mendalam tentang metode iteratif numerik
- Memvisualisasikan proses konvergensi secara interaktif
- Membandingkan kinerja antar metode secara akademik
- Menjadi alat bantu dalam penulisan laporan dan jurnal ilmiah

---

## 3. Fitur

| Fitur | Keterangan |
|---|---|
| 📐 Persamaan Nonlinear | Menyelesaikan f(x) = 0 |
| 🔢 Sistem Persamaan Linear | Menyelesaikan Ax = b |
| 📊 Perbandingan Metode | Analisis perbandingan antar metode |
| 📋 Tabel Iterasi | Riwayat setiap langkah iterasi |
| 📈 Grafik Interaktif | Grafik fungsi + grafik error (Plotly) |
| ✅ Validasi Input | Pengecekan ekspresi dan parameter |

---

## 4. Metode Numerik

### Persamaan Nonlinear — mencari akar f(x) = 0

#### Fixed Point Iteration
- **Bentuk:** x = g(x)
- **Rumus:** x_{n+1} = g(x_n)
- **Input:** g(x), x₀, toleransi, maks. iterasi

#### Newton-Raphson
- **Rumus:** x_{n+1} = x_n − f(x_n) / f'(x_n)
- **Kelebihan:** Konvergensi kuadratik (sangat cepat)
- **Catatan:** Turunan f'(x) dihitung otomatis oleh SymPy

#### Secant
- **Rumus:** x_{n+1} = x_n − f(x_n) · (x_n − x_{n-1}) / (f(x_n) − f(x_{n-1}))
- **Kelebihan:** Tidak membutuhkan turunan
- **Input:** f(x), x₀, x₁, toleransi, maks. iterasi

### Sistem Persamaan Linear — mencari x dari Ax = b

#### Jacobi
- Semua x baru dihitung menggunakan nilai x dari iterasi **sebelumnya**
- Konvergen jika matriks A diagonally dominant

#### Gauss-Seidel
- Langsung menggunakan nilai x **terbaru** yang sudah dihitung
- Umumnya lebih cepat konvergen daripada Jacobi

---

## 5. Struktur Proyek

```
NUMERA/
│
├── app.py                ← UI + Navigasi + Input + Output
├── numerical_methods.py  ← Semua algoritma numerik
├── utils.py              ← Parsing, Validasi, Grafik
├── test_methods.py       ← Pengujian algoritma
├── requirements.txt      ← Dependensi library
├── README.md             ← Dokumentasi ini
│
└── assets/
    └── logo.png
```

---

## 6. Instalasi

### Prasyarat
- Python 3.10 atau lebih baru
- pip

### Langkah Instalasi

```bash
# Clone atau buka direktori proyek
cd NUMERA

# (Opsional) Buat virtual environment
python -m venv .venv
.venv\Scripts\activate        # Windows
source .venv/bin/activate     # Linux/macOS

# Install semua dependensi
pip install -r requirements.txt
```

---

## 7. Cara Menjalankan

```bash
# Jalankan aplikasi Streamlit
streamlit run app.py
```

Buka browser dan akses: **http://localhost:8501**

---

## 8. Menjalankan Pengujian

```bash
python test_methods.py
```

Contoh output:
```
============================================================
  PERSAMAAN NONLINEAR — f(x) = x² - 4, akar = 2
============================================================

Fixed Point Iteration  [g(x) = (x + 4/x) / 2, x₀ = 3]
  Solusi    : 2.0
  Iterasi   : 5
  Error     : 1.31e-11
  [PASS ✓] Konvergen
  [PASS ✓] Solusi mendekati 2

...

  ✅  Semua pengujian berhasil.
  ✅  Kelima metode bekerja dengan benar.
```

---

## 9. Contoh Penggunaan

### Persamaan Nonlinear

| Input | Nilai |
|---|---|
| Fungsi f(x) | `x**2 - 4` |
| Metode | Newton-Raphson |
| x₀ | 3 |
| Toleransi | 1e-6 |

**Output:**
```
Solusi         : 2.000000
Jumlah Iterasi : 5
Error Akhir    : 2.22e-16
Status         : ✓ Konvergen
```

### Sistem Persamaan Linear

```
Matriks A:     Vektor b:
2  1  1         6
1  3  1        10
1  1  4        12
```

**Output (Gauss-Seidel):**
```
x1 = 0.705882
x2 = 2.352941
x3 = 2.235294
Iterasi : 12
Status  : ✓ Konvergen
```

---

## 10. Format Input Ekspresi

Sistem menggunakan **SymPy** untuk parsing ekspresi secara aman:

| Fungsi Matematika | Format Input |
|---|---|
| x² − 4 | `x**2 - 4` atau `x^2 - 4` |
| sin(x) − x/2 | `sin(x) - x/2` |
| e^x − 3 | `exp(x) - 3` |
| ln(x) | `log(x)` |
| √x | `sqrt(x)` |
| \|x\| | `abs(x)` |

---

## 11. Validasi Input

NUMERA menangani berbagai kasus tidak valid:

| Kondisi | Pesan |
|---|---|
| Ekspresi kosong atau salah format | ⚠️ Persamaan tidak valid |
| f'(x₀) = 0 pada Newton-Raphson | ⚠️ Turunan bernilai nol |
| Diagonal matriks A = 0 | ⚠️ Elemen diagonal tidak boleh nol |
| Tidak konvergen dalam N iterasi | ⚠️ Metode belum mencapai toleransi |

---

## 12. Teknologi

| Library | Kegunaan |
|---|---|
| **Streamlit** | Framework web UI |
| **NumPy** | Komputasi numerik |
| **SymPy** | Parsing ekspresi & turunan simbolik |
| **Pandas** | Tabel iterasi |
| **Plotly** | Grafik interaktif |

---

## 13. Pengembang

Dibuat sebagai proyek akademik untuk mata kuliah **Metode Numerik**.

---

*NUMERA v1.0.0*
