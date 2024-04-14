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
    -   [ ] Commit: `Create Notification service struct skeleton.`
    -   [ ] Commit: `Implement subscribe function in Notification service.`
    -   [ ] Commit: `Implement subscribe function in Notification controller.`
    -   [ ] Commit: `Implement unsubscribe function in Notification service.`
    -   [ ] Commit: `Implement unsubscribe function in Notification controller.`
    -   [ ] Write answers of your learning module's "Reflection Publisher-2" questions in this README.
-   **STAGE 3: Implement notification mechanism**
    -   [ ] Commit: `Implement update method in Subscriber model to send notification HTTP requests.`
    -   [ ] Commit: `Implement notify function in Notification service to notify each Subscriber.`
    -   [ ] Commit: `Implement publish function in Program service and Program controller.`
    -   [ ] Commit: `Edit Product service methods to call notify after create/delete.`
    -   [ ] Write answers of your learning module's "Reflection Publisher-3" questions in this README.

## Your Reflections
This is the place for you to write reflections:

### Mandatory (Publisher) Reflections

#### Reflection Publisher-1
1. Single Model struct sudah cukup dikarenakan pada case BambangShop Subscriber hanya terdiri dari satu tipe saja, Sedangkan interface diperlukan jika observer yang kita memiliki banyak variasi.

2. Dikarenakan id dan url unik, maka penerapan DashMap lebih disarankan karena dengan penerapan DashMap maka kita dapat lebih mudah dalam melakukan akses data dan manipulasi data dikarenakan pada DashMap kita dapat melakukan pengecekan apakah data kita unik atau tidak dengan mudah. Tidak seperti penggunaan vec yang lebih sulit bagi kita untuk mengetahui apakah data kita unik atau tidak, selain itu untuk akses data yang diinginkan, vec juga tidak seefisien DashMap karena pada DashMap kita dapat melakukan pemetaan antara key dan value sedangkan pada vec maka kita harus membuat vec 2 dimensi untuk menampung id dan url dan melakukan pengecekan satu-satu untuk mencari data yang diinginkan dan juga melakukan pengecekan satu-satu untuk mengetahui apakah id dan url unik.
   
3. Penggunaan DashMap diperlukan dikarenakan DashMap adalah struktur data yang dirancang khusus untuk konkurensi, sehingga menyediakan cara aman untuk menyimpan dan mengakses beberapa thread (thread safe). Penggunaan DashMap dapat membuat kita terhindari dari deadlock. Sedangkan singleton pattern digunakan untuk memastikan bahwa hanya ada satu instance di seleluruh aplikasi. Biasanya ini digunakan untuk membuat suatu objek global yang dapat diakses dari mana saja, tetapi dalam konteks thread-safe, singleton pattern mungkin saja mengalami masalah thread-safe. Dalam kasus ini penggunaan DashMap dalam SUBSCRIBER sudah benar karena DashMap dapat menjamin thread-safe.
#### Reflection Publisher-2

#### Reflection Publisher-3
