# ⚡ Reviewify.ai — Enterprise-Grade AI-Powered Code Reviewer

<div align="center">

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![React](https://img.shields.io/badge/Frontend-React%2019%20%2B%20Vite-blue.svg)](https://react.dev/)
[![Node.js](https://img.shields.io/badge/Backend-Node.js%20%2B%20Express-green.svg)](https://nodejs.org/)
[![MongoDB](https://img.shields.io/badge/Database-MongoDB%20v6.0%2B-brightgreen.svg)](https://www.mongodb.com/)
[![Gemini API](https://img.shields.io/badge/AI%20Engine-Google%20Gemini%202.5-orange.svg)](https://ai.google.dev/)

**Reviewify.ai** is an advanced, interactive, and premium web application designed to perform static vulnerability scanning and code reviews on the fly. Powered by the **Google Gemini API** (`gemini-2.5-flash`) and equipped with a local JavaScript sandboxed runtime, Reviewify.ai allows developers to write, inspect, scan, and refactor code inside a single glassmorphic workspace.

[Key Features](#-key-features-and-capabilities) • [Architecture](#-project-architecture) • [Tech Stack](#-tech-stack) • [Installation](#-getting-started) • [API Documentation](#-api-specification) • [Deployment](#-deployment--configuration)

</div>

---

## 🎨 Key Features and Capabilities

*   **🔍 Real-Time Code Editor:** A fully integrated editor built using `react-simple-code-editor` and `prismjs` supporting syntax highlighting for multiple languages:
    *   JavaScript, Python, C++, Java, CSS, and HTML.
*   **🤖 Dual-Engine Error Detection:**
    *   *Programmatic Sandbox*: Runs Node.js codes locally inside a custom native `vm` execution sandbox to isolate and format real-time JavaScript compilation issues.
    *   *AI Compiler Simulator*: Detects syntax faults in other languages and produces high-fidelity console diagnostics.
*   **🖥️ Simulated VS Code Terminal:** Programmatic syntax error catcher (using a Node.js sandbox VM for JavaScript) and AI-simulated compiler output displayed in a classic dark terminal console.
*   **📈 Dynamic Quality Dashboard:**
    *   **Quality Score Gauge:** A beautiful SVG-based circular indicator presenting an automated score based on findings.
    *   **Issues Tab:** Highlights and categorizes scanned issues by severity (Critical ❌, Warnings ⚠️, Info/Safe ✔️).
    *   **Refactored Code:** Clean tab rendering optimized code suggestions with copy-to-clipboard access.
    *   **Raw Markdown:** Rich-text display of the full explanation from the AI reviewer.
*   **📁 File Upload Support:** Directly drag-and-drop or select scripts to import code, auto-detecting language formats.
*   **📚 Interactive Templates & Presets:** Loaded template bugs (e.g., Memory Leaks, Callback Hell, SQL Injection, Mutable Defaults, Out of Bounds, Resource Leaks) for immediate testing.
*   **💾 Review History & Logs:** Integrated review logs stored in a MongoDB database with a LocalStorage fallback to allow users to revisit, toggle, or clear past reviews.

---

## 🏗️ Project Architecture

Reviewify.ai decouples frontend interactions from code analysis through an optimized Express API layer:

```
[ Frontend Client ] 
        │
        ▼ (POST /ai/get-review)
[ Backend Express Controller ]
        │
        ├─► [ Local VM Sandbox ] ──► (Catches JavaScript runtime & syntax errors)
        │
        ├─► [ Gemini AI Engine ] ──► (Reviews patterns, scans security, formats fixes)
        │
        └─► [ MongoDB Instance ] ──► (Saves review output details & history log)
```

### Directory Structure

Below is the directory mapping of the project's source codebase:

*   **Backend Server Modules:**
    *   [server.js](file:///c:/Users/Paras/OneDrive/Pictures/Attachments/Desktop/Ai-code-reviwer/AI-Code-Reviewer/Backend/server.js) — Main entry point initiating database connections and hosting the Express application listener.
    *   [app.js](file:///c:/Users/Paras/OneDrive/Pictures/Attachments/Desktop/Ai-code-reviwer/AI-Code-Reviewer/Backend/src/app.js) — Express app configuration, Middleware definitions, and CORS configuration.
    *   [db.js](file:///c:/Users/Paras/OneDrive/Pictures/Attachments/Desktop/Ai-code-reviwer/AI-Code-Reviewer/Backend/src/db.js) — MongoDB client initialization using the native driver.
    *   [ai.routes.js](file:///c:/Users/Paras/OneDrive/Pictures/Attachments/Desktop/Ai-code-reviwer/AI-Code-Reviewer/Backend/src/routes/ai.routes.js) — Express routers mapping REST endpoints to controllers.
    *   [ai.controller.js](file:///c:/Users/Paras/OneDrive/Pictures/Attachments/Desktop/Ai-code-reviwer/AI-Code-Reviewer/Backend/src/controller/ai.controller.js) — Route controllers managing code reviews, history queries, VM sandboxing, and clear functions.
    *   [ai.service.js](file:///c:/Users/Paras/OneDrive/Pictures/Attachments/Desktop/Ai-code-reviwer/AI-Code-Reviewer/Backend/src/services/ai.service.js) — Generative AI Service configuring system prompts and interacting with the `@google/generative-ai` API SDK.
*   **Frontend Dashboard UI:**
    *   [App.jsx](file:///c:/Users/Paras/OneDrive/Pictures/Attachments/Desktop/Ai-code-reviwer/AI-Code-Reviewer/Frontend/src/App.jsx) — Main dashboard component rendering templates, code editor, history panel, quality gauges, and VS Code terminal simulator.
    *   [App.css](file:///c:/Users/Paras/OneDrive/Pictures/Attachments/Desktop/Ai-code-reviwer/AI-Code-Reviewer/Frontend/src/App.css) — Custom stylesheet providing premium glassmorphic properties, glowing tabs, and terminal font styles.
    *   [index.css](file:///c:/Users/Paras/OneDrive/Pictures/Attachments/Desktop/Ai-code-reviwer/AI-Code-Reviewer/Frontend/src/index.css) — Root layout setup, scrolling setups, and tailwind/custom configurations.
    *   [main.jsx](file:///c:/Users/Paras/OneDrive/Pictures/Attachments/Desktop/Ai-code-reviwer/AI-Code-Reviewer/Frontend/src/main.jsx) — Primary index runner rendering the App context.

---

## 🛠️ Tech Stack

| Tier | Component / Library | Purpose |
| :--- | :--- | :--- |
| **Frontend** | React 19 (Vite) | High-performance SPA view layer & routing |
| | Prism.js | Tokenizer rendering real-time editor syntax styles |
| | React Markdown | Formats complex AI responses containing tables and blocks |
| | Axios | Manages API communication and asynchronous fetches |
| **Backend** | Node.js (Express.js) | Server runtime supporting JSON payloads and API routing |
| | `@google/generative-ai` | Integrates with Google Gemini API models |
| | Node VM Subsystem | Executes JavaScript scripts inside clean sandbox contexts |
| | MongoDB Native Driver | Retains logs and query records in collection documents |

---

## 🚀 Getting Started

Follow these steps to set up and run a local instance of Reviewify.ai.

### Prerequisites
*   Node.js (v18.x or later recommended)
*   MongoDB (local instance or MongoDB Atlas connection URI)
*   Google Gemini API Key (obtain from [Google AI Studio](https://aistudio.google.com/))

### 1. Clone and Prepare the Workspace
```bash
git clone https://github.com/NoumanAhmed01/AI-Code-Reviewer.git
cd AI-Code-Reviewer/AI-Code-Reviewer
```

### 2. Configure and Boot the Backend

1. Navigate to the backend directory:
   ```bash
   cd Backend
   ```
2. Install all server dependencies:
   ```bash
   npm install
   ```
3. Set up environment configurations:
   Create a `.env` file based on the provided template:
   ```bash
   cp .env.example .env
   ```
   Edit `.env` to include your configuration variables:
   ```env
   PORT=3000
   MONGODB_URI=mongodb://localhost:27017/reviewify
   GOOGLE_GEMINI_KEY=your_google_gemini_api_key
   GEMINI_MODEL=gemini-2.5-flash
   ```
4. Run the backend server in development mode:
   ```bash
   npm run dev
   ```
   *The server will start running on `http://localhost:3000`.*

### 3. Configure and Launch the Frontend

1. Open a new terminal pane and navigate to the frontend directory:
   ```bash
   cd ../Frontend
   ```
2. Install client dependencies:
   ```bash
   npm install
   ```
3. Set up environment configurations:
   Create a `.env` file based on the provided template:
   ```bash
   cp .env.example .env
   ```
   Set the API URL variable:
   ```env
   VITE_API_URL=http://localhost:3000
   ```
4. Run the frontend development server:
   ```bash
   npm run dev
   ```
   *Open your browser and navigate to `http://localhost:5173`.*

---

## 🔌 API Specification

All endpoints are prefixed with the base `/ai` path.

### 1. Perform Code Review
*   **Endpoint:** `POST /ai/get-review`
*   **Headers:** `Content-Type: application/json`
*   **Request Body:**
    ```json
    {
      "code": "function checkUser(id) { const query = 'SELECT * FROM users WHERE id = ' + id; return db.execute(query); }",
      "language": "javascript"
    }
    ```
*   **Success Response (200 OK):**
    ```json
    {
      "review": "### ❌ Issues\n1. **SQL Injection Vulnerability**: Direct string interpolation...",
      "error": null
    }
    ```

### 2. Fetch Review Log History
*   **Endpoint:** `GET /ai/history`
*   **Success Response (200 OK):**
    ```json
    [
      {
        "id": "64c8d5a1b32f41a8a25c1b5a",
        "language": "javascript",
        "code": "function checkUser(id) { ... }",
        "review": "...",
        "error": null,
        "date": "10:35 PM - Jun 25"
      }
    ]
    ```

### 3. Delete All Logs
*   **Endpoint:** `DELETE /ai/history`
*   **Success Response (200 OK):**
    ```json
    {
      "message": "History cleared successfully"
    }
    ```

---

## 🔒 Security & VM Sandbox Mechanics

To catch compilation and reference bugs before shipping scripts to the AI Engine, Reviewify.ai incorporates a dual validation layer:
*   **Native VM Sandbox:** When a user requests review on a block of JavaScript code, the server passes it directly into the native Node.js `vm` core module:
    ```javascript
    const vm = require("vm");
    new vm.Script(code); // Throws SyntaxError on malformed structures
    ```
    This catches syntactical compilation faults locally inside an isolated thread context without exposing the server environment.
*   **AI Compiler Simulation:** In non-JS formats, system prompt boundaries force Gemini to identify reference issues and format them inside predefined tags (`[TERMINAL_ERROR] ... [/TERMINAL_ERROR]`). The controller intercepts these tags and maps them to the terminal console layout.

---

## 🌍 Deployment & Configuration

### Backend Deployment (Vercel, Render, or Railway)
Deploy the `Backend/` subdirectory. Ensure you set the following environment variables:
*   `MONGODB_URI` — Connection URI for database storage.
*   `GOOGLE_GEMINI_KEY` — API credentials key.
*   `GEMINI_MODEL` — Configured AI model version (defaults to `gemini-2.5-flash`).

### Frontend Deployment (Vercel or Netlify)
Deploy the `Frontend/` subdirectory. Set the build settings to:
*   **Build Command:** `npm run build`
*   **Output Directory:** `dist`
*   **Environment Variable:** `VITE_API_URL` pointing to your deployed backend URL.

---

## 🤝 Contributing

Contributions make the open-source community an amazing place to learn, inspire, and create. Any contributions you make are **greatly appreciated**.

1. Fork the Project
2. Create your Feature Branch (`git checkout -b feature/AmazingFeature`)
3. Commit your Changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the Branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

---

## 📜 License

Distributed under the MIT License. See [LICENSE](file:///c:/Users/Paras/OneDrive/Pictures/Attachments/Desktop/Ai-code-reviwer/LICENSE) for more information.

---
Developed with ❤️ by the Reviewify Team using Google Gemini & React.
