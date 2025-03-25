**TEST CASES - Laravel REST API with PostgreSQL & Keycloak**

**Submitted By**  
Pravesh, Abhishek

**Submitted To**  
Vipin Tripathi  

**Test Case Version**  
1.0

**Reviewer Name**  
Manmeet Narang, Pooja Joshi

---

## **Goal**
The purpose of these test cases is to ensure that the Laravel REST API, integrated with PostgreSQL and Keycloak authentication, functions correctly, securely, and efficiently. The test cases focus on verifying API accessibility, database interactions, authentication, data validation, error handling, and overall system performance.

---

## **Table of Contents**

1. **Test Environment**  
2. **Test Cases**  
   - TC1: API Accessibility  
   - TC2: Database Connection  
   - TC3: User Registration  
   - TC4: User Login  
   - TC5: Fetch User Profile  
   - TC6: Save Data in Database  
   - TC7: Data Validation  
   - TC8: Frontend Integration  
   - TC9: Error Handling  

---

## **Test Environment**
- **Operating System:** Ubuntu (using Podman for containerization)
- **Backend Framework:** Laravel (PHP)
- **Database:** PostgreSQL
- **Authentication:** Keycloak
- **Server:** Laravel's built-in server Apache
- **Version Control:** Git
- **Logging & Debugging:** Laravel logs, PostgreSQL logs

---

### **TC1: API Accessibility**
**Scenario:** Ensure that the API is accessible and responding.  
**Remarks:** API routes must be correctly set in `routes/api.php`.

- **Given** the API server is running,
- **When** a user sends a request to an API endpoint,
- **Then** the server responds with a `200 OK` status.

**Test Run Date:**   
**Result:**   

---

### **TC2: Database Connection**
**Scenario:** Validate connection between Laravel and PostgreSQL.  
**Remarks:** Ensure correct `.env` configurations.

- **Given** the database details are correctly set in the `.env` file,
- **When** the Laravel app starts,
- **Then** it should connect to PostgreSQL successfully.

**Test Run Date:**   
**Result:**   

---

### **TC3: User Registration**
**Scenario:** A new user should be able to register via API.  
**Remarks:** Ensure email uniqueness and password encryption.

- **Given** a user provides valid registration details (name, email, password),
- **When** they send a `POST` request to `/api/register`,
- **Then** a new user is created, and the API returns `201 Created`.

**Test Run Date:**   
**Result:**   

---

### **TC4: User Login**
**Scenario:** A registered user should be able to log in.  
**Remarks:** Invalid credentials should return `401 Unauthorized`.

- **Given** a user provides valid login details (email, password).
- **When** they send a `POST` request to `/api/login`,
- **Then** the API returns an authentication token with `200 OK`.

**Test Run Date:**   
**Result:**   

---

### **TC5: Fetch User Profile**
**Scenario:** A logged-in user should fetch their profile details.  
**Remarks:** Unauthorized users should get a `401` error.

- **Given** the user is logged in,
- **When** they send a `GET` request to `/api/profile`,
- **Then** the API returns user details with `200 OK`.

**Test Run Date:**   
**Result:**   

---

### **TC6: Save Data in Database**
**Scenario:** Data should be correctly saved in PostgreSQL.  
**Remarks:** Verify if the database table updates properly.

- **Given** the user sends valid data via `POST` request,
- **When** the request reaches the API,
- **Then** the data is stored successfully.

**Test Run Date:**   
**Result:**   

---

### **TC7: Data Validation**
**Scenario:** The API should reject incorrect data.  
**Remarks:** Use Laravel’s built-in validation.

- **Given** the user submits incomplete or invalid data (Invalid email format, Weak or short password),
- **When** they send a request to the API,
- **Then** the API returns a `422 Unprocessable Entity` error.

**Test Run Date:**   
**Result:**   

---

### **TC8: Frontend Integration**
**Scenario:** The frontend should correctly display API data.  
**Remarks:** Ensure proper CORS settings.

- **Given** the frontend makes a valid API request (Fetching user profile (Get Request), Submitting a form (post request) Saving data in database (Post request),
- **When** the API responds,
- **Then** the frontend correctly displays the data.

**Test Run Date:**   
**Result:**   

---

### **TC9: Error Handling**
**Scenario:** API should return proper error messages.  
**Remarks:** Standardize error responses.

- **Given** an API request fails due to an issue,
- **When** an error occurs,
- **Then** the API returns a response with an error message.

**Test Run Date:**   
**Result:**   

---



