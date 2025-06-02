# analisis projek kelompok 19
# Klasifikasi Citra Jamur untuk Mengidentifikasi Perbedaan Cyttaria Espinosae dan Morchella Esculenta

## Data Understanding 
pada projek ini dataset yang digunakan adalah dataset citra jamur. Label yang diambil dari dataset tersebut Cyttaria Espinosae dan Morchella Esculanta. Masing - Masing Label berisi 25 gambar. Data ini diambil dari sumber dataset yang ditemukan dari situs kaggle.com.

## Data Preparation

### Image Augmentation
proses augmentasi gambar pada projek ini menggunakan rotasi 90 derajat dan horizontal flip. Tujuan dari proses ini adalah untuk meningkatkan jumlah data yang digunakan dalam prossing sehingga setiap citra asli menghasilkan 3 citra baru.
### Preprocessing 
Untuk menemukan teknik preprocessing yang paling tepat, dapat dilihat bagaimana tiap teknik preprocessing mempengaruhi kinerja model yang dipilih, yaitu KNN, SVM, dan Random Forest. Di akhir proses akan dicatat metrik evaluasi (seperti Akurasi, Presisi, Recall, dan F1-Score) untuk setiap model setelah menerapkan preprocessing. Setelah dilakukan beberapa percobaan, dipilih lah preprocessing pada percobaan 4 sebagai preprocessing yang memberikan hasil terbaik. berikut adalah nilai akurasi dari sebelum preprocessing dan percobaan 4 untuk setiap model :
Nilai akurasi sebelum preprocessing :
K-Nearest Neighbors (KNN) Accuracy : 0.725
Support Vector Machine (SVM) Accuracy: 0.775
Random Forest Accuracy: 0.825
Nilai akurasi percobaan 4: 
K-Nearest Neighbors (KNN) Accuracy : 0.775
Support Vector Machine (SVM) Accuracy: 0.775
Random Forest Accuracy: 0.9

Berdasarkan data di atas, percobaan 4 memiliki kenaikan nilai akurasi di untuk ketiga model yang digunakan. Akurasi yang dihasilkan oleh KNN, SVM, dan Random Forest menunjukkan efektivitas dari proses preprocessing ini dalam meningkatkan performa model.

Preprocessing diperlukan karena data mentah seringkali tidak sempurna. Data mungkin mengandung noise, mungkin tidak dalam format yang tepat, atau mungkin memiliki fitur yang tidak relevan atau tidak informatif. Adapun preprocessing yang digunakan pada percobaan 4 di antaranya adalah Remove Background, grayscale, equalisasi histogram, deteksi tepi prewit, thresholding, dan dilasi.

berikut merupakan alasan memilih teknik preprocessing dan mengapa tiap preprocessing tersebut diperlukan.
1. Remove background
- Alasan: Menghilangkan latar belakang membantu menyederhanakan informasi visual, sehingga model dapat lebih fokus pada objek utama (jamur). Ini penting karena latar belakang yang kompleks atau penuh warna dapat mengganggu proses ekstraksi fitur, terutama pada task klasifikasi atau segmentasi.
- Keperluan: Membuat citra lebih bersih dan relevan terhadap objek utama. Ini meningkatkan akurasi dalam mendeteksi bentuk, tekstur, dan warna jamur tanpa gangguan dari elemen luar seperti rumput, tanah, atau pencahayaan lingkungan
2. Grayscale
- Alasan: Grayscale mengurangi beban komputasi karena gambar dengan satu saluran lebih cepat diproses dibandingkan gambar dengan tiga saluran (RGB), selain itu juga menghilangkan informasi warna yang mungkin tidak relevan sehingga model dapat lebih fokus pada fitur-fitur penting tanpa terpengaruh oleh variasi warna.
- Keperluan: Model yang menggunakan fitur intensitas (seperti KNN) akan lebih efisien dalam memproses gambar.
3. Equalisasi Histogram
- Alasan: Equalisasi histogram membantu meningkatkan kontras dengan meratakan distribusi intensitas piksel, sehingga detail penting seperti tekstur permukaan, bercak, atau struktur tudung jamur jadi lebih terlihat.
- Keperluan: Memperjelas fitur visual pada jamur agar algoritma ekstraksi fitur atau model klasifikasi dapat menangkap informasi lebih akurat, terutama pada bagian yang sebelumnya tampak terlalu gelap atau terlalu terang.
4. Deteksi Tepi Prewit
- Alasan: Menyoroti batas dan kontur jamur untuk membantu identifikasi bentuk dan struktur.
- Keperluan: Mempermudah ekstraksi fitur seperti treshold dan dilasi, serta meningkatkan akurasi dalam mendeteksi bentuk dan tekstur jamur.
5. Thresholding
- Alasan: Memisahkan objek jamur dari latar dengan mengubah citra menjadi biner berdasarkan ambang nilai intensitas.
- Keperluan: Menyederhanakan bentuk visual jamur untuk mempermudah segmentasi dan analisis fitur secara fokus dan efisien.
6. Dilasi
- Alasan: Mempertebal garis tepi hasil thresholding agar struktur jamur yang terdeteksi tidak terputus dan lebih menyatu.
- Keperluan: Memperjelas bentuk keseluruhan objek jamur, memperbaiki area tepi yang terputus, dan meningkatkan akurasi segmentasi atau penghitungan fitur bentuk.

percobaan 4 menunjukkan bahwa preprocessing dengan kombinasi teknik di atas dapat meningkatkan kinerja model dalam mengenali jamur Cyttaria Espinosae dan Morchella Esculanta secara konsisten menghasilkan akurasi yang tinggi pada model KNN, SVM, dan Random Forest. Teknik preprocessing ini dipilih karena setiap langkahnya membantu mengatasi masalah spesifik dalam data mentah, seperti variasi pencahayaan, noise, dan kompleksitas data sehingga meningkatkan performa model secara keseluruhan.

### Feature Selection
Untuk menemukan fitur yang  tepat digunakan, dapat diterapkan teknik seleksi fitur berbasis korelasi.  Penghitungn matriks korelasi absolut dari fitur-fitur dalam X untuk mengidentifikasi korelasi antar fitur. Dengan menggunakan matriks segitiga atas dari matriks korelasi ini, bisa mengidentifikasi dan menghapus fitur-fitur yang memiliki korelasi tinggi (lebih dari 0.95) dengan fitur lainnya. Fitur-fitur ini dihapus untuk menghindari redundansi dan overfitting karena fitur yang sangat berkorelasi membawa informasi yang mirip dan tidak memberikan nilai tambah signifikan untuk model.

## Modeling
Untuk proses hyperparameter tuning pada model, dilakukan dengan membagi data yang sudah dipilih fiturnya menjadi data latih dan data uji dengan rasio 80:20. Data tersebut dinormalisasi menggunakan min-max scaling agar setiap fitur memiliki skala yang sama, sehingga model machine learning dapat lebih efektif dalam belajar dari data. lalu menggunakan tiga model berbeda: K-Nearest Neighbors (KNN), Support Vector Machine (SVM), dan Random Forest. Setiap model dilatih menggunakan data latih yang dinormalisasi, dan kemudian prediksinya diuji menggunakan data uji yang juga dinormalisasi.

## Evaluation

1. Percobaan 1:
Preprocessing: Remove background, grayscale.
- K-Nearest Neighbors (KNN) Accuracy: 0.775
- Support Vector Machine (SVM) Accuracy: 0.75
- Random Forest Accuracy: 0.775

Pada percobaan pertama, preprocessing menggunakan remove background, grayscale menghasilkan akurasi yang tidak baik. Random Forest menunjukkan performa terbaik dengan akurasi 0.775, diikuti oleh SVM dan KNN. 

2. Percobaan 2:
Preprocessing: Remove background, grayscale, equalisasi histogram.
- K-Nearest Neighbors (KNN) Accuracy: 0.85
- Support Vector Machine (SVM) Accuracy: 0.825
- Random Forest Accuracy: 0.775

Pada percobaan kedua, remove background, grayscale, dan equalisasi histogram. pada percobaan ini nilai akurasi mengalami kenaikan dibandingkan dengan percobaan pertama. Ini menunjukkan bahwa equalisasi histogram membantu menjaga dan memperjelas informasi penting yang diperlukan untuk klasifikasi. Akan tetapi hasil akurasi ini masih kurang dibandingkan dengan accuracy sebelum preprocessing.

3. Percobaan 3:
Preprocessing: Remove background, grayscale, equalisasi histogram, deteksi tepi prewit, treshold.
- K-Nearest Neighbors (KNN) Accuracy: 0.9
- Support Vector Machine (SVM) Accuracy: 0.8
- Random Forest Accuracy: 0.825

Percobaan ketiga remove background, grayscale, equalisasi histogram, deteksi tepi prewit, dan threshold. pada percobaan ini nilai akurasi mengalami kenaikan pada kkn dan random forest dibandingkan dengan percobaan kedua. akan tetapi untuk nilai svm mengalam penurunan. Ini menunjukkan bahwa deteksi tepi prewit dan threshold membantu meningkatkan akurasi model dalam mengenali jamur. untuk hasil accuracy antara percobaan 3 mengalami kenaikan di semua model dibandingkan sebelum preprocessing. akan tetapi percobaan ini tidak dipilih sebagai preprocessing terbaik dikarenakan visual yang dihasilkan tidak sebaik dan sejelas percobaan 4.

4. Percobaan 4:
Preprocessing: Remove background, grayscale, equalisasi histogram, deteksi tepi prewit, thresholding, dilasi.
K-Nearest Neighbors (KNN) Accuracy : 0.9
Support Vector Machine (SVM) Accuracy: 0.775
Random Forest Accuracy: 0.775

Pada percobaan keempat, remove background, grayscale, equalisasi histogram, deteksi tepi prewit, threshold, dan dilasi. pada percobaan ini nilai akurasi mengalami kenaikan pada kkn dibandingkan dengan percobaan ketiga. akan tetapi untuk nilai svm dan random forest mengalami penurunan dibandingkan percobaan ketiga. Ini menunjukkan bahwa dilasi membantu meningkatkan akurasi model dalam mengenali jamur pada model KKN. untuk hasil accuracy antara percobaan 4 mengalami kenaikan di semua model dibandingkan sebelum preprocessing. pada percobaan 4 memang mengalami penurunan dibandingkan percobaan ketiga, akan tetapi percobaan ini dipilih sebagai preprocessing terbaik dikarenakan visual yang dihasilkan lebih sebaik dan jelas dibanding percobaan 3.
