# Akuisisi Data Nyata melalui Web Scraping dan OpenStreetMap API

## Identitas Mahasiswa & Mata Kuliah
* **Nama:** Gabriela Arnaiz Lopita
* **NIM:** 2501010326
* **Email:** 2501010326@instiki.ac.id
* **Mata Kuliah:** Akuisisi dan Manajemen Data (BIFP-243)
* **Dosen Pengampu:** Dr. I Gede Totok Suryawan, S.Kom., M.T.
* **Sektor:** Pariwisata dan Kebudayaan (Labuan Bajo, Kabupaten Manggarai Barat, NTT)

---

## 1. Sumber Data
* **Sumber 1 (Geospasial):** OpenStreetMap via Overpass API
  * **URL:** `https://overpass-api.de/api/interpreter`
  * **Penerbit:** Komunitas Kontributor OpenStreetMap (OSM)
* **Sumber 2 (Web Scraping):** Portal Informasi Wisata Labuan Bajo
  * **URL:** `https://ita.travel/destination/indonesia/labuan-bajo`
  * **Penerbit:** ITA Travel Portal

## 2. Tanggal dan Jam Akses
* **Waktu Akses:** 15 November 2026, pukul 15:21:00 WITA (Waktu Indonesia Tengah)

## 3. Metode Akuisisi
* **API (OpenStreetMap):**
  * **Endpoint:** `/api/interpreter`
  * **Parameter:** *Bounding Box* `[bbox: -8.55,119.83,-8.45,119.92]` dengan filter tag `["tourism"]` dan `["amenity"~"restaurant|cafe|fast_food|hotel|hostel|motel"]`.
* **Web Scraping:**
  * **Halaman Target:** `https://ita.travel/destination/indonesia/labuan-bajo`
  * **Selector:** Menargetkan elemen penampung artikel perjalanan atau destinasi (`div` dengan nama kelas bertema `card`, `destination`, atau `item`). Proses ini dilengkapi dengan *fallback mechanism* lokal terstruktur guna menjamin keberlanjutan data jika server utama mengembalikan status HTTP 404.

## 4. Batasan Etika
* **Ketentuan API & `robots.txt`:** Mematuhi aturan `robots.txt` OpenStreetMap dengan menyertakan *header* `User-Agent` berisi identitas akademik yang jelas.
* **Jeda Waktu (*Rate Limiting*):** Menerapkan penundaan (`time.sleep(2)`) sebelum pengiriman *request* untuk menghormati server target.
* **Lisensi:**
  * Data OSM berlisensi **ODbL (Open Database License)** yang mewajibkan atribusi kepada kontributor.
  * Data wisata lokal digunakan murni untuk keperluan studi akademis non-komersial (*Fair Use*).
* **Data yang Sengaja Tidak Diambil:** Informasi pribadi pengelola penginapan, nomor telepon personal, dan data transaksi keuangan.

## 5. Penjelasan Kolom Dataset

### A. `openstreetmap_labuanbajo.csv` (Fasilitas Wisata)

| Nama Kolom | Deskripsi |
| :--- | :--- |
| `osm_id` | ID unik objek di OpenStreetMap. |
| `type` | Tipe data spasial (`node` / `way`). |
| `latitude` | Koordinat lintang. |
| `longitude` | Koordinat bujur. |
| `name` | Nama fasilitas atau amenitas. |
| `amenity` | Klasifikasi jenis amenitas (restoran, hotel, atraksi). |
| `website` | Situs web resmi fasilitas (jika ada). |
| `opening_hours` | Jam operasional fasilitas. |

### B. `scraping_labuanbajo.csv` (Destinasi Wisata)

| Nama Kolom | Deskripsi |
| :--- | :--- |
| `destination_id` | Kode ID unik destinasi wisata. |
| `destination_name` | Nama destinasi pariwisata. |
| `category` | Kategori atraksi (Atraksi Alam atau Petualangan/Budaya). |
| `location` | Lokasi administratif daerah. |
| `accessibility` | Jenis akses menuju lokasi (akses *boat*, darat, dll.). |
| `source_url` | URL sumber rujukan data. |

## Hasil Akuisisi dan Pengolahan Data

### 1. Ringkasan Hasil Akuisisi Data

Berdasarkan proses akuisisi data pariwisata, diperoleh data dari beberapa sumber, yaitu Kementerian Pariwisata (Kemenpar), OpenStreetMap (OSM) melalui Overpass API, dan Wikipedia. Data yang diperoleh kemudian melalui proses pembersihan dan pengolahan sebelum diintegrasikan menjadi dataset akhir.

Berikut ringkasan hasil akuisisi data:

| Sumber Data | Jumlah Data | Keterangan |
|---|---:|---|
| Kemenpar Nasional | 150 baris, 13 kolom | Data pariwisata tingkat nasional |
| Kemenpar Manggarai Raya | 120 baris | Data wilayah Manggarai Raya |
| Manggarai Barat | 50 baris | Data Kabupaten Manggarai Barat |
| Manggarai | 35 baris | Data Kabupaten Manggarai |
| Manggarai Timur | 35 baris | Data Kabupaten Manggarai Timur |
| Overpass API | 1.530 baris | Data mentah dari OpenStreetMap |
| OSM Bersih | 910 baris | Data setelah proses pembersihan |
| Kecamatan Wikipedia | 34 baris | Data administratif kecamatan |
| **Dataset Akhir** | **910 baris, 36 kolom** | **Hasil akhir pengolahan data** |

### 2. Hasil Data Cleaning dan Integrasi

Data yang diperoleh dari berbagai sumber diproses melalui tahapan pembersihan (*data cleaning*) untuk mengurangi data duplikat dan memperbaiki kualitas data. 

Data mentah dari Overpass API yang awalnya berjumlah 1.530 baris menghasilkan 910 baris setelah proses pembersihan. Selanjutnya, data dari sumber-sumber yang digunakan diolah dan diintegrasikan menjadi dataset akhir dengan ukuran 910 baris dan 36 kolom.

### 3. Pemeriksaan Persyaratan Jumlah Data

Berdasarkan hasil pengolahan, dataset telah memenuhi persyaratan jumlah minimum data sebagai berikut:

| Persyaratan | Jumlah Minimum | Hasil Dataset | Status |
|---|---:|---:|---|
| Soal 1 | 100 baris | 910 baris | Memenuhi |
| Soal 3 | 30 baris | 910 baris | Memenuhi |

Hasil pemeriksaan program:

```text
Kemenpar nasional      : (150, 13)
Kemenpar Manggarai Raya: 120

kabupaten
Manggarai Barat    50
Manggarai          35
Manggarai Timur    35

API Overpass (mentah)  : 1530
OSM bersih             : 910
Kecamatan Wikipedia    : 34
Dataset akhir          : (910, 36)

Syarat >=100 baris (Soal 1): True
Syarat >=30 baris  (Soal 3): True
```

### 4. Kesimpulan

Berdasarkan hasil akuisisi, pembersihan, dan integrasi data, diperoleh dataset akhir sebanyak **910 baris dan 36 kolom**. Jumlah tersebut telah memenuhi persyaratan minimum data pada Soal 1 dan Soal 3. Dataset ini selanjutnya dapat digunakan untuk analisis dan eksplorasi data pariwisata.

**Catatan:** Jumlah baris menunjukkan banyaknya record, bukan otomatis jumlah destinasi wisata unik. Validasi wilayah dan duplikasi tetap diperlukan sebelum dataset digunakan sebagai data final penelitian.

