# BoardgameListingWebApp

## Description

**Board Game Database Full-Stack Web Application.**
This web application displays lists of board games and their reviews. While anyone can view the board game lists and reviews, they are required to log in to add/ edit the board games and their reviews. The 'users' have the authority to add board games to the list and add reviews, and the 'managers' have the authority to edit/ delete the reviews on top of the authorities of users.  

## Technologies

- Java
- Spring Boot
- Amazon Web Services(AWS) EC2
- Thymeleaf
- Thymeleaf Fragments
- HTML5
- CSS
- JavaScript
- Spring MVC
- JDBC
- H2 Database Engine (In-memory)
- JUnit test framework
- Spring Security
- Twitter Bootstrap
- Maven

## Features

- Full-Stack Application
- UI components created with Thymeleaf and styled with Twitter Bootstrap
- Authentication and authorization using Spring Security
  - Authentication by allowing the users to authenticate with a username and password
  - Authorization by granting different permissions based on the roles (non-members, users, and managers)
- Different roles (non-members, users, and managers) with varying levels of permissions
  - Non-members only can see the boardgame lists and reviews
  - Users can add board games and write reviews
  - Managers can edit and delete the reviews
- Deployed the application on AWS EC2
- JUnit test framework for unit testing
- Spring MVC best practices to segregate views, controllers, and database packages
- JDBC for database connectivity and interaction
- CRUD (Create, Read, Update, Delete) operations for managing data in the database
- Schema.sql file to customize the schema and input initial data
- Thymeleaf Fragments to reduce redundancy of repeating HTML elements (head, footer, navigation)

## How to Run

1. Clone the repository
2. Open the project in your IDE of choice
3. Run the application
4. To use initial user data, use the following credentials.
  - username: bugs    |     password: bunny (user role)
  - username: daffy   |     password: duck  (manager role)
5. You can also sign-up as a new user and customize your role to play with the application! 😊

## PLUGINS TO BE INSTALLED INSIDE JENKINS
1. Eclipse Temurin installer plugin
2. Maven Integration plugin
3. Sonar Quality Gates Plugin
4. SonarQube Scanner for Jenkins
5. Docker Pipeline, Docker plugin, docker-build-step, Docker Commons Plugin
6. Kubernetes CLI Plugin, Kubernetes plugin
7. AWS Credentials Plugin
8. Email Extension Template Plugin

## Add bellow crdentials in jenkins
1. mail	
2. docker-cred (Username with password)	
3. sonar-token (secret text)
4. k8s (Secret file)
5. aws-cred(AWS Credentials)

## Tools to be configured
1. JDK installations - JDK - jdk17
2. SonarQube Scanner installations - sonar-scanner - latest
3. Maven installations - maven3.6
4. Docker installations - docker - latest

## Global System Configurations
1. SonarQube installations
 - Name:sonar-server
 - Server URL: http://ec2-public-ip:9000
 - Server authentication token: sonaar-token

## Configure Email
* manage Jenkins –> configure system there under the E-mail Notification section configure the details Click on Apply and save.
* Click on Manage Jenkins–> credentials and add your mail username and generated password
* This is to just verify the mail configuration
* Now under the Extended E-mail Notification section configure the details as shown in the below images. Click on Apply and save.
