# Catatan Refleksi Commit 1

## Milestone 1: Server Web Single-Threaded

Pada Milestone 1, saya menerapkan server web single-threaded dasar yang dapat mendengarkan dan mencetak permintaan HTTP masuk.

### Komponen Utama

- **Setup Pendengar TCP**: Fungsi `TcpListener::bind` mendengarkan pada port tertentu (127.0.0.1:7878), sementara `listener.incoming()` menyediakan iterator atas upaya koneksi.

- **Penanganan Koneksi**: Di dalam fungsi `handle_connection`, saya menggunakan `BufReader` untuk membungkus `TcpStream`, yang memungkinkan pembacaan data masuk yang lebih efisien.

- **Parsing Permintaan**: Kode memanfaatkan pipeline iterasi fungsional—khususnya `lines()`, `map()`, dan `take_while()`—untuk mengekstrak baris permintaan hingga mencapai baris kosong yang menandakan akhir header HTTP. Proses ini secara efektif mengurai permintaan HTTP mentah menjadi kumpulan string yang dapat diperiksa di konsol.

### Hasil Pembelajaran

Mengumpulkan baris-baris ini ke dalam `Vec` dan mencetaknya membantu saya memvisualisasikan semua metadata yang dikirim browser saya ke server selama permintaan.
