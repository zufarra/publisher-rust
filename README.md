# Reflection Tutorial Modul 9

**Zufar Romli Amri**  
**NPM**: 2306202694  
**Kelas**: A

---

### a. How much data your publisher program will send to the message broker in one run?

**Jawab:**

Program publisher yang ditunjukkan akan mengirimkan lima (5) data dalam satu kali eksekusi program. Hal ini terlihat dari adanya lima pemanggilan fungsi publish_event yang masing-masing mengirimkan sebuah pesan bertipe UserCreatedEventMessage. Setiap pesan berisi dua field data yaitu user_id (berupa string berisi angka dari "1" hingga "5") dan user_name (berupa string yang memuat NPM "2306202694" diikuti dengan nama yang berbeda, yaitu "Amir", "Budi", "Cica", "Dira", dan "Emir"). Kelima pesan ini dikirimkan ke antrian yang diberi nama "user_created" di message broker AMQP. Jumlah data yang dikirim secara spesifik bergantung pada ukuran serialisasi Borsh dari struktur UserCreatedEventMessage untuk masing-masing pesan, namun secara fungsional program ini mengirimkan lima entitas data pesan ke broker.

---

### b. The url of: “amqp://guest:guest@localhost:5672” is the same as in the subscriber program, what does it mean?

**Jawab:**

URL "amqp://guest:guest@localhost:5672" yang sama pada program publisher dan subscriber menunjukkan bahwa kedua program tersebut terhubung ke server message broker AMQP yang sama. Kesamaan URL ini mengindikasikan bahwa kedua program berkomunikasi melalui broker pesan yang identik, yang berada pada mesin lokal (localhost) dan port 5672, dengan menggunakan kredensial autentikasi yang sama (username: guest, password: guest). Hal ini memungkinkan terjadinya komunikasi asinkron antara publisher dan subscriber, di mana publisher mengirimkan pesan ke antrian "user_created" pada broker, dan subscriber menerima pesan dari antrian yang sama. Dengan demikian, keduanya tidak perlu berkomunikasi secara langsung atau mengetahui keberadaan satu sama lain, tetapi hanya perlu mengetahui detail koneksi ke broker pesan yang menjadi perantara komunikasi mereka, menciptakan arsitektur yang loosely coupled dan tangguh.

---

## Running RabbitMQ as Message Broker

![/running-RabbitMQ](./images/running-RabbitMQ.jpg)

---

## Sending and Processing Event

![/run-publisher](./images/run-publisher.jpg)

![/run-subscriber](./images/run-subscriber.jpg)

Pada kedua gambar di atas, kita dapat melihat komunikasi antara publisher dan subscriber dengan memanfaatkan RabbitMQ untuk melihat koneksinya. Pada gambar pertama, publisher akan mengirimkan 5 data ke message broker ketika command cargo run dijalankan (jika terdapat subscriber yang memiliki koneksi dengan publisher). Nantinya, pesan tersebut akan diproses dan diterima oleh subscriber, seperti yang ada pada gambar kedua.