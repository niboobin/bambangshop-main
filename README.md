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
    -   [ ] Commit: `Implement update method in Subscriber model to send notification HTTP requests.`
    -   [ ] Commit: `Implement notify function in Notification service to notify each Subscriber.`
    -   [ ] Commit: `Implement publish function in Program service and Program controller.`
    -   [ ] Commit: `Edit Product service methods to call notify after create/delete.`
    -   [ ] Write answers of your learning module's "Reflection Publisher-3" questions in this README.

## Your Reflections
This is the place for you to write reflections:

### Mandatory (Publisher) Reflections

#### Reflection Publisher-1
1. Observer pattern and interfaces: In the Observer pattern, the interface is used to define a contract for the Observer (Subscriber). This allows the Subject (Publisher) to communicate with any object that implements this interface, making the system more flexible and extensible. A single Model struct is enough, but using an interface would make it easier to add different types of Observers in the future.

2. Vec vs DashMap for uniqueness: If uniqueness is a requirement for `id` in Program and `url` in Subscriber, a map/dictionary like DashMap would be more suitable than a Vec. This is because checking for uniqueness in a Vec requires iterating over the entire list (O(n) complexity), while in a map/dictionary, this can be done in constant time (O(1) complexity).

3. DashMap vs Singleton for thread safety: The Singleton pattern ensures that a class has only one instance and provides a global point of access to it. However, it doesn't inherently provide thread safety. DashMap, on the other hand, is a concurrent HashMap that is designed to be thread-safe. If you need to access and modify the List of Subscribers from multiple threads, using DashMap would be a better choice.
#### Reflection Publisher-2
1. Separation of `Service` and `Repository` from a Model: In the context of software design, separating concerns into different components can make the system more organized, easier to maintain, and more scalable. The `Repository` is typically responsible for data access logic, while the `Service` contains business logic. By separating these from the `Model`, you can change the data storage mechanism or business rules without affecting the other parts of the system. This separation also makes it easier to test each component independently.

2. Interactions between each model affecting code complexity: If we only use the Model and put all the logic (data access, business rules, etc.) in it, the Model can become bloated and difficult to maintain. For example, if the `Program`, `Subscriber`, and `Notification` models all contain their own data access and business logic, changes in one model could potentially affect the others. This tightly coupled design can lead to higher code complexity and make the system more prone to errors.

3. Exploration of Postman: `Postman` is a powerful tool for testing APIs. It allows you to send requests to an API and view the responses. These features can be very helpful in both group projects and future software engineering projects, as they can speed up the process of testing and debugging APIs.

#### Reflection Publisher-3
