# Train Reservation System

### High-level design of Train Reservation System

![trainTicketArchitecture](https://user-images.githubusercontent.com/23628103/161523420-f93bdbc8-e8e7-45fc-ab91-73236da34fc9.png)

### Tech Stack

| #                                                                                                                                       | Name                     |
| --------------------------------------------------------------------------------------------------------------------------------------- | ------------------------ |
| <img src="https://th.bing.com/th/id/OIP.mbEpyJoKrhRxgM8hOEyCnwHaDl?pid=ImgDet&rs=1" width="30px" />                                     | Go                       |
| <img src="https://raw.githubusercontent.com/gin-gonic/logo/master/color.png" width="22px" height="25px" />                              | Gin-gonic                |
| <img src="https://jwt.io/img/pic_logo.svg" width="28px" />                                                                              | JWT                      |
| <img src="https://th.bing.com/th/id/OIP.opCGA6vB3-uK-wovJxHocQHaMB?pid=ImgDet&rs=1" width="25px" height="30px" />                       | Kafka                    |
| <img src="https://yt3.ggpht.com/-4DiTG0vtEW0/AAAAAAAAAAI/AAAAAAAAAAA/73kg_CNK54g/s900-c-k-no-mo-rj-c0xffffff/photo.jpg" width="40px" /> | Docker                   |
| <img src="https://th.bing.com/th/id/OIP.2DKX6fd0wlVbbjff_noWHgAAAA?pid=ImgDet&rs=1" width="30px" />                                     | Swagger                  |
| <img src="https://th.bing.com/th/id/OIP.4y0O4Ytk5MArYDVEKMahLQHaHa?pid=ImgDet&rs=1" width="30px" />                                     | MongoDB (Mongo-Atlas)          |
| <img src="https://th.bing.com/th/id/OIP.KWTSipv0th6chxVeD_oWhwHaCD?pid=ImgDet&rs=1" width="55px" />                                     | Sonarqube                |
| <img src="https://hostbillapp.com/appstore/payment_razorpay/images/logo.png" width="55px" />                                            | RazorPay Payment Gateway |

### User Service

Service that directly interacts with client and used for creating, updating, deleting users.
PORT - 8081
APIs: `/login`, `/signup`, `/getUserDetails`, `/user`
(delete method)

Producing greeting messages at the time of successful registration to `kafka` which is consumed by `email service`.

### Train Service

This service also directly interact with client. Client can search for train routes from source to destination station code on specific time and do booking.
PORT - 8082
APIs: `/book`, `/search`

### Payment Service

This service also directly interact with client. Client can pay for their tickets that links with
PORT - 8083
APIs: `/book`, `/search`

### Email Service

service continously consuming kafka messages of topic-"email" and sends email to given receiver email and content.

### Invoice Service

service used to generated invoice of paid tickets for user which sends details to email service.

### Logging Service

service used to store all the logs generated by other services in mongoDB according to log level in different collection of `log` database.

### Database Service

service that stores data in MongoDB after consuming the details from kafka.

### Kafka Brokers

- `topic` : email | `host` : localhost:9091
- `topic` : invoice | `host` : localhost:9092
- `topic` : error, info, debug, warn | `host` : localhost:9093
- `topic` : pay | `host` : localhost:9094
