
# Restful Booker API Test Automation Framework

## 1. Executive Summary
This repository hosts a robust API test automation suite for the **Restful Booker Platform**. The project utilizes **Postman** for script development and **Newman** for command-line execution, integrated into a **GitHub Actions** CI/CD pipeline.

The framework validates the full booking lifecycle—including Authentication, Creation, Retrieval, Updates, and Deletion—ensuring backend stability through strict status code, response time, and JSON schema assertions.

**Author:** Oynndrila Singh Purkayestha
**Role:** QA Automation Engineer
**Tools:** Postman, Newman, GitHub Actions, JavaScript

---

## 2. Repository Artifacts & Traceability

| File Name | Description |
|:---|:---|
| **RestFul-API.postman_collection.json** | Core test script containing API requests, pre-request scripts, and test assertions. |
| **RestFul-API.postman_environment.json** | Configuration file managing environment variables (Base URL, Tokens, IDs). |


---

## 3. Test Scope & Coverage
The automation suite covers End-to-End (E2E) workflows:

### 3.1 Authentication
* **Endpoint:** \`POST /auth\`
* **Logic:** Generates a secure token which is programmatically extracted and stored in the \`{{token}}\` environment variable for subsequent protected requests (PUT/DELETE).

### 3.2 Booking Operations (CRUD)
1.  **Create Booking (POST):** Validates creation of new records with dynamic payloads. Assertions check for \`200 OK\` and capture the new \`bookingid\`.
2.  **Get Booking (GET):** Retrieves data using the stored \`{{bookingid}}\`. Validates data consistency between the Request and Response bodies.
3.  **Update Booking (PUT):** Modifies existing records using the Auth Token. Verifies data persistence.
4.  **Partial Update (PATCH):** Updates isolated fields (e.g., First Name) to test partial resource modification.
5.  **Delete Booking (DELETE):** Removes the record and performs a negative test verification to ensure the resource is \`404 Not Found\`.

---

## 4. Technical Implementation

### 4.1 Environment Chaining
Data is passed dynamically between requests using Postman Environment Variables to ensure test independence:
* \`{{url}}\`: Centralized Base URL configuration.
* \`{{token}}\`: Dynamic Authentication Token.
* \`{{bookingid}}\`: Runtime-generated ID for chaining CRUD operations.

### 4.2 Automated Assertions
Each request includes JavaScript-based tests verifying:
* **Status Codes:** 200, 201, 204, 404.
* **Performance:** Response time < 2000ms.
* **Data Integrity:** JSON body parsing and value matching.

---

## 5. Execution Guide

### 5.1 Manual Execution (GUI)
1.  Import both \`.json\` files into Postman.
2.  Select **RestFul-API** from the environment dropdown.
3.  Run the collection using the **Collection Runner**.

### 5.2 Command Line Execution (Newman)
To run tests headlessly (without GUI) and generate HTML reports:

\`\`\`bash
# Install Newman and Reporter
npm install -g newman
npm install -g newman-reporter-htmlextra

# Run Test Suite
newman run RestFul-API.postman_collection.json -e RestFul-API.postman_environment.json -r cli,htmlextra
\`\`\`

---

## 6. CI/CD Integration (GitHub Actions)
This repository is configured with a **Continuous Integration (CI)** pipeline.
* **Trigger:** Push to \`main\` branch.
* **Action:** Automatically installs Node.js, sets up Newman, runs the API test suite, and generates a test report artifact.
* **Workflow File:** Located at \`.github/workflows/postman-ci.yml\`.

---

## 7. Author
**Oynndrila Singh Purkayestha**


