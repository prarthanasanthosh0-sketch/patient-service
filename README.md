🏥 Secure Patient Service Backend

This project is a secure Spring Boot microservice that manages patient data with:

🔐 Keycloak Authentication

👤 Role-Based Access Control (RBAC)

🌐 HTTPS (TLS)

🔒 AES Encryption for sensitive data

⚙️ Jenkins CI/CD pipeline

📦 GitHub integration

The goal of this project is to demonstrate enterprise-level backend security implementation.

📌 Project Features

This system provides:

Feature	Description
Authentication	Managed using Keycloak
Authorization	Role-based API access control
HTTPS	Secure TLS communication
AES Encryption	Protects patient data in database
Jenkins CI/CD	Automatic project build pipeline
GitHub	Version control integration
🏗️ Technology Stack
Technology	Purpose
Spring Boot	Backend framework
Keycloak	Authentication & authorization
MySQL	Database
AES	Data encryption
HTTPS (TLS)	Secure communication
Jenkins	CI/CD automation
GitHub	Source control
🔐 Security Architecture

The application includes three security layers:

1️⃣ Authentication

Handled using Keycloak

Users must log in before accessing APIs.

2️⃣ Authorization (RBAC)

Two roles exist:

Role	Permission
viewer	Can GET patient data
editor	Can GET + POST patient data

Example:

viewer → allowed → GET /patients
viewer → blocked → POST /patients

editor → allowed → POST /patients
3️⃣ Data Encryption

Sensitive fields encrypted before saving:

name
disease

Stored encrypted in database using AES algorithm

Returned decrypted in API responses.

Example stored value:

vs6vI4D2M4J9WQ/wiwZJ/A==
🌐 HTTPS Configuration

The application runs securely using TLS:

https://localhost:8443

Steps implemented:

Generated keystore file

Configured Spring Boot SSL

Enabled HTTPS port 8443

This ensures secure communication between client and server.

👤 Keycloak Setup

Realm created:

healthcare

Client created:

patient-api

Users:

testuser
editoruser

Roles:

viewer
editor

Role mapping:

testuser → viewer
editoruser → editor
🔑 Token Generation Example

Keycloak token endpoint:

http://localhost:9090/realms/healthcare/protocol/openid-connect/token

POST request body:

grant_type=password
client_id=patient-api
username=testuser
password=1234

Returned:

access_token

Used in API requests:

Authorization: Bearer <token>
📡 API Endpoints

Base URL:

https://localhost:8443/patients
GET all patients
GET /patients

Role required:

viewer OR editor
GET patient by ID
GET /patients/{id}

Role required:

viewer OR editor
CREATE patient
POST /patients

Example request:

{
  "name": "Prarthana",
  "disease": "Fever"
}

Role required:

editor
🔒 AES Encryption Implementation

Before saving:

name → encrypted
disease → encrypted

Before returning response:

name → decrypted
disease → decrypted

Implemented using:

AESUtil.java

Encryption flow:

Request → Encrypt → Save DB
Response → Decrypt → Return JSON
⚙️ Jenkins CI/CD Pipeline

Jenkins automates project build from GitHub.

Pipeline steps:

Pull project from repository

Execute Maven build

Generate executable JAR

Verify build success

Command used:

mvn clean install

Build result:

BUILD SUCCESS
📦 GitHub Repository

Project hosted at:

https://github.com/prarthanasanthosh0-sketch/patient-service

Contains:

src/
pom.xml
application.properties
keystore.p12
AESUtil.java
SecurityConfig.java
PatientController.java
🗄️ Database Security

Stored values are encrypted.

Example:

Field	Stored Value
name	encrypted
disease	encrypted

Returned values:

decrypted automatically
▶️ How To Run Project
Step 1

Start Keycloak:

http://localhost:9090
Step 2

Run Spring Boot:

mvn spring-boot:run
Step 3

Access API securely:

https://localhost:8443/patients
Step 4

Generate token using Postman

Use:

access_token

for authorization header

🧪 Testing Using Postman

Add header:

Authorization: Bearer <access_token>

Test:

GET /patients
POST /patients

Verify role restrictions.

📊 Project Workflow
Client
   ↓
Keycloak Authentication
   ↓
Role Validation (RBAC)
   ↓
Spring Boot API
   ↓
AES Encryption
   ↓
Database Storage
🎯 Learning Outcomes

This project demonstrates:

✔ Secure authentication using Keycloak
✔ Role-based authorization
✔ HTTPS communication
✔ AES encryption for sensitive data
✔ CI/CD automation using Jenkins
✔ GitHub integration


Secure Patient Service Backend Project
Spring Boot + Keycloak + AES + HTTPS + Jenkins CI/CD 🚀
