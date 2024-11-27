# Springboot_Application

# Student Management System

This is a **Spring Boot** application for managing student information. It allows users to register, log in, and update their details while preventing duplicate accounts with the same email. The application is designed to demonstrate basic user management functionality.

---

## Features

1. **User Registration**
   - Allows users to register with unique email addresses.
   - Prevents multiple accounts with the same email.

2. **User Login**
   - Authenticate users for secure access.

3. **CRUD Operations**
   - Retrieve user details.
   - Update user information.

4. **Database**
   - In-memory H2 database for data storage.

---

## Technologies Used

- **Spring Boot** (Java-based application framework)
- **Spring Data JPA** (Persistence API)
- **H2 Database** (Lightweight, in-memory database for testing)
- **Maven** (Build automation tool)

---


## Endpoints
| Method | Endpoint          | Description              |
|--------|-------------------|--------------------------|
| POST   | /api/users/register | Register a new user      |
| GET    | /api/users/{id}     | Get user information     |
| PUT    | /api/users/{id}     | Update user information  |

## Deployment
The application is deployed using Jenkins CI/CD pipeline to AWS EC2.

## Jenkinsfile
pipeline {
    agent any
    stages {
       stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/SanviBhelkar/Springboot_Application.git'
            }
        }
        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }
        stage('Deploy to AWS') {
            steps {
                sh '''
                scp -i /Downloads/key1.pem target/student-management-system.jar ec2-user@ec2-3-105-85-107.ap-west-1.compute.amazonaws.com:/home/ec2-user/
                ssh -i /Downloads/key1.pem ec2-user@ec2-3-105-85-107.ap-west-1.compute.amazonaws.com "java -jar /home/ec2-user/student-management-system.jar"
                '''
            }
        }
    }
}



### Instructions
1. Clone the repository.
2. Configure AWS EC2 and Jenkins.
3. Deploy using the Jenkinsfile provided.

-**Set up Project Structure**
curl https://start.spring.io/starter.zip -d dependencies=web,data-jpa,h2,security -d name=student-management-system -o student-management-system.zip
unzip student-management-system.zip
cd student-management-system

-**Deploy EC2**
**Upload JAR file to EC2**
scp -i /Downloads/key1.pem target/student-management.jar eec2-user@ec2-3-105-85-107.ap-west-1.compute.amazonaws.com:/home/ec2-user/

**SSH into EC2 and run the JAR file**
ssh -i /Downloads/key1.pem ec2-user@ec2-3-105-85-107.ap-west-1.compute.amazonaws.com "java -jar /home/ec2-user/student-management.jar"

### Prerequisites

- Java 17 or later
- Maven 3.8 or later
- Any IDE (e.g., IntelliJ IDEA, Eclipse, VS Code)

