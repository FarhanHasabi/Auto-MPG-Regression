# Auto MPG Prediction with ElasticNet Regression

Prediksi konsumsi bahan bakar mobil (MPG) menggunakan dataset **Auto MPG** dari UCI Machine Learning Repository, dengan preprocessing, transformasi log pada target, dan tuning hyperparameter menggunakan **Optuna**.

## Dataset
- **Sumber**: [UCI Auto MPG Dataset (ID: 9)](https://archive.ics.uci.edu/ml/datasets/auto+mpg)
- **Fitur**: `cylinders`, `displacement`, `horsepower`, `weight`, `acceleration`, `model_year`, `origin`
- **Target**: `mpg` (Miles Per Gallon)
- **Jumlah sampel setelah pembersihan**: 392

## Preprocessing
- Ganti nilai `'?'` dengan `NaN` dan hapus baris yang mengandung missing values.
- Konversi tipe data ke format numerik/kategorikal yang sesuai.
- **Log-transform** pada target (`mpg`) untuk mendekati distribusi normal.
- Standarisasi fitur numerik (`StandardScaler`).
- One-hot encoding untuk fitur kategorikal (`origin`).

## Model & Optimasi
- **Algoritma**: `ElasticNet` (kombinasi L1 + L2 regularization)
- **Pipeline**: Preprocessing + regresi dalam satu alur terintegrasi.
- **Hyperparameter Tuning**: Menggunakan **Optuna** (150 trials) untuk mengoptimalkan:
  - `alpha` (kekuatan regularisasi)
  - `l1_ratio` (proporsi L1 penalty)
- **Evaluasi**: Dilakukan pada skala asli (`exp(log_mpg)`) untuk interpretasi realistis.

## Hasil Performa (Skala Asli)
| Metrik   | Nilai     |
|----------|-----------|
| R² Score | ~0.85     |
| RMSE     | ~2.1 MPG  |

## Dependensi
```txt
ucimlrepo
pandas
numpy
matplotlib
seaborn
scikit-learn
optuna
```

## Cara Menjalankan
1. Clone repositori ini:
```
git clone https://github.com/username/auto-mpg-prediction.git
cd auto-mpg-prediction
```
2. Install dependensi:
```
pip install -r requirements.txt
```
3. Jalankan notebook utama:
```
jupyter notebook main.ipynb
```