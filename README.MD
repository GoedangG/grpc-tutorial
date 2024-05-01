## MODUL 9

#### REFLECTION
1. What are the key differences between unary, server streaming, and bi-directional streaming RPC (Remote Procedure Call) methods, and in what scenarios would each be most suitable?
- Jawab:
> Unary RPC: Klien mengirim 1 permintaan, server merespons 1 respons. Cocok untuk operasi sederhana.

> Server Streaming RPC: Klien mengirim 1 permintaan, server merespons dengan aliran banyak respons. Cocok untuk mentransfer banyak data dari server ke klien secara bertahap.

> Bi-directional Streaming RPC: Klien dan server dapat mengirim dan menerima aliran data secara bersamaan. Cocok untuk komunikasi dua arah real-time atau transfer data besar dua arah.

2. What are the potential security considerations involved in implementing a gRPC service in Rust, particularly regarding authentication, authorization, and data encryption?
- Jawab:
Pertama pastikan koneksi antara client dan server terjamin aman dengan menggunakan TLS untuk mengenkripsi data saat transit. Kedua, kita perlu tahu pasti siapa yang mengakses layanan tersebut. Hal ini bisa dilakukan dengan memberikan token khusus pada client, seperti token JWT. Ketiga, kita harus pastikan bahwa pengguna hanya bisa melakukan hal yang diperbolehkan. Misalnya, jika seseorang adalah pengguna biasa, dia tidak bisa melakukan hal yang hanya bisa dilakukan oleh admin. Terakhir, pastikan semua data yang dikirim antara client dan server dienkripsi untuk menjaga kerahasiaan dan integritas data.

3. What are the potential challenges or issues that may arise when handling bidirectional streaming in Rust gRPC, especially in scenarios like chat applications?
- Jawab:
> Manajemen aliran data: Mengelola aliran data masuk dan keluar secara bersamaan dapat menjadi rumit. Perlu mengatur buffer dan mengontrol laju aliran untuk mencegah kelebihan beban.

> Penanganan kesalahan dan pemulihan: Perlu menangani kesalahan dan memulihkan koneksi saat terjadi gangguan jaringan. Memastikan konsistensi data saat terjadi kegagalan menjadi tantangan.

> Skalabilitas dan performa: Menjaga performa optimal saat jumlah koneksi tinggi. Memastikan skalabilitas horizontal untuk menangani beban besar.

4. What are the advantages and disadvantages of using the tokio_stream::wrappers::ReceiverStream for streaming responses in Rust gRPC services?
- Jawab:
##### advantage
> kemudahan dalam melakukan konversi dari Receiver menjadi Stream
> Kemudahan penggunaan dan integrasi dengan fitur dan alat lain dari tokio
##### disadvantage
> Tidak cocok untuk throughput yang tinggi
> Terlalu kompleks bagi developer yang tidak terbiasa dengan tokio



5. In what ways could the Rust gRPC code be structured to facilitate code reuse and modularity, promoting maintainability and extensibility over time?
- Jawab:
    1. pisahkan business logic dari implementasi gRPC.
    2. Gunakan Protobuf untuk mendefinisikan services dan Traits untuk abstraksi solid antara services dan implementasi konkretnya.
    3. Terapkan modularisasi kode dengan memisahkan fungsionalitas ke dalam modul terpisah.
    4. Manfaatkan generics dan traits untuk fungsi umum dan abstraksi interfaces.
    5. Terapkan dependency injection untuk memudahkan pengujian dan pembaruan komponen.
    6. Pastikan penanganan kesalahan yang konsisten di seluruh modul.
Dengan menerapkan pemisahan concerns, abstraksi yang baik, modularisasi, dan praktik terbaik seperti dependency injection serta penanganan kesalahan, proyek Rust gRPC akan menjadi lebih terstruktur, mudah dipelihara, dan reusable.

6. In the MyPaymentService implementation, what additional steps might be necessary to handle more complex payment processing logic?
- Jawab:
    1. Validasi data yang diterima dari client.
    2. Implementasi logika untuk proses pembayaran seperti total harga.
    3. Jika melibatkan pengiriman data yang berurutan, streaming gRPC perlu mengirim dan menerima data secara bertahap.

7. What impact does the adoption of gRPC as a communication protocol have on the overall architecture and design of distributed systems, particularly in terms of interoperability with other technologies and platforms?
- Jawab:
Penggunaan gRPC memungkinkan komunikasi antara layanan yang ditulis dalam bahasa pemrograman yang berbeda melalui protobuf. Ini memfasilitasi interoperabilitas antar platform dan teknologi, karena protokol komunikasi yang sama digunakan di seluruh sistem. Selain itu, gRPC dapat mempermudah integrasi dengan platform lain yang mendukung protobuf, seperti Android dan JavaScript, tanpa memerlukan penyesuaian yang rumit.

8. What are the advantages and disadvantages of using HTTP/2, the underlying protocol for gRPC, compared to HTTP/1.1 or HTTP/1.1 with WebSocket for REST APIs?
- Jawab:
##### Advantages
    1. Dukungan untuk multiplexing dan streaming data dalam dua arah, meningkatkan efisiensi dan responsivitas.
    2. Header compression mengurangi overhead jaringan dan mempercepat waktu muat halaman.
    3. Mendukung penggunaan Protocol Buffers untuk serialisasi data, menawarkan format data yang lebih efisien.
##### Disadvantages
    1. Lebih kompleks untuk diimplementasi daripada HTTP/1.1.
    2. Tidak semua server mendukungnya sepenuhnya.
    3. Kompatibilitas dengan perangkat atau browser lama mungkin terbatas.
    4. Fitur yang disediakan mungkin terlalu berlebihan untuk aplikasi sederhana.

9. How does the request-response model of REST APIs contrast with the bidirectional streaming capabilities of gRPC in terms of real-time communication and responsiveness?
- Jawab:
Model request-response dari REST APIs memungkinkan komunikasi unary, di mana client mengirim permintaan ke server dan menunggu respons dari server. Sementara itu, kemampuan bi-directional dari gRPC memungkinkan komunikasi real-time yang lebih responsif. Dengan gRPC, client dan server dapat mengirim dan menerima data secara langsung tanpa harus menunggu permintaan atau respons sebelumnya selesai, yang memungkinkan respons yang lebih cepat dan pengalaman pengguna yang lebih responsif dalam aplikasi real-time seperti chat dan call.

10. What are the implications of the schema-based approach of gRPC, using Protocol Buffers, compared to the more flexible, schema-less nature of JSON in REST API payloads?
- Jawab:
Pendekatan berbasis skema dari gRPC menggunakan Protocol Buffers menawarkan validasi data yang ketat, otomatisasi kode, dan kesesuaian yang kuat antara client dan server. Sementara itu, sifat yang lebih fleksibel dari JSON dalam REST API memungkinkan penanganan data yang lebih dinamis dan perubahan struktur tanpa perlu pembaruan skema atau kode. Pemilihan antara keduanya tergantung spesific needs masing-masing.