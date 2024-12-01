Full Stack Web Application
Full stack development refers to the process of building web applications that include both client-side (front-end) and server-side (back-end) components.

Detailing structure of Application:
ReactJS Frontend
Java SpringBoot backend
MySQL RDBMS
The Outline of this Project Includes:
Architecture Diagram
Flow Diagram
Installing Prerequisites
Setup, Build, and Manual Deployment of the Application
Daemonizing the Services
Dockerizing the Application
Creating a Docker Compose File and Running the Application
Architecture Diagram
Flow Diagram
                      [ User Action ]
                                |
                                |
                      [ ReactJS Frontend ]
                                |  HTTP Request
                                |
                    [ Java Spring Boot Backend ]
   
                                |   Database Query
                                |
                         [ MySQL Database ]
                                |    Data Response
                                |
                     [ Java Spring Boot Backend ]
                                |  HTTP Response
                                |
                         [ ReactJS Frontend ]
                                |
                                |
                             [ UI Update ]
Installing Prerequisites
Following toolset/package to be installed

Java 17
Maven 3.8.8
NodeJs 14.x
MySQL 8.x
Setup, Build, and Manual Deployment of the Application
Backup- setup,Build and Run the application
Frontend- setup Build and Run the application
Daemonizing the Services
Create SystemD Service for java backend
Daemon Reload & systemctl the Service
Create SystemD Service for react frontend
Daemon Reload & systemctl the Service
Dockerizing the Application
Create a Dockerfile for Frontend
create a Dockerfile for backend
Create a Dockerfile for MySQL
Creating a Docker Compose File
Create a dockercompose file using above Dockerfile of each service and run the application automatically.
