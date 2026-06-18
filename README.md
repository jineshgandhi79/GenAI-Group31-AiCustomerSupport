# 🚀 AI Customer Support & RAG Knowledge Base

A production-ready, full-stack AI Customer Support system featuring **Retrieval-Augmented Generation (RAG)**, automated human ticket escalation, real-time analytics dashboards, and an interactive feedback loop. 

🔗 **Deployed Web App:** [https://ai-customer-support-ten-delta.vercel.app/](https://ai-customer-support-ten-delta.vercel.app/)

---

## 🛠️ Technology Stack

| Layer | Technologies Used |
|---|---|
| **Frontend** | React 19 (Vite), React Router 7, Axios, Lucide React, CSS (Vanilla) |
| **Backend** | Node.js, Express.js, JWT Authentication, Helmet, Express Rate Limit, Multer, PDF Parse |
| **Database** | MongoDB Atlas (via Mongoose), Qdrant Cloud (Vector Database) |
| **Generative AI** | Google Gemini API (`gemini-3.5-flash` for completions/completions classification, `text-embedding-004` for vectors) |

---

## ✨ Features

- 🤖 **Interactive Support Chatbot**: Provides contextual replies to customer questions with conversation memory tracking.
- 📚 **RAG Knowledge Base**: Admin-facing document ingestion portal supporting PDF uploads, Markdown imports, and recursive URL crawling. Content is automatically chunked, embedded, and stored in Qdrant.
- 🎫 **Auto-Escalation Engine**: Automatically escalates tickets to human support when query confidence falls below a preset threshold or the inquiry is categorized as out-of-scope.
- 📊 **Real-time Analytics Dashboard**: Tracks query volumes, customer satisfaction rates, top unresolved questions, and classification metrics.
- 🔐 **Secure Role-based Control**: JWT-based access separation between standard Users (customer workspace) and Admins (dashboards and knowledge configuration).
- 📝 **Feedback Loop**: Native user feedback mechanisms (thumbs-up/thumbs-down ratings) on chatbot messages to audit response quality.

---

## 📐 Architecture

```
                                  +-------------------+
                                  |   Client App      |
                                  |   (React/Vite)    |
                                  +---------+---------+
                                            |
                                 HTTP REST  | JWT Auth
                                 Requests   v
                                  +---------+---------+
                                  |   Express Backend |
                                  +----+----+----+----+
                                       |    |    |
                    Mongoose Connection |    |    | Gemini Embeddings & Completions
                                        v    |    v
                            +----------+--+ | +--+--------------+
                            | MongoDB Atlas | | | Google Gemini  |
                            | (Users, Chats | | | (Flash, Text   |
                            | Feedback, etc)| | | Embedding-004) |
                            +-------------+ | +-----------------+
                                          | |
                     Qdrant REST Channels | |
                                          v v
                                  +-------+-----------+
                                  |   Qdrant Vector   |
                                  |   Database Cloud  |
                                  +-------------------+
```

---

## 📂 Project Structure

```
AI Customer Support/
├── backend/                       # Express API Server
│   ├── src/
│   │   ├── config/                # Db & Qdrant setups
│   │   ├── middleware/            # Auth guards, rate limiting, error handlers
│   │   ├── models/                # Mongoose Database Models
│   │   ├── modules/               # Feature controllers and route handlers
│   │   ├── services/              # Gemini completions, Qdrant vectors & parser services
│   │   ├── utils/                 # General utils (ticket generators)
│   │   ├── app.js
│   │   └── server.js
│   ├── scripts/                   # Verification and PDF testing scripts
│   ├── uploads/                   # Temporary directory for file uploads
│   ├── .env.example
│   ├── package.json
│   ├── README.md                  # Backend details
│   └── REST_API_DOCS.md           # API Reference Guide
├── frontend/                      # React SPA
│   ├── src/
│   │   ├── components/            # Header, layout components, and router guards
│   │   ├── context/               # Auth status management
│   │   ├── pages/                 # UI pages (Chat, Analytics, Escalations, Feedback, Ingestion)
│   │   ├── App.jsx
│   │   ├── index.css              # Custom styling definitions
│   │   └── main.jsx
│   ├── public/                    # Icon assets
│   ├── package.json
│   └── vite.config.js
└── CONTRIBUTORS.MD                # Team work division tracker
```

---

## 🔑 Demo & Test Credentials

For quick verification of both the live application and local development instances, the database includes two predefined accounts. Run the seed script (`node seedUsers.js` in the backend folder) to populate them:

- **Admin Account:**
  - **Email:** `test_admin@support.com`
  - **Password:** `admin_password_123`
- **Standard User Account:**
  - **Email:** `test_user@support.com`
  - **Password:** `user_password_123`

---

## 🚀 Setup & Local Execution

### 1. Clone & Pre-requisites
Make sure you have [Node.js (v18+)](https://nodejs.org/) installed. Clone the repository and navigate into the project workspace:
```bash
git clone <repository-url>
cd "AI Customer Support"
```

### 2. Backend Installation & Setup
1. Navigate to the `backend` folder:
   ```bash
   cd backend
   ```
2. Install package dependencies:
   ```bash
   npm install
   ```
3. Initialize the environment configuration file:
   ```bash
   copy .env.example .env
   ```
4. Configure the parameters inside your `.env` file with your credentials (e.g. MongoDB Atlas Connection URI, Google Gemini API Key, and Qdrant Cloud credentials).
5. Seed the database with the test users:
   ```bash
   node seedUsers.js
   ```
6. Start the Express development server:
   ```bash
   npm run dev
   ```
   *The server runs locally at: `http://localhost:5000`*

### 3. Frontend Installation & Setup
1. Open a new terminal window and navigate to the `frontend` folder:
   ```bash
   cd frontend
   ```
2. Install client dependencies:
   ```bash
   npm install
   ```
3. Run the Vite developer server:
   ```bash
   npm run dev
   ```
   *The client app runs locally at: `http://localhost:5173`*

---

## 📄 References & Docs

- **API Documentation:** For complete backend endpoints, refer to [backend/REST_API_DOCS.md](file:///d:/Projects/AI%20Customer%20support/backend/REST_API_DOCS.md).
- **Frontend Development Details:** For React component structure and assets details, check out [backend/frontend.md](file:///d:/Projects/AI%20Customer%20support/backend/frontend.md).
- **Backend README:** For model field specifications, see [backend/README.md](file:///d:/Projects/AI%20Customer%20support/backend/README.md).
