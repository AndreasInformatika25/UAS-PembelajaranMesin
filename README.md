# [cite_start]Integrasi Topic Modeling, Social Network Analysis, dan NER pada Kasus Korban Pinjol [cite: 10, 11]

## 📌 Deskripsi Proyek
[cite_start]Repositori ini berisi dokumentasi dan implementasi *code* untuk Ujian Akhir Semester (UAS) mata kuliah Pembelajaran Mesin[cite: 10, 11]. [cite_start]Proyek ini berfokus pada integrasi tiga pendekatan analisis teks yaitu *Topic Modeling*, *Social Network Analysis* (SNA), dan *Named Entity Recognition* (NER) untuk membedah opini publik dengan tema utama "Korban Pinjol" (Pinjaman Online)[cite: 10, 11].

## 🛠️ Pengumpulan Data (Crawling)
[cite_start]Data dikumpulkan melalui platform Twitter (X) dan menghasilkan total 1538 data/tweet mentah yang disimpan dalam format Excel[cite: 20, 21]. 

[cite_start]Pencarian data dilakukan menggunakan sekumpulan kata kunci spesifik[cite: 14]:
* [cite_start]gagal bayar pinjol [cite: 15]
* [cite_start]pinjol galbay [cite: 16]
* [cite_start]dc lapangan pinjol [cite: 17]
* [cite_start]sebar data pinjol [cite: 18]
* [cite_start]korban pinjol [cite: 19]

## 🧹 Preprocessing Data
[cite_start]Untuk menghasilkan data yang siap diolah oleh model, dilakukan tahapan *preprocessing* sistematis[cite: 29]:
1. [cite_start]**Menghapus Duplikat:** Membersihkan *tweet* yang redundan[cite: 41, 42].
2. [cite_start]**Case Folding:** Menyeragamkan seluruh karakter teks menjadi huruf kecil (*lowercase*)[cite: 50].
3. [cite_start]**Cleaning Data:** Menghapus tag RT, URL/tautan, *mention*, karakter khusus, emoji, serta spasi berlebih[cite: 69, 73, 76, 78, 80].
4. [cite_start]**Ekstraksi Atribut:** Memisahkan *username* pada kolom *author* dan menarik seluruh *mention* spesifik untuk kebutuhan pembangunan jaringan SNA[cite: 84, 89, 92].
5. [cite_start]**Tokenisasi:** Memecah kalimat menjadi token kata menggunakan pustaka NLTK[cite: 100, 104].
6. [cite_start]**Normalisasi:** Memperbaiki penulisan kata tidak baku menggunakan penggabungan kamus eksternal (CSV) dan kamus manual[cite: 110, 111].
7. [cite_start]**Stop Word Removal:** Memfilter kata-kata hubung atau tidak bermakna menggunakan bantuan pustaka NLTK, CSV, dan kamus manual (*custom filter* khusus domain pinjol)[cite: 132, 408, 409, 410, 411, 412].
8. [cite_start]**Stemming:** Mengembalikan kata ke bentuk dasarnya menggunakan *library* Sastrawi[cite: 144, 146].

## ⚙️ Metodologi & Hasil
### 1. Topic Modeling
Proyek ini membandingkan penggunaan dua algoritma *clustering*:
* [cite_start]**Frequent Term-Based Text Clustering (FTC):** Menggunakan ekstraksi *frequent termsets* dan perhitungan *Entropy Overlap* dengan rumus $EO(C_{i})=\sum_{D_{j}\in C_{i}}\frac{-1}{f_{j}}.Ln(\frac{1}{f_{j}})$ untuk mengevaluasi kualitas klaster[cite: 184, 185, 189]. [cite_start]Model dijalankan dengan parameter *minimum support* (`minsup`) sebesar 0.05[cite: 238].
* [cite_start]**Latent Dirichlet Allocation (LDA):** Berbasis pemodelan probabilistik dengan evaluasi menggunakan metrik *Elbow Perplexity*[cite: 404, 463]. [cite_start]Berdasarkan kurva perplexity, didapatkan nilai K optimal sebesar K=3[cite: 520, 529].
  * [cite_start]**Topik 1:** Teror Debt Collector & Korban Pinjol [cite: 530]
  * [cite_start]**Topik 2:** Utang, Kredit & Kondisi Ekonomi [cite: 532]
  * [cite_start]**Topik 3:** Pelaporan Pinjol Ilegal & Dampak Sosial [cite: 534]

### 2. Social Network Analysis (SNA)
[cite_start]Digunakan untuk memetakan dinamika interaksi (mention) antar akun terkait topik Pinjol[cite: 548, 669].
* [cite_start]**Visualisasi & Tools:** Data diekspor ke dalam bentuk `edge_list.csv` dan `node_list.csv` untuk diproses di Gephi, serta disajikan interaktif melalui *library* PyVis[cite: 550, 551, 552].
* **Centrality Metrics:**
  * [cite_start]Top Akun Paling Sering Di-mention (*Indegree*): `@ojkindonesia` (0.0187) dan `@prabowo` (0.0156)[cite: 635, 646].
  * [cite_start]Top Akun Paling Aktif Mention (*Outdegree*): `@belengbeleng687` (0.0374) dan `@divhumas_polri` (0.0234)[cite: 652, 663].
* [cite_start]Hasil analisis jaringan di Gephi mencapai skor *Community Detection* sebesar 0.929[cite: 676].

### 3. Named Entity Recognition (NER)
[cite_start]Mengekstrak entitas-entitas penting menggunakan dua metode untuk perbandingan komprehensif[cite: 687]:
* [cite_start]**NER SpaCy Indonesian:** Menggunakan model *pre-trained* `id_ner_spacy_indonesian` untuk mendeteksi entitas bersasarkan label ORG, GPE, PERSON, NOR, dan LOC[cite: 692, 696, 700].
* [cite_start]**NER Rule-Based:** Mengandalkan integrasi pola *Regex* dan *Custom Dictionary* (seperti 'ojk', 'polisi', 'bpjs', dll)[cite: 762, 764, 772].
* [cite_start]**Kesimpulan NER:** Metode *Rule-Based* terbukti memberikan hasil ekstraksi jumlah entitas (seperti "Indonesia", "Bpjs", dan "Ojk") yang lebih banyak dan relevan dibandingkan metode SpaCy[cite: 847, 850].

## 🧑‍💻 Penulis
* [cite_start]**Nama / NIM:** Andreas / 2411500750 [cite: 6]
