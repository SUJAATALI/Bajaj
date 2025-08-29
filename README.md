# Bajaj SQL Challenge (Spring Boot App)

This project is a **Spring Boot application** built for the Bajaj Hiring Challenge.  
It automatically solves the assigned SQL problem on startup and submits the solution to the provided webhook.

---

## 📌 Problem Statement
- On app startup, the application:
  1. Sends a `POST` request to generate a webhook.
  2. Receives a `webhook` URL and `accessToken` (JWT).
  3. Solves an SQL problem (based on the last two digits of the registration number).
  4. Submits the **final SQL query** back to the webhook using JWT authentication.

---

## 📊 SQL Question (Even Reg No → Question 2)

### Problem:
For each employee, calculate the number of employees **younger** than them in the same department.  
Return:
- `EMP_ID`
- `FIRST_NAME`
- `LAST_NAME`
- `DEPARTMENT_NAME`
- `YOUNGER_EMPLOYEES_COUNT`

Order by `EMP_ID` in **descending** order.

### ✅ Final SQL Query:
```sql
SELECT 
    e1.EMP_ID,
    e1.FIRST_NAME,
    e1.LAST_NAME,
    d.DEPARTMENT_NAME,
    COUNT(e2.EMP_ID) AS YOUNGER_EMPLOYEES_COUNT
FROM EMPLOYEE e1
JOIN DEPARTMENT d 
    ON e1.DEPARTMENT = d.DEPARTMENT_ID
LEFT JOIN EMPLOYEE e2
    ON e1.DEPARTMENT = e2.DEPARTMENT
   AND e2.DOB > e1.DOB
GROUP BY 
    e1.EMP_ID, e1.FIRST_NAME, e1.LAST_NAME, d.DEPARTMENT_NAME
ORDER BY 
    e1.EMP_ID DESC;

Bajaj/
 ├── src/main/java/com/example/demo/
 │     ├── DemoApplication.java
 │     ├── WebhookInitializer.java
 │     └── AppConfig.java
 ├── src/main/resources/
 │     └── application.properties
 ├── pom.xml
 └── README.md

git clone https://github.com/SUJAATALI/Bajaj.git
cd Bajaj

