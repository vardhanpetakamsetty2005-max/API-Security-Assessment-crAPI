# 🔐 API Security Assessment — crAPI

A hands-on API security testing project focused on identifying and understanding common API security weaknesses using **crAPI (Completely Ridiculous API)** and **Burp Suite**.

This repository contains testing notes, HTTP request and response screenshots, security observations, and recommendations for improving API security.

---

## 📌 Table of Contents

- [Project Overview](#-project-overview)
- [Objectives](#-objectives)
- [Tools and Technologies](#️-tools-and-technologies)
- [Testing Methodology](#-testing-methodology)
- [Security Testing Scenarios](#-security-testing-scenarios)
- [Screenshots and Evidence](#-screenshots-and-evidence)
- [Security Recommendations](#️-security-recommendations)
- [Learning Outcomes](#-learning-outcomes)
- [Scope and Responsible Testing](#️-scope-and-responsible-testing)
- [About Me](#-about-me)

---

## 📖 Project Overview

APIs allow applications to exchange data and perform operations. However, improper authorization, weak authentication controls, and excessive data exposure can create security risks.

The purpose of this project is to practice API security testing in the intentionally vulnerable crAPI lab environment. Using Burp Suite, API requests and responses are inspected to understand application behavior and investigate selected security scenarios.

The project documents the testing process through screenshots and provides recommendations for strengthening API security.

## 🎯 Objectives

- Understand API communication through HTTP requests and responses.
- Learn how to intercept and analyze API traffic.
- Investigate Broken Object Level Authorization (BOLA).
- Examine API responses for excessive data exposure.
- Explore authentication and OTP-related security controls.
- Understand account takeover attack scenarios.
- Investigate Server-Side Request Forgery (SSRF).
- Document test evidence and practical security recommendations.

## 🛠️ Tools and Technologies

| Tool / Technology | Purpose |
|---|---|
| **crAPI** | Intentionally vulnerable application for API security practice |
| **Burp Suite** | Intercepting, inspecting, and modifying HTTP requests and responses |
| **HTTP / REST APIs** | Understanding API endpoints, methods, headers, and responses |
| **Web browser** | Accessing the lab application and testing workflows |
| **Terminal** | Supporting lab setup and command-line tasks, where applicable |

## 🔬 Testing Methodology

The project follows a structured API testing workflow:

1. **Application exploration:** Identify relevant application features and API endpoints.
2. **Request interception:** Capture HTTP requests using Burp Suite.
3. **Request analysis:** Inspect methods, paths, parameters, headers, and response data.
4. **Authorization testing:** Examine whether users can access resources they are permitted to access.
5. **Authentication testing:** Explore OTP-related and account access workflows.
6. **Input and request testing:** Investigate the application's handling of selected request values and destinations.
7. **Evidence collection:** Capture relevant requests and responses for documentation.
8. **Recommendations:** Identify appropriate security controls based on the observed behavior.

---

## 🔍 Security Testing Scenarios

### 1. API Request and Response Analysis

**Objective:** Understand how API endpoints process requests and return data.

**Testing activities:**
- Inspect HTTP methods, endpoints, headers, and parameters.
- Review status codes and response bodies.
- Compare request changes with the resulting application behavior.

**Security benefit:** Helps identify unusual behavior, improper validation, and potentially sensitive information in responses.

### 2. Broken Object Level Authorization (BOLA)

**Objective:** Investigate whether the application properly checks access to individual resources.

**Testing activities:**
- Examine requests containing resource identifiers.
- Compare application behavior when authorized test resources are requested.
- Determine whether server-side ownership and permission checks are enforced.

**Potential impact:** Inadequate object-level authorization can expose or allow unauthorized modification of another user's resources.

**Recommendation:** Validate the authenticated user's permissions for every requested object on the server side.

### 3. Excessive Data Exposure

**Objective:** Examine whether API responses contain more information than the client needs.

**Testing activities:**
- Inspect response bodies and returned fields.
- Identify information that may not be required for the requested operation.
- Assess whether sensitive fields are appropriately protected.

**Potential impact:** Unnecessary information in responses can increase the risk of personal or account-related data exposure.

**Recommendation:** Return only necessary fields and apply appropriate authorization and data filtering.

### 4. Authorization Testing — Other Vehicle

**Objective:** Examine whether resource access controls are consistently enforced across different vehicle or object identifiers.

**Testing activities:**
- Review requests involving vehicle or resource identifiers.
- Compare responses for resources available to the test account.
- Assess whether access restrictions are applied consistently.

**Recommendation:** Enforce resource ownership and authorization checks independently of client-supplied identifiers.

### 5. OTP Security Testing

**Objective:** Explore OTP-related authentication controls.

**Security controls to assess:**
- OTP expiration and single-use enforcement.
- Verification attempt limits.
- Rate limiting against repeated requests.
- Server-side validation of OTPs.
- Protection against unauthorized account recovery.

**Potential impact:** Weak OTP controls may increase the risk of authentication abuse or unauthorized account access.

**Recommendation:** Enforce expiration, single-use codes, attempt limits, and server-side verification.

### 6. Account Takeover Testing

**Objective:** Examine an account-related attack scenario and assess the application's authentication protections.

**Security controls to assess:**
- Account recovery validation.
- Authentication and session handling.
- Rate limiting and abuse detection.
- Notifications for suspicious account activity.

**Potential impact:** Weak account protection can allow unauthorized access if authentication or recovery controls can be bypassed.

**Recommendation:** Strengthen account recovery, protect sessions, limit repeated attempts, and monitor suspicious authentication activity.

### 7. Server-Side Request Forgery (SSRF)

**Objective:** Investigate how the application handles user-controlled URLs or server-side requests.

**Security controls to assess:**
- URL and destination validation.
- Restrictions on internal network access.
- Protection of cloud metadata endpoints.
- Outbound network restrictions.
- Redirect and DNS resolution handling.

**Potential impact:** An SSRF vulnerability may allow a server to make unintended requests to internal services or other restricted destinations.

**Recommendation:** Use strict destination allowlists, validate resolved IP addresses, block sensitive internal destinations, and restrict outbound connections.

> **Note:** These sections describe the testing scenarios and potential risks. A vulnerability should be marked as confirmed only when the collected evidence demonstrates that the security control failed.

---

## 📸 Screenshots and Evidence

The `evidence/` directory contains screenshots documenting the API testing process. Each image should show relevant testing activity without exposing credentials, session tokens, OTPs, or personal information.

### 1. User Request and Response

**Purpose:** Document the initial API request and the corresponding response.

![User 1 Request](evidence/01_User1_Request.png)

![User 1 Response](evidence/02_User1_Response.png)

### 2. Broken Object Level Authorization (BOLA)

**Purpose:** Document requests and responses examined during object-level authorization testing.

![BOLA Request](evidence/03_BOLA_Request.png)

![BOLA Response](evidence/04_BOLA_Response.png)

### 3. Excessive Data Exposure

**Purpose:** Record API response data reviewed for potentially unnecessary or sensitive fields.

![Data Exposure Request](evidence/05_Data_Exposure_Request.png)

![Data Exposure Response](evidence/06_Data_Exposure_Response.png)

![Additional Data Exposure Evidence](evidence/07_Data_Exposure_Additional_Response.png)

### 4. Authorization Testing — Other Vehicle

**Purpose:** Document the request and response associated with testing access to another vehicle or resource.

![Other Vehicle Request](evidence/08_BOLA_Other_Vehicle_Request.png)

![Other Vehicle Response](evidence/09_BOLA_Other_Vehicle_Response.png)

### 5. OTP Security Testing

**Purpose:** Document the OTP-related test scenario and the application's observed behavior.

![OTP Testing Evidence](evidence/10_OTP_Testing_Redacted.png)

### 6. Account Takeover Testing

**Purpose:** Record evidence associated with the account security testing scenario.

![Account Takeover Evidence](evidence/11_Account_Takeover_Evidence.png)

### 7. Server-Side Request Forgery (SSRF)

**Purpose:** Document the request and response examined during SSRF-related testing.

![SSRF Request](evidence/12_SSRF_Request.png)

![SSRF Response](evidence/13_SSRF_Response.png)

---

## 🛡️ Security Recommendations

Based on the types of API risks investigated in this project, recommended defensive practices include:

- **Authorization:** Verify resource ownership and permissions on every relevant request.
- **Authentication:** Use secure authentication, session management, and account recovery controls.
- **OTP protection:** Enforce expiration, single-use verification codes, and rate limits.
- **Data minimization:** Return only the information required by the client.
- **Input validation:** Validate untrusted input on the server side.
- **SSRF prevention:** Restrict outbound requests and block access to sensitive internal services.
- **Monitoring:** Log relevant security events without storing secrets or unnecessary personal data.
- **Retesting:** Verify that security controls work correctly after remediation.

## 📚 Learning Outcomes

Through this project, I developed practical familiarity with:

- API request and response analysis.
- Burp Suite for intercepting and examining HTTP traffic.
- Object-level authorization testing concepts.
- Authentication and OTP security considerations.
- Identifying potential excessive data exposure.
- Understanding SSRF risks and defensive controls.
- Organizing screenshots as security evidence.
- Writing clear security observations and remediation recommendations.

## ⚖️ Scope and Responsible Testing

This project is intended for educational purposes and authorized testing in the crAPI lab environment.

All testing should be limited to systems for which explicit permission has been granted. Credentials, OTPs, bearer tokens, cookies, personal information, and other sensitive data must be removed from screenshots before publication.

The documented scenarios should not be interpreted as confirmed vulnerabilities unless supported by the actual test results.

---

## 👨‍💻 About Me

Hi, I'm **Vardhan Petakamsetty**, an aspiring Cybersecurity professional passionate about ethical hacking, API security, vulnerability assessment, and penetration testing.

This project helped me gain practical experience with:

- API Security Testing
- Burp Suite for HTTP Request and Response Analysis
- Broken Object Level Authorization (BOLA) Testing
- Authentication and Authorization Testing
- Identifying Potential Data Exposure
- Security Evidence Documentation and Remediation Recommendations

I'm continuously improving my cybersecurity skills by building hands-on security projects and exploring application security, cloud security, and identity and access management (IAM).

⭐ If you found this project useful, consider giving it a star!

---

*This repository is a learning project documenting API security testing concepts, evidence, and defensive recommendations.*
