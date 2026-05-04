# Modul 8 High-Level Networking

## Reflection
### 1. What are the key differences between unary, server streaming, and bi-directional streaming RPC (Remote Procedure Call) methods, and in what scenarios would each be most suitable?

Unary RPC paling sederhana diantara ketiganya di mana client mengirim satu request dan menerima satu response. Ini cocok untuk operasi CRUD sederhana. Pada server streaming RPC, client mengirim satu request dan dapat menerima banyak response, cocok untuk notifikasi atau daya berukuran besar yang dipecah menjadi beberapa bagian kecil. Pada bi-directional streaming RPC, client dan server dapat mengirim banyak response secara simultan, cocok untuk aplikasi real-time seperti chat.

### 2. What are the potential security considerations involved in implementing a gRPC service in Rust, particularly regarding authentication, authorization, and data encryption?

Aspek keamanan penting meliputi authentication (misalnya menggunakan token JWT atau TLS client certificate), authorization (membatasi akses berdasarkan role/permission), serta data encryption (menggunakan TLS/HTTPS karena gRPC berjalan di atas HTTP/2); selain itu, perlu juga memperhatikan validasi input, proteksi terhadap replay attack, dan pengamanan metadata yang dikirim dalam request.

### 3. What are the potential challenges or issues that may arise when handling bidirectional streaming in Rust gRPC, especially in scenarios like chat applications?

Tantangannya adalah manajemen concurrency karena banyak stream berjalan bersamaan, sinkronisasi data, serta potensi memory leak jika stream tidak ditutup dengan benar.

### 4. What are the advantages and disadvantages of using the tokio_stream::wrappers::ReceiverStream for streaming responses in Rust gRPC services?

Penggunaan `tokio_stream::wrappers::ReceiverStream` memudahkan integrasi antara channel async dengan dtream grpc sehingga kita bisa mengirim data secara async dengan mudah dan fleksibel. Kekurangannya adalah ada potensi overhead tambahan dan bisa ada bottleneck jika channel tidak dikelola dengan baik.

### 5. In what ways could the Rust gRPC code be structured to facilitate code reuse and modularity, promoting maintainability and extensibility over time?

Untuk meningkatkan modularitas dan reuse, code dapat dipisahkan menjadi beberapa layer seperti service, bussines logic, dan repository.

### 6. In the MyPaymentService implementation, what additional steps might be necessary to handle more complex payment processing logic?

Untuk menangani pembayaran yg lebih kompleks, perlu ditambahkan validasi transaksi, integrasi dengan payment gateway eksternal, logging, dan notifikasi status pembayaran.

### 7. What impact does the adoption of gRPC as a communication protocol have on the overall architecture and design of distributed systems, particularly in terms of interoperability with other technologies and platforms?

Pengunaan gRPC membuat desaign lebih efisien dan strongly typed melalui penggunaan protocol buffers. Tapi interoperabilitas dengan sistem lain bisa terjadi kendala jika teknologi tidak mendukung gRPC, sehingga diperlukan gateway untuk lintas platform.

### 8. What are the advantages and disadvantages of using HTTP/2, the underlying protocol for gRPC, compared to HTTP/1.1 or HTTP/1.1 with WebSocket for REST APIs?

HTTP/2 bisa multiplexing (banyak request dalam satu koneksi), header compression, dan performa yg lebih baik dibandingkan HTTP/1.1. Dibandingkan websocket, HTTP/2 lebih terstruktur dan cocok untuk gRPC. Namun, websocket lebih fleksibel untuk komunikasi event-driven sederhana. Kekurangannya HTTP/2 lebih kompleks.

### 9. How does the request-response model of REST APIs contrast with the bidirectional streaming capabilities of gRPC in terms of real-time communication and responsiveness?

Model request-response di rest API bersifat stateless dan biasanya tidak real time karena tiap interaksi harus dimulai oleh client. Sedangkan gRPC dengan bidirectional lebih responsif dan efisien untuk aplikasi real time.

### 10. What are the implications of the schema-based approach of gRPC, using Protocol Buffers, compared to the more flexible, schema-less nature of JSON in REST API payloads?

Keuntungan pendekatan schema-based pada gRPC dengan protocol buffers adalah validasi tipe yang ketat, ukuran payload lebih kecil, dan performa lebih tinggi dibandingkan JSON. Namun, ini mengurangi fleksibilitas karena perubahan skema harus dikelola dengan hati-hati, beda dengan JSON di REST API yang lebih bebas dan mudah diubah tapi rentan overhead ukuran data.