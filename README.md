# Web Security Final Project – OWASP Juice Shop

## 📌 Project Overview
This repository contains the final project for the **Web Security** course.  
The project is based on **OWASP Juice Shop** and focuses on adding and documenting a **new security challenge** that demonstrates a real-world vulnerability.

---

## 🧩 Added Challenge: Race Condition Login Lock

### Category
Broken Authentication

### Difficulty
★★★★☆

### Description
This challenge demonstrates a **Race Condition vulnerability** in the login mechanism.  
By sending multiple login requests concurrently, it is possible to bypass the account lockout mechanism that should activate after several failed login attempts.

---

## 🎯 Challenge Goal
Trigger a race condition to bypass the account lockout after too many failed login attempts.

The challenge appears under the "Broken Authentication" category:

![Challenge in Juice Shop](https://github.com/Azrieli-College-of-Engineering/final-project-shahd-nammari/blob/main/juice-shop/screenshots/race-challenge-list.png)
---

## 🧠 Vulnerability Explanation
The vulnerability is caused by an **unsynchronized access** to a shared in-memory counter that tracks failed login attempts per user.

When multiple login requests are processed at the same time:
- Each request reads the same counter value
- Updates are overwritten (lost update)
- The lockout condition is never reached

This behavior allows an attacker to continue attempting logins indefinitely.

---

## 🛠 Implementation Details
The challenge was implemented by modifying the login flow:
- Introducing a small asynchronous delay
- Allowing concurrent requests to interleave
- Detecting a race condition when the counter changes unexpectedly
- Solving the challenge automatically when the race is triggered

---

## 🧪 Proof of Concept (POC)
The challenge can be solved by:
1. Sending many concurrent login requests with incorrect credentials
2. Triggering overlapping execution on the server
3. Bypassing the intended login lock mechanism
4- The attack was performed against a local Juice Shop instance.
   
When successful, Juice Shop displays:
> ✅ *You have successfully solved a challenge: Race Condition Login Lock*

![race-challenge-solved](https://github.com/Azrieli-College-of-Engineering/final-project-shahd-nammari/blob/main/juice-shop/screenshots/race-condition-solved.png)
---

## 🔐 Mitigation & Fix
To prevent this vulnerability:
- Use atomic operations or database-level locking
- Synchronize access to shared state
- Implement rate limiting per user/IP
- Avoid in-memory counters for security-critical logic

---

## 🚀 How to Run the Project
```bash
cd juice-shop
npm install
npm run serve
```

---

## Then open
``` http://localhost:3000 ```

---


## 📂 Repository Structure
```
juice-shop/
├── routes/login.ts        # Vulnerable login logic
├── data/static/challenges.yml
├── models/challenge.ts
├── config/fbctf.yml
```

---

## 📚 Technologies Used
- Node.js
- Express
- TypeScript
- OWASP Juice Shop
- SQLite


[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-22041afd0340ce965d47ae6ef1cefeee28c7c493a6346c4f15d667ab976d596c.svg)](https://classroom.github.com/a/Nt4zUlkt)
