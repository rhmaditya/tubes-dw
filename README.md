## Misi 1 - Dokumentasi Spesifikasi

# LAPORAN PERANCANGAN DATA WAREHOUSE
**Industri Sepak Bola Taktika: “Where Data Meets Strategy”**

## A. Profil Industri & Masalah Bisnis

Di tengah transformasi digital dunia sepak bola, data kini menjadi aset penting untuk merumuskan strategi kemenangan. Namun, kompleksitas data mulai dari statistik pemain, jalannya pertandingan, hingga formasi dan taktik membuat klub dan pelatih kesulitan mengakses wawasan yang benar-benar relevan.

Taktika hadir sebagai penyedia layanan data analytics untuk sepak bola modern. Kami mengubah data mentah dari lebih dari 25.000 pertandingan dan 10.000 pemain Eropa menjadi insight taktis dan strategis untuk berbagai pihak: klub, pelatih, analis, media, bahkan fans. Tantangan utamanya adalah integrasi data dari berbagai sumber yang tidak terstruktur, sehingga dibutuhkan solusi Data Warehouse (DW) sebagai pondasi sistem analitik yang solid, akurat, dan mudah digunakan.

## B. Daftar Stakeholder & Tujuan Bisnis

### Stakeholder & Peran dalam Industri Sepak Bola

| Stakeholder          | Peran dalam Industri Sepak Bola                             | Tujuan Penggunaan Data Warehouse                           |
|----------------------|------------------------------------------------------------|-----------------------------------------------------------|
| Pelatih Tim          | Menentukan strategi dan susunan pemain                      | Mengoptimalkan formasi dan taktik berdasarkan data lawan   |
| Analis Klub          | Menganalisis performa tim dan pemain                        | Mengukur performa per pertandingan, musim, dan lawan       |
| Departemen Rekrutmen | Menyeleksi dan mengevaluasi pemain baru                     | Menilai potensi pemain berdasarkan statistik historis       |
| Media & Penyiar      | Menyampaikan berita dan analisis pertandingan               | Menyediakan statistik menarik dan prediktif untuk penonton |
| Fans & Komunitas     | Konsumen informasi sepak bola                               | Mengakses insight mendalam, tidak hanya highlight atau skor|

### Tujuan Bisnis

- Mengoptimalkan strategi pertandingan berdasarkan data historis lawan
- Meningkatkan efektivitas scouting pemain melalui data performa objektif
- Menyediakan laporan dan insight cepat untuk pelatih dan analis teknis
- Memberikan informasi taktis yang mudah diakses untuk media dan fans
- Menyatukan sumber data pertandingan dalam satu sistem terpusat (DW)

### Interview Simulasi (Pelatih Kepala):

1. Saat menyusun strategi melawan lawan tertentu, data apa yang paling Anda butuhkan?
2. Apakah Anda ingin melihat performa pemain lawan berdasarkan formasi yang digunakan?
3. Seberapa sering Anda ingin mendapatkan laporan data (harian, mingguan, sebelum match)?
4. Apakah Anda lebih suka data visual (grafik, heatmap) atau tabel?
5. Pernahkah Anda kehilangan peluang taktik karena keterlambatan data?

### Studi Kasus

Banyak klub sepak bola di Eropa mengalami kesulitan dalam melakukan analisis taktik lawan karena data tersebar di banyak file, tidak real-time, dan tidak disesuaikan dengan kebutuhan pelatih. Dengan DW, semua data ini dapat diakses dalam satu sistem dan bisa ditampilkan sesuai kebutuhan pelatih — misal: "Rekap 5 pertandingan terakhir melawan tim dengan formasi 4-3-3."

## C. Daftar Fakta & Dimensi

### Fakta (Measures)

- Jumlah Gol
- Jumlah Assist
- Jumlah Tembakan & Akurasi
- Jumlah Intersep / Tackle
- Rata-rata Rating Pemain
- Penguasaan Bola (%)

### Dimensi

- **Waktu**: Tanggal, musim, pekan ke-
- **Pemain**: Nama, posisi, usia, tinggi, kemampuan individu
- **Klub**: Nama klub, formasi, pelatih, liga
- **Kompetisi**: Nama liga, negara, tahun kompetisi
- **Lokasi**: Stadion, status (home/away), kota pertandingan
- **Formasi**: Formasi yang digunakan klub (misal: 4-3-3, 3-5-2)

### Diagram Skema

#### Penjelasan Skema Bintang

Skema bintang (Star Schema) adalah model data dimensional yang umum digunakan dalam data warehouse untuk memfasilitasi analisis cepat dan efisien. Dalam skema ini:

- **Tabel Fakta** berada di tengah dan berisi data kuantitatif seperti gol, assist, dan statistik performa.
- **Tabel Dimensi** mengelilingi tabel fakta dan menyediakan konteks analisis, seperti siapa pemainnya, kapan pertandingan berlangsung, di mana lokasinya, dan dalam kompetisi apa.
  
Setiap tabel dimensi terhubung langsung ke tabel fakta melalui kunci primer/asing (primary/foreign key). Bentuk "bintang" muncul dari struktur ini: fakta di tengah, dan dimensi menyebar keluar.

**Keunggulan dari skema ini:**

- Query analisis menjadi lebih cepat
- Struktur mudah dipahami oleh analis bisnis dan pelatih
- Mendukung visualisasi dan pelaporan yang fleksibel

## D. Sumber Data & Metadata

| Nama File    | Kaggle Konten Utama                             | Format | Frekuensi Update |
|--------------|-------------------------------------------------|--------|------------------|
| Match.csv    | Data pertandingan, skor, tim, event pertandingan | CSV    | Mingguan         |
| Player.csv   | Atribut & statistik pemain                      | CSV    | Triwulanan       |
| Team.csv     | Info klub: nama, formasi, pelatih               | CSV    | Triwulanan       |
| League.csv   | Daftar liga, negara                             | CSV    | Tahunan          |

### Contoh Metadata:

| Nama Kolom        | Tipe Data   | Deskripsi                                                   |
|-------------------|-------------|-------------------------------------------------------------|
| home_team_goal    | INTEGER     | Jumlah gol oleh tim tuan rumah                              |
| away_team_goal    | INTEGER     | Jumlah gol oleh tim tamu                                    |
| buildUpPlaySpeed  | STRING      | Strategi serangan: cepat/lambat                             |
| player_api_id     | INTEGER     | ID unik pemain yang digunakan lintas sistem                 |
| date              | DATE        | Tanggal pertandingan berlangsung                            |
| possession_home   | FLOAT       | Persentase penguasaan bola oleh tim tuan rumah              |

## E. Referensi

1. Hugomathien, “European Soccer Database,” Kaggle Dataset:  
   [Kaggle Link](https://www.kaggle.com/datasets/hugomathien/soccer)
   
2. Kimball, Ralph. *The Data Warehouse Toolkit*
