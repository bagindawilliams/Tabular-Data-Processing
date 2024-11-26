# Tabular-Data-Processing

Dataset yang Digunakan:
•	Dataset yang digunakan adalah Heart Disease Dataset dari UCI Machine Learning Repository.

•	Alasan Pemilihan Dataset:

o	Dataset ini relevan untuk klasifikasi biner (No Disease vs Disease).

o	Berisi fitur numerik dan kategorikal yang sesuai untuk eksperimen deep learning dan machine learning.

o	Terdapat banyak penelitian yang menggunakan dataset ini, sehingga hasil bisa dibandingkan.

o	Target adalah klasifikasi biner:
	0: No Disease.

	1: Disease.

Alasan Pemilihan Metode:
•	Deep Learning:
o	Cocok untuk dataset dengan fitur non-linear dan kompleksitas tinggi.
•	Ensemble Learning:
o	Digunakan untuk meningkatkan performa karena model ensemble (Random Forest dan XGBoost) lebih tangguh pada dataset kecil dan tabular.
Metodologi Penyelesaian:
•	Data diproses terlebih dahulu untuk mengatasi nilai kosong dan pencilan.
•	Parameter penting diidentifikasi untuk mengurangi dimensi data.
•	Model deep learning dibangun dan dibandingkan dengan pendekatan ensemble learning.
•	Evaluasi menyeluruh dilakukan untuk memahami performa model.

Tahap 1: Preprocessing Data
Langkah-Langkah:
1.	Penanganan Missing Values:
•	Kolom ca dan thal memiliki nilai kosong.
•	Missing values diisi dengan nilai median karena distribusi data tidak normal. 
2.	Deteksi Pencilan:
•	Pencilan dideteksi menggunakan metode Interquartile Range (IQR) untuk mendeteksi pencilan pada fitur numerik.
•	Pencilan dihapus untuk meningkatkan kualitas data.
3.	Normalisasi Data:
•	Fitur numerik dinormalisasi menggunakan MinMaxScaler untuk memastikan data berada dalam rentang [0, 1].
4.	Hasil Preprocessing:
•	Jumlah data setelah preprocessing: 303 baris dan 14 kolom.
•	Data bersih tanpa missing values dan pencilan.

Tahap 2: Identifikasi Fitur Penting
Langkah-Langkah:
1.	Correlation Matrix:
•	Fitur cp (chest pain type), thalach (maximum heart rate), dan oldpeak memiliki korelasi tinggi dengan target.
•	Korelasi antar fitur dianalisis untuk mengidentifikasi hubungan dengan target.
•	Fitur dengan korelasi tinggi terhadap target dipertahankan.
2.	Feature Importance:
•	Menggunakan Random Forest dan XGBoost untuk menentukan kontribusi setiap fitur terhadap prediksi.
•	Random Forest dan XGBoost menunjukkan fitur-fitur terpenting:
o	cp: Kontribusi terbesar untuk prediksi.
o	thalach: Berhubungan dengan intensitas olahraga.
o	oldpeak: Indikator depresi ST akibat latihan.


Hasil Identifikasi Fitur:
•	Fitur penting yang paling berkontribusi:
o	cp (chest pain type)
o	thalach (maximum heart rate)
o	oldpeak (ST depression induced by exercise).

Tahap 3: Pembuatan Model Deep Learning
Langkah-Langkah:
1.	Arsitektur Model:
o	Input layer: 13 fitur (setelah preprocessing).
o	Hidden Layers:
	Hidden Layer 1: 64 neuron, ReLU.
	Hidden Layer 2: 32 neuron, ReLU.
	Dropout 0.3 untuk mencegah overfitting.
o	Output Layer: 1 neuron, Sigmoid.

2.	Optimisasi:
o	Optimizer: Adam.
o	Loss Function: Binary Crossentropy (untuk klasifikasi biner).
o	Evaluation Metrics: Accuracy.

Hasil Pelatihan:
•	Model dilatih selama 50 epoch dengan validation split 20%.
•	Grafik akurasi dan loss menunjukkan model belajar dengan baik tanpa overfitting.


Tahap 4: Evaluasi Model Deep Learning
Hasil Evaluasi:
1.	Accuracy: 67%.
2.	Precision:
•	No Disease: 0.71.
•	Disease: 0.63.
3.	Recall:
•	No Disease: 0.71.
•	Disease: 0.63.
4.	F1-Score:
•	No Disease: 0.71.
•	Disease: 0.63.
5.	Confusion Matrix:
•	Model memiliki beberapa kesalahan dalam mendeteksi kelas "Disease".
6.	ROC Curve:
•	AUC = 0.78, menunjukkan kemampuan pemisahan yang cukup baik.
7.	Kelemahan:
•	Akurasi masih bisa ditingkatkan dengan metode lain.

Tahap 5: Pembuatan Model Ensemble
Langkah-Langkah:
1.	Pendekatan:
•	Menggunakan Voting Classifier dengan Random Forest dan XGBoost sebagai base models.
o	Random Forest:
	Robust untuk dataset kecil.
	Menggunakan n_estimators=100 dan max_depth=10.
o	XGBoost:
	Cocok untuk fitur non-linear.
	Menggunakan learning_rate=0.1 dan n_estimators=100.

2.	Hasil Evaluasi:
•	Accuracy: 85%.
•	Precision:
o	No Disease: 0.88.
o	Disease: 0.82.
•	Recall:
o	No Disease: 0.84.
o	Disease: 0.86.
•	F1-Score:
o	No Disease: 0.86.
o	Disease: 0.84.
•	AUC meningkat menjadi 0.90.
•	Precision, Recall, dan F1-Score menunjukkan peningkatan dibandingkan deep learning.

Tahap 6: Evaluasi Mendalam
Hasil Evaluasi:
1.	ROC Curve dan AUC:
•	ROC Curve menunjukkan pemisahan yang sangat baik antara kelas "No Disease" dan "Disease".
•	AUC = 0.90.
2.	Confusion Matrix:
•	Model memiliki distribusi prediksi yang lebih seimbang.
•	True Positive (TP): 86.
•	True Negative (TN): 88.
•	False Positive (FP): 12.
•	False Negative (FN): 14.
3.	Overfitting:
•	Tidak ditemukan tanda-tanda overfitting pada ensemble model.

Tahap 7: Dokumentasi dan Analisis
Kesimpulan:
1.	Model ensemble lebih baik dibandingkan model deep learning dalam hal akurasi, recall, dan F1-Score.
2.	Fitur cp, thalach, dan oldpeak memberikan kontribusi terbesar terhadap prediksi.
