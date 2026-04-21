# Catatan Refleksi Commit 1

## Milestone 1: Server Web Single-Threaded

Pada Milestone 1, saya menerapkan server web single-threaded dasar yang dapat mendengarkan dan mencetak permintaan HTTP masuk.

### Komponen Utama

- **Setup Pendengar TCP**: Fungsi `TcpListener::bind` mendengarkan pada port tertentu (127.0.0.1:7878), sementara `listener.incoming()` menyediakan iterator atas upaya koneksi.

- **Penanganan Koneksi**: Di dalam fungsi `handle_connection`, saya menggunakan `BufReader` untuk membungkus `TcpStream`, yang memungkinkan pembacaan data masuk yang lebih efisien.

- **Parsing Permintaan**: Kode memanfaatkan pipeline iterasi fungsional—khususnya `lines()`, `map()`, dan `take_while()`—untuk mengekstrak baris permintaan hingga mencapai baris kosong yang menandakan akhir header HTTP. Proses ini secara efektif mengurai permintaan HTTP mentah menjadi kumpulan string yang dapat diperiksa di konsol.

### Hasil Pembelajaran

Mengumpulkan baris-baris ini ke dalam `Vec` dan mencetaknya membantu saya memvisualisasikan semua metadata yang dikirim browser saya ke server selama permintaan.

# Catatan Refleksi Commit 2

## Milestone 2: Mengirim File HTML sebagai Respons HTTP

Pada Milestone 2, saya mempelajari cara mengirimkan konten file HTML sebagai respons dari server web ke browser.

### Komponen Utama

- **Membaca File HTML**: Saya menggunakan fungsi `fs::read_to_string` untuk membaca isi file `hello.html` menjadi string yang kemudian dikirimkan ke klien.

- **Menyusun Respons HTTP**: Struktur respons HTTP harus mengikuti format yang tepat, yaitu _status line_ (`HTTP/1.1 200 OK`), header, dan body.

- **Header `Content-Length`**: Header ini penting untuk memberi tahu browser ukuran data (dalam byte) yang akan diterima. Jika nilainya tidak sesuai ukuran konten sebenarnya, browser bisa gagal menampilkan halaman dengan benar atau terus menunggu data tambahan.

- **Menggabungkan Respons dengan `format!`**: Dengan makro `format!`, saya menyatukan _status line_, header, dan isi file HTML menjadi satu string respons utuh sebelum dikirim melalui `stream.write_all`.

### Hasil Pembelajaran

Saya memahami bahwa ketepatan format respons HTTP sangat berpengaruh pada keberhasilan browser dalam merender halaman yang dikirim server.

### Dokumentasi Commit 2

![Dokumentasi Commit 2](commit2.png)
