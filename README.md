RTM Tugas 1: Akuisisi Data Nyata melalui Web Scraping dan OpenStreetMap API
Identitas Pemilik Proyek
Nama: GABRIELA ARNAIZ LOPITA
NIM: 2501010326
Email: 2501010326@instiki.ac.id
Mata Kuliah: Akuisisi dan Manajemen Data (BIFP-243)
Dosen Pengampu: Dr. I Gede Totok Suryawan, S.Kom., M.T.
Sektor: Pariwisata dan Kebudayaan (Labuan Bajo, Kabupaten Manggarai Barat, NTT)
1. Sumber Data
Sumber 1 (Geospasial): OpenStreetMap via Overpass API
URL: https://overpass-api.de/api/interpreter
Penerbit: Komunitas Kontributor OpenStreetMap (OSM)
Sumber 2 (Scraping): Portal Informasi Wisata Labuan Bajo
URL: https://ita.travel/destination/indonesia/labuan-bajo
Penerbit: ITA Travel Portal
2. Tanggal dan Jam Akses
Waktu Akses: 2026-11-15 pukul 15:21:00 WITA (Waktu Indonesia Tengah)
3. Metode Akuisisi
API (OpenStreetMap):
Endpoint: /api/interpreter
Parameter: Bounding Box [bbox: -8.55,119.83,-8.45,119.92] dengan filter tag ["tourism"] dan ["amenity"~"restaurant|cafe|fast_food|hotel|hostel|motel"].
Web Scraping:
Halaman Target: https://ita.travel/destination/indonesia/labuan-bajo
Selector: Menargetkan elemen penampung artikel perjalanan atau destinasi (div dengan nama kelas bertema card, destination, atau item). Dilengkapi dengan fallback mechanism lokal terstruktur guna menjamin keberlanjutan data jika server utama mengembalikan status HTTP 404.
4. Batasan Etika
Ketentuan API & robots.txt: Mematuhi aturan robot.txt OpenStreetMap dengan menyertakan header User-Agent identitas akademik yang jelas.
Jeda Waktu (Rate Limiting): Menerapkan penundaan (time.sleep(2)) sebelum pengiriman request untuk menghormati server target.
Lisensi:
Data OSM berlisensi ODbL (Open Database License) yang mewajibkan atribusi kepada kontributor.
Data wisata lokal digunakan murni untuk keperluan studi akademis non-komersial (Fair Use).
Data yang sengaja tidak diambil: Informasi pribadi pengelola penginapan, nomor telepon personal, atau data transaksi keuangan.
5. Penjelasan Kolom Dataset
A. openstreetmap_labuanbajo.csv (Fasilitas Wisata)
osm_id: ID unik objek di OpenStreetMap.
type: Tipe data spasial (node/way).
latitude: Koordinat lintang.
longitude: Koordinat bujur.
name: Nama fasilitas/amenitas.
amenity: Klasifikasi jenis amenitas (restoran, hotel, atraksi).
website: Website resmi fasilitas (jika ada).
opening_hours: Jam operasional.
B. scraping_labuanbajo.csv (Destinasi Wisata)
destination_id: Kode ID unik destinasi wisata.
destination_name: Nama destinasi pariwisata.
category: Kategori atraksi (Atraksi Alam atau Petualangan/Budaya).
location: Lokasi administratif daerah.
accessibility: Jenis akses menuju lokasi (akses boat, darat, dll).
source_url: URL sumber rujukan data.
6. Cara Menjalankan Ulang Notebook
Pastikan koneksi internet aktif.
Jalankan sel bagian 1. Persiapan Struktur Folder untuk membuat folder data/raw/ dan docs/.
Jalankan sel 2. Pengambilan Data Geospasial untuk mengunduh data pariwisata OSM.
Jalankan sel 3. Web Scraping untuk melakukan ekstraksi destinasi wisata.
Jalankan sel 4. Dokumentasi Kepatuhan Etika untuk memperbarui checklist etika.
Jalankan sel 5. Metadata Asal-Usul untuk merekam hash MD5 terbaru dari seluruh berkas.
