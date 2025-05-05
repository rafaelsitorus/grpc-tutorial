Reflection Module 8

1. Perbedaan metode Unary RPC: Unary RPC menggunakan satu permintaan dan satu tanggapan, mirip dengan API REST konvensional, dan cocok untuk tugas sederhana seperti verifikasi pengguna. Bi-directional streaming memungkinkan dua pihak bertukar pesan secara bersamaan tanpa menunggu respons, yang ideal untuk aplikasi chat atau sistem kolaborasi real-time. Hal ini terjadi karena server streaming mengirimkan satu permintaan dan menerima aliran respons berkelanjutan.

2. Pertimbangan keamanan gRPC: Saat menggunakan gRPC dalam Rust, kita harus mempertimbangkan beberapa elemen keamanan. Ini termasuk autentikasi klien dengan token JWT atau sertifikat TLS, enkripsi data dengan TLS untuk melindungi komunikasi dari penyadapan, dan sistem otorisasi untuk membatasi akses ke metode tertentu. Sementara mekanisme pengendalian kecepatan diperlukan untuk melindungi dari serangan DoS, validasi input juga penting untuk mencegah serangan injeksi.

3. Kendala streaming dua arah Dalam gRPC, streaming dua arah menghadapi masalah seperti menangani diskoneksi jaringan yang membutuhkan mekanisme reconnect yang solid, mengelola persaingan untuk mencegah kondisi persaingan saat memproses chat flow secara bersamaan, dan mengatur sumber daya yang tepat untuk menangani banyak koneksi klien tanpa mengganggu efisiensi sistem.

4. Penggunaan tokio_stream::wrappers oleh ReceiverStream dalam gRPC Rust: ReceiverStream memanfaatkan sistem kompetisi asinkron tokio, yang memungkinkan pemrosesan respons non-blocking, dan menawarkan cara yang menarik untuk menerapkan streaming respons di Rust. Tetapi, untuk menggunakannya, kita harus paham tentang manajemen channel dan potensi backpressure saat menangani banyak pesan.

5. Struktur kode gRPC Rust untuk modularitas: User dapat membuat kode gRPC Rust lebih modular dengan membagi layanan menjadi modul berbeda, menggunakan abstraksi untuk logika bisnis, dan menggunakan trait untuk interface yang konsisten. Metode ini meningkatkan penggunaan kembali komponen dan memudahkan pengujian unit sambil tetap fleksibel untuk perubahan protokol komunikasi di masa depan.

6. Kompleksitas MyPaymentService: Implementasi yang lebih kompleks dari MyPaymentService membutuhkan integrasi dengan sistem pembayaran eksternal, pengelolaan transaksi di database, mekanisme rollback untuk transaksi yang gagal, pengawasan audit yang menyeluruh, dan teknik caching untuk meningkatkan kinerja permintaan yang sering terjadi.

7. Dampak gRPC pada arsitektur: Adopsi gRPC mendorong pendekatan microservice yang terdefinisi dengan baik, memungkinkan komunikasi lintas platform yang efektif, dan menyediakan kontrak layanan yang jelas. Ini membuat adopsi gRPC berdampak pada arsitektur sistem. Alat seperti gRPC gateway yang menjembatani ke REST membuat komunikasi dengan teknologi lain lebih mudah, meskipun ada konsekuensi dari kompleksitas deployment yang lebih tinggi.

8. HTTP/2 versus HTTP/1.1: HTTP/2 yang digunakan gRPC memungkinkan multiplexing permintaan melalui satu koneksi, kompresi header, dan dukungan push server, yang menghasilkan latensi yang lebih rendah dibandingkan HTTP/1.1. Namun, HTTP/2 memiliki kesulitan debugging yang lebih besar dan dukungan infrastruktur yang lebih sedikit dibandingkan HTTP/1.1 yang lebih mapan.

9. Perbandingan gRPC dengan REST untuk komunikasi real-time: Model permintaan-respons REST bergantung pada polling atau teknik long-polling, sehingga tidak ideal untuk komunikasi real-time. Sebaliknya, streaming bi-direksi gRPC memungkinkan komunikasi asinkron dan respons instan tanpa biaya tambahan, menjadikannya lebih efisien untuk aplikasi seperti platform perdagangan atau game multipemain yang membutuhkan pembaruan real-time.

10. Protocl Buffers vs JSON: Meskipun Protocol Buffers membutuhkan definisi skema awal, pendekatan berbasis skema gRPC dengan Protocol Buffers menawarkan validasi tipe yang kuat, serialisasi yang efektif, dan ukuran payload yang lebih kecil dibandingkan dengan JSON yang lebih fleksibel dalam REST.

