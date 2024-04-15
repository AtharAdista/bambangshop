# BambangShop Publisher App
Tutorial and Example for Advanced Programming 2024 - Faculty of Computer Science, Universitas Indonesia

---

## About this Project
In this repository, we have provided you a REST (REpresentational State Transfer) API project using Rocket web framework.

This project consists of four modules:
1.  `controller`: this module contains handler functions used to receive request and send responses.
    In Model-View-Controller (MVC) pattern, this is the Controller part.
2.  `model`: this module contains structs that serve as data containers.
    In MVC pattern, this is the Model part.
3.  `service`: this module contains structs with business logic methods.
    In MVC pattern, this is also the Model part.
4.  `repository`: this module contains structs that serve as databases and methods to access the databases.
    You can use methods of the struct to get list of objects, or operating an object (create, read, update, delete).

This repository provides a basic functionality that makes BambangShop work: ability to create, read, and delete `Product`s.
This repository already contains a functioning `Product` model, repository, service, and controllers that you can try right away.

As this is an Observer Design Pattern tutorial repository, you need to implement another feature: `Notification`.
This feature will notify creation, promotion, and deletion of a product, to external subscribers that are interested of a certain product type.
The subscribers are another Rocket instances, so the notification will be sent using HTTP POST request to each subscriber's `receive notification` address.

## API Documentations

You can download the Postman Collection JSON here: https://ristek.link/AdvProgWeek7Postman

After you download the Postman Collection, you can try the endpoints inside "BambangShop Publisher" folder.
This Postman collection also contains endpoints that you need to implement later on (the `Notification` feature).

Postman is an installable client that you can use to test web endpoints using HTTP request.
You can also make automated functional testing scripts for REST API projects using this client.
You can install Postman via this website: https://www.postman.com/downloads/

## How to Run in Development Environment
1.  Set up environment variables first by creating `.env` file.
    Here is the example of `.env` file:
    ```bash
    APP_INSTANCE_ROOT_URL="http://localhost:8000"
    ```
    Here are the details of each environment variable:
    | variable              | type   | description                                                |
    |-----------------------|--------|------------------------------------------------------------|
    | APP_INSTANCE_ROOT_URL | string | URL address where this publisher instance can be accessed. |
2.  Use `cargo run` to run this app.
    (You might want to use `cargo check` if you only need to verify your work without running the app.)

## Mandatory Checklists (Publisher)
-   [x] Clone https://gitlab.com/ichlaffterlalu/bambangshop to a new repository.
-   **STAGE 1: Implement models and repositories**
    -   [x] Commit: `Create Subscriber model struct.`
    -   [x] Commit: `Create Notification model struct.`
    -   [x] Commit: `Create Subscriber database and Subscriber repository struct skeleton.`
    -   [x] Commit: `Implement add function in Subscriber repository.`
    -   [x] Commit: `Implement list_all function in Subscriber repository.`
    -   [x] Commit: `Implement delete function in Subscriber repository.`
    -   [x] Write answers of your learning module's "Reflection Publisher-1" questions in this README.
-   **STAGE 2: Implement services and controllers**
    -   [x] Commit: `Create Notification service struct skeleton.`
    -   [x] Commit: `Implement subscribe function in Notification service.`
    -   [x] Commit: `Implement subscribe function in Notification controller.`
    -   [x] Commit: `Implement unsubscribe function in Notification service.`
    -   [x] Commit: `Implement unsubscribe function in Notification controller.`
    -   [x] Write answers of your learning module's "Reflection Publisher-2" questions in this README.
-   **STAGE 3: Implement notification mechanism**
    -   [x] Commit: `Implement update method in Subscriber model to send notification HTTP requests.`
    -   [x] Commit: `Implement notify function in Notification service to notify each Subscriber.`
    -   [x] Commit: `Implement publish function in Program service and Program controller.`
    -   [x] Commit: `Edit Product service methods to call notify after create/delete.`
    -   [x] Write answers of your learning module's "Reflection Publisher-3" questions in this README.

## Your Reflections
This is the place for you to write reflections:

### Mandatory (Publisher) Reflections

#### Reflection Publisher-1
1. Single Model struct sudah cukup dikarenakan pada case BambangShop Subscriber hanya terdiri dari satu tipe saja, Sedangkan interface diperlukan jika observer yang kita memiliki banyak variasi.

2. Dikarenakan id dan url unik, maka penerapan DashMap lebih disarankan karena dengan penerapan DashMap maka kita dapat lebih mudah dalam melakukan akses data dan manipulasi data dikarenakan pada DashMap kita dapat melakukan pengecekan apakah data kita unik atau tidak dengan mudah. Tidak seperti penggunaan vec yang lebih sulit bagi kita untuk mengetahui apakah data kita unik atau tidak, selain itu untuk akses data yang diinginkan, vec juga tidak seefisien DashMap karena pada DashMap kita dapat melakukan pemetaan antara key dan value sedangkan pada vec maka kita harus membuat vec 2 dimensi untuk menampung id dan url dan melakukan pengecekan satu-satu untuk mencari data yang diinginkan dan juga melakukan pengecekan satu-satu untuk mengetahui apakah id dan url unik.
   
3. Penggunaan DashMap diperlukan dikarenakan DashMap adalah struktur data yang dirancang khusus untuk konkurensi, sehingga menyediakan cara aman untuk menyimpan dan mengakses beberapa thread (thread safe). Penggunaan DashMap dapat membuat kita terhindari dari deadlock. Sedangkan singleton pattern digunakan untuk memastikan bahwa hanya ada satu instance di seleluruh aplikasi. Biasanya ini digunakan untuk membuat suatu objek global yang dapat diakses dari mana saja, tetapi dalam konteks thread-safe, singleton pattern mungkin saja mengalami masalah thread-safe. Dalam kasus ini penggunaan DashMap dalam SUBSCRIBER sudah benar karena DashMap dapat menjamin thread-safe.
   
#### Reflection Publisher-2
1. "Service" dan "Repository" perlu dipisah agar kita dapat memenuhi prinsip single responsibility, yang dimana sebuah kelas hanya melakukan tugas sesuai dengan kelasnya saja (hanya memiliki satu tanggung jawab). Dengan melakukan hal ini maka kode kita nantinya akan mudah untuk di maintain. Pada MVC asli, "Model" melakukan semua hal yang terkait dengan data, mulai dari business logics, validations, bahkan sampai operasi penyimpanan data. Dengan memisahkan business logic ke "Service" dan operasi penyimpanan data ke "Repository", "Model" hanya bertaggung jawab sebagai "representative" atau struktur dari sekumpulan data, sehingga kode kita akan lebih clean dan lebih mudah di maintain nantinya karena terjadi sebuah pemiasahan yang jelas antar tiap bagiannya.

2. Jika kita hanya menggunakan "Model" tanpa memisahkan ke "Service" dan "Repository maka "Model" melakukan semua hal yang terkait dengan data, mulai dari business logics, validations, bahkan sampai operasi penyimpanan data. Hal ini tentunya akan melanggar prinsip single responsibility, kode kita akan sulit di maintain, Kode kita juga akan meningkat complexitynya, kode kita fleksibilitasnya juga akan berkurang hal tersebut dikarenakan pemisahan antar bagian kurang jelas karena satu bagian melakukan banyak sekali hal yang berbeda. Misalnya jika kita menerapkan "Model" tanpa "Service" dan "Repository" pada (Program, Subscriber, Notification), maka "Model" akan melakukan banyak sekali hal yang berbeda mulai dari business logics, validations, bahkan sampai operasi penyimpanan data. Hal ini akan menyebabkan model menjadi sangat kompleks, kode akan saling terkait satu sama lain, sehingga jika melakukan perubahan atau penambahan fitur maka akan meningkatkan resiko terjadinya error karena keterkaitan satu sama lain yang sangat erat, keterkaitan ini akan membuat kode sulit untuk diperluas.

3. Postman dapat membantu kita dalam melakukan pengecekan API, postman membantu dalam membuat permintaan HTTP ke endpoint API, postman dapat kita gunakan untuk pengecekan "GET", "POST", "PUT", "DELETE", "PATCH", dll., serta menambahkan paramater, header, dan body ke permintaan tersebut. Postman dapat membantu kita dalam melakukan simulasi apa yang terjadi ketika kita mengirimkan respons ke endpoint kita di berbagai lingkungan, sehingga memungkinkan kita untuk menguji API kita dalam berbagai kondisi dan konfigurasi. Fitur postman yang menarik bagi saya adalah:
   
   - Pengecekan method "GET", "POST, "PUT", "DELETE", dll, memanfaatkan HTTP request, selain itu bahkan kita dapat menambahkan paramater, header, dan body ke request tersebut.
   - Membuat dokumentasi API berdasarkan API definition.
   - Simulasi di lingkungan yang berbeda sehingga memungkinkan kita untuk menguji API kita dalam berbagai kondisi dan konfigurasi.
   - Kita dapat membuat skrip pengujian otomatis untuk menguji endpoint API secara otomatis, sehingga kita dapat melakukan validasi fungsionalitas dengan cepat.


#### Reflection Publisher-3
1. Dalam tutorial kali ini kita menggunakan push model, hal ini dapat kita lihat di notification.rs. Jadi setiap kita melakukan update data product maka publisher akan melakukan push data (mengirimkan data langsung) ke para subscriber, dalam kasus ini maka notification suatu produk akan dikirim kepada subscriber yang berlangganan.

2. Jika kita lebih memilih menggunakan pull model, maka ada beberapa keuntungan yang kita dapatkan seperti subscriber akan memiliki kendali penuh kapan dan bagaimana data akan diambil, subscriber dapat hanya mengambil data kita diperlukan saja sehingga akan mengoptimalkan penggunaan sumber daya dan menghindari pembaruan yang tidak perlu, serta akan mengurangi beban publisher karena subscriber yang memiliki tanggung jawab untuk mengambil data ketika benar-benar diperlukan saja. Sementara itu, kerugian dari pull model adalah dapat menyebabkan overhead jaringan, terutama ketika subscriber sering meminta pembaruan data. Kerugian lainnya adalah kurang efisien karena data mungkin saja kurang real time dikarenakan dalam pull model subscriber harus aktif meminta pembaruan data dari publisher, sehingga subscriber mungkin tidak selalu mendapatkan data secara real time. Kerugian yang terakhir adalah penggunaan bandwith, model pull dapat menghabiskan bandwidth karena pengguna terus-menerus meminta pembaruan data, terutama jika ada banyak pengguna yang melakukan permintaan secara bersamaan. Hal ini dapat menyebabkan beban server yang tinggi.

3. Jika kita tidak memakai multi-thread dalam fitur notification maka data akan dikirim satu-persatu secara berurutan sehingga akan menyebabkan terjadinya keterlambatan pengiriman notifikasi dan kinerja aplikasi akan menjadi lambat terutama apabila terdapat banyak notifikasi yang perlu dikirim, selain itu ika jumlah notifikasi yang harus dikirim tiba-tiba meningkat secara signifikan, maka tanpa multi-threading, aplikasi mungkin tidak mampu menangani beban tersebut dengan efisien. Fitur notifikasi tanpa multi-thread juga akan dapat menyebabkan adanya resiko bottlenecks, di mana satu tugas yang memakan waktu lama dapat menghambat proses pengiriman notifikasi keseluruhan. Dengan menerapkan multi-thread maka kita akan dapat mengirimkan notifikasi secara paralel sehingga akan lebih efisien dan masalah-masalah diatas dapat dihindari.
