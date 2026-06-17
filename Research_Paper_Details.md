# Hireonix: An AI-Powered Comprehensive Technical Assessment and Interview Preparation Platform

## 1. Abstract
Hireonix is an advanced, full-stack technical assessment and interview preparation tracking platform designed to bridge the gap between academic learning and industry readiness. The platform provides a multi-tenant ecosystem where candidates can practice coding, take dynamically generated aptitude tests, analyze their resumes against industry ATS standards, and simulate mock interviews with an AI bot. The integration of modern web technologies and Generative AI ensures a personalized, real-time, and scalable learning experience.

---

## 2. Technology Stack & Architecture

The system is built on the **MERN** stack but modernized with Vite, Framer Motion, and AI API integrations.

### Frontend (Client Tier)
* **Core Framework:** React.js (Bootstrapped with Vite for high-performance HMR and optimized builds)
* **Styling & UI:** Tailwind CSS v4 (Modern utility-first CSS, utilizing dynamic `bg-linear-to-*` syntax), vanilla CSS for fundamental resets.
* **Animations:** Framer Motion (Delivering a premium, dynamic, and engaging UI with micro-interactions).
* **State Management:** React Context API (`AppContext` for Authentication/Global Theme, `ActivityContext` for Session Tracking).
* **Routing:** React Router DOM (With secure `<ProtectedRoute>` wrappers).
* **Data Visualization:** Recharts (For analytical testing trends, pie charts, and radar graphs).
* **Code Editor Integration:** `@monaco-editor/react` (Provides a VS Code-like coding environment natively in the browser).

### Backend (Server Tier)
* **Runtime Environment:** Node.js
* **Framework:** Express.js 
* **Authentication:** JSON Web Tokens (JWT) stored securely in `httpOnly` cookies over CORS.
* **CORS Handling:** Dynamic Regex-based Origin detection to allow secure local-host port drift and production environment validation.

### Database (Data Tier)
* **Database:** MongoDB (NoSQL)
* **ODM:** Mongoose 

### Third-Party API Integrations & AI
* **Generative AI:** Google Gemini API (`gemini-pro` model) used natively for two core modules: Resume Analysis and AI Mock Interviews.
* **Code Execution Sandbox:** Judge0 API (via RapidAPI) for secure, containerized Remote Code Execution (RCE) in multiple languages.
* **Dynamic Testing:** Open Trivia DB API for dynamic, non-repetitive aptitude question generation.
* **Email Service:** Brevo (SMTP) for sending OTPs and verification workflows.

### DevOps & Infrastructure
* **Containerization:** Docker (Multi-stage builds traversing `node:20-alpine` and `nginx:alpine`).
* **Environment Orchestration:** Docker Compose (Automated networking connecting the Vite client, Express server, and MongoDB container).

---

## 3. Core Modules & Methodology

### A. Intelligent Resume Analyzer (ATS Simulation)
* **Methodology:** The system allows users to select a target job role (e.g., Software Engineer, Data Scientist). The resume (simulated via file proxy) is passed alongside the target role to the **Gemini AI API**. 
* **Outcome:** The AI evaluates the inputs to generate a simulated Applicant Tracking System (ATS) score out of 100, assigns a grade, detects missing core skills logically required for the chosen role, and outputs highly actionable formatting and keyword suggestions.

### B. AI Interview Preparation Bot
* **Methodology:** Simulates a live chat with an industry expert. Candidates select a persona (HR, Frontend, Machine Learning, etc.). A curated session of 6 situational and technical questions is generated. 
* **AI Evaluation Pipeline:** After the user submits an answer, the text is securely passed to the Gemini API via an engineered prompt. Gemini evaluates the strictness, correctness, and thoroughness of the answer, returning an evaluated score (0-100) and specific conversational feedback. 

### C. Live Multi-Language Coding Test Platform
* **Methodology:** Implements the `Monaco Editor` to provide syntax highlighting and auto-completion.
* **Execution:** Candidates can write algorithms in JavaScript, Python, C++, Java, Ruby, or C. When "Run" is clicked, the source code is dispatched via REST to the **Judge0 API**, sandboxed, executed, and returned safely to the UI showing `stdout`, `stderr`, execution time, and memory limits.

### D. Dynamic Aptitude Test Generation
* **Methodology:** Replaces static test banks with an algorithmic query to the **Open Trivia API**. Each session dynamically fetches 10 unique, multiple-choice questions per specific difficulty and category (Mathematics, Computer Science, etc.), minimizing memorization bias. 
* **Mechanics:** Includes an active countdown timer constraint (10 minutes) and real-time mapping of skipped vs. answered states.

### E. Analytics Dashboard & Session Management
* **Methodology:** Utilizes dynamic `localStorage` isolated by multi-tenant authentication (`hireonix_activity_${userID}`). 
* **Analytics:** Aggregates unstructured activity data into a timeline, transforming it via algorithmic grouping into visual trends using **Recharts** (Bar charts for weekly activity, Radar charts for topic weaknesses, Pie charts for module engagement).

---

## 4. System Security & Quality of Life Features

1. **Robust Authentication:** OTP-based email verification paired with highly secured, cookie-based JWT sessions. 
2. **Persistent Night / Light Mode:** Controlled via the global context. Preferences are cached into the user's local instance so UI states persist beyond page refresh.
3. **Protected Routing:** Strict endpoint interception guarding private endpoints like `/test-results` or `/dashboard` from anonymous requests.
4. **Resilient Network Layer:** A dynamically generated, regex-based CORS bypass that eliminates standard frontend-backend port mismatching without compromising cross-site security.
