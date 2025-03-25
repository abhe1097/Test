# Approach Paper - Laravel API with PostgreSQL & Keycloak

## Table of Contents

1. [Objective](#1-objective)
2. [Proposed Solution](#2-proposed-solution)
   - [Approach: Laravel API with Keycloak Authentication](#approach-laravel-api-with-keycloak-authentication)
   - [Architecture Diagram](#21-architecture-diagram)
   - [Description](#22-description)
   - [Implementation Steps](#23-implementation-steps)
   - [Pre-requisites](#24-pre-requisites)

## 1. Objective

The goal of this project is to develop a RESTful API using PHP Laravel, with PostgreSQL as the database and Keycloak for authentication and authorization. This API will support CRUD (Create, Read, Update, Delete) operations and will be deployed using Podman on Ubuntu terminal.

## 2. Proposed Solution

### Approach: Laravel API with Keycloak Authentication

### 2.1. Architecture Diagram

![Project Diagram](images/arcjitecture_diagram.png)

### 2.2. Description

#### Solution:
- The client sends a CRUD request to the API.
- Laravel API processes the request and verifies the authentication token with Keycloak.
- If the token is valid, the API performs CRUD operations on PostgreSQL and returns the response.
- If the token is invalid, the API returns an error message.

#### Pros:
- Secure authentication with Keycloak
- Scalable due to microservices architecture
- Easy deployment with Podman containers

#### Cons:
- Complex initial setup due to multiple integrations
- Requires additional resources to manage Keycloak

### 2.3. Implementation Steps

1. **Set Up Laravel Project**
   - Install Laravel on the Ubuntu server.
   - Configure PostgreSQL as the database in the `.env` file.

2. **Set Up Keycloak for Authentication**
   - Deploy Keycloak server and configure clients, and roles.
   - Integrate Laravel with Keycloak using OAuth2/OpenID Connect.
   - Implement token validation in middleware to secure API endpoints.

3. **Develop API Endpoints**
   - Define routes in `routes/api.php` for CRUD operations.
   - Implement controllers for handling requests.
   - Use Eloquent models for database interactions.

4. **Perform CRUD Operations**
   - Allow authenticated users to perform create, read, update, and delete operations.
   - Implement validation and error handling.

5. **Testing & Deployment**
   - Test API functionality using Postman.
   - Deploy the API on an Ubuntu server.
   - Use logs to monitor performance and issues.

### 2.4. Pre-requisites

#### Hardware Requirements
- Minimum 4GB RAM
- Multi-core processor
- At least 20GB storage

#### Software Requirements
- **Operating System:** Ubuntu 22.04 LTS
- **Web Framework:** Laravel 10
- **Database:** PostgreSQL 15
- **Authentication Server:** Keycloak 21
- **Containerization:** Podman
- **PHP Version:** 8.1+

#### Networking Requirements
- Secure API endpoints with HTTPS
- Open ports for PostgreSQL, Keycloak, and API server
- Secure communication between services


