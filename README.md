# foody-documentation

Foody is an online food delivery system.

## System Architecture

![Screenshot](./resources/SOA.png?raw=true)

### Core Services

* **Account Service** :- Account service is the oauth service that is responsible for issuing the authentication token to users in the system based on the clients. Authentication will be done using OTP flow.

* **Customer Management System** :- Customer management system is responsible for managing the information of the customer(phone number, profile, addresses etc)

* **Rider Management System** :- Rider management system is responsible for managing the information of the delivery executives(phone number, profile, is active to take order for delivery, current location of delivery executives etc)

* **Merchant Management System** :- Merchant management system is responsible for managing the information of merchants(phone number, email, profile etc)

* **OTP Service** :- OTP Service is responsible for generating, managing and sending the OTP SMS through Notification service.

* **Notification Service** :- Notification service is resposible for send out push and sms notification to the users.

* **Catalog System** :- Catalog system is responsible to managing the restaurant and product catalog.

* **Order Management System** :- Order management system is responsible for managing cart, order and order payments. Once the order is placed, OMS sends event to kafka topic to notify Delivery management system.

* **Coupon Management System** :- Coupon management system is responsible for managing and providing coupons for flat and percentage discount on restaurants with some constraints.

* **Delivery Management System** :- Delivery management system is responsible for assigning a rider to an order.

### Infrastructure System

* **Kubernetes** :- We will be using kuberenetes for deploying and managing services since it is easy to configure, manage and scale services. We will be using Kubernetes configMaps and secrets to provide configuration settings to applications. 

* **Nginx** :- Nginx is a open source web server that will be using for routing the request to specific service based on host and path, Rate limiting, Authenticating token using Account service. We will be using kubernetes nginx ingress controller, since it's easy to manage, configure using yamls annotations.

* **StackDriver** :- We will be using google stackdriver to collect and alert on metrics exposed from services. Services will expose metric in prometheus style fashion. Each service pod will run stackdriver-prometheus-sidecar to extract metric from metric endpoint and push it to stackdriver. Some of the metrics being expose are :- Number of request based on status codes, service and url path, Response time of request based on status codes, service and url path etc.

* **Jaeger** :- Jaeger is open source distributed tracing system that will help us to monitor and troubleshoot the system. Each service is instrumented with Jaeger to provide the system trace. The Jaeger trace ID will be send to the client as request id and the logger(foody-common) is also instrumented to log trace ID, span ID, user ID, app ID and user role.

* **Databases** :- We will be using MongoDB and MySQL as our persistent datastore in most of the services. We will be using Redis in OTP and Rider management system(to store riders geo location).

* **Kafka** :- We will be using Kafka to interact asynchronously between services. For eg: we will be using kafka for sending notifications, for sending order events from OMS to delivery management system.

## Progress

- [x] account-service(Unit Test cases pending)
- [x] customer-management-system(In progress)
- [ ] rider-management-service
- [ ] merchant-management-system
- [ ] otp-service
- [ ] notification-service
- [x] catalog-service (with some UT test cases)
- [ ] order-management-system
- [ ] coupon-management-system
- [ ] delivery-management-system

