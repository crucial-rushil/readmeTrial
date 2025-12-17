# Adobe Invoice Automation Platform

## 📚 Table of Contents

<details open>
<summary><strong>Contents</strong></summary>

- 🌟 [Introduction](#introduction)
- 🧱 [System Architecture](#system-architecture)
- 🎯 [Frontend Overview](#frontend-overview)
- ⚙️ [Backend Overview](#backend-overview)
- 🌐 [Application Routes](#application-routes)
- 👥 [Team and Roles](#team-and-roles)
- 🧰 [Prerequisites](#prerequisites)
- ⬇️ [Installation & Setup](#installation-setup)
- 🚀 [Deployment](#deployment)
- 🔐 [Admin Login](#admin-login)
- 📌 [Notes](#notes)
- 📄 [License](#license)

</details>

---

<h2 id="introduction">🌟 Introduction</h2>

This project introduces an automated system for invoice submission and contract management built for Adobe. The platform replaces a largely manual, Airtable-based workflow with a streamlined, end-to-end solution that centralizes contractor data, reduces operational errors, and improves visibility across teams. By automating invoice intake, Airtable updates, and contract PDF generation, the system significantly improves efficiency and reliability for both administrators and creators.

> **Important:** The frontend and backend are maintained in **two separate repositories** and communicate via REST APIs.

---

<h2 id="system-architecture">🧱 System Architecture (High Level)</h2>

The system is split into two major components:

### Frontend (Client)
- **Framework:** React + TypeScript  
- **Build Tool:** Vite  
- **Styling:** Tailwind CSS  
- **Deployment:** Vercel  

**Responsibilities**
- Collect invoice submissions from creators  
- Provide a secure admin dashboard  
- Display Airtable-backed data in real time  

### Backend (Server)
- **Language:** Python  
- **Framework:** FastAPI  
- **Integrations:** PyAirtable, ReportLab  
- **Deployment:** Render  

**Responsibilities**
- Act as the system’s automation engine  
- Process invoice submissions  
- Update multiple Airtable bases deterministically  
- Generate contract PDFs  
- Expose REST APIs to the frontend  

---

<h2 id="frontend-overview">🎯 Frontend Overview</h2>

### Initial Goals
- Build a **secure invoice submission form** for creators  
- Support uploading payment details and invoice PDFs  
- Automatically sync submissions with the backend  
- Provide admins with a **real-time operational dashboard**  

### Core Pages
- **Home Page** – Adobe-themed landing page routing users to submission or admin login  
- **Login Page** – Protected admin authentication  
- **Invoice Submission Form** – Public-facing creator form with client-side validation  
- **Admin Dashboard** – Internal dashboard displaying payments, purchase orders, and contract progress  

The frontend intentionally contains minimal business logic. All validation beyond basic checks, Airtable updates, and contract generation are handled server-side.

---

<h2 id="backend-overview">⚙️ Backend Overview</h2>

### Initial Goals
- **Automate the entire invoice workflow**  
- Eliminate manual Airtable updates  
- Enforce consistent business rules  
- Enable programmatic contract generation  

### Core Backend Logic
Using **PyAirtable**, the backend:
1. Creates a record in the **Payments** table  
2. Updates **Community Leaders** status and attaches invoice PDFs  
3. Adjusts balances in **Purchase Orders**  
4. Generates personalized PDF contracts via **ReportLab** (partially implemented)  

Each submission is processed as a single transaction to prevent partial state updates.

### Known Integration Notes
- Hosted on Render using a paid tier to avoid cold starts  
- Airtable base IDs are mocked for development but easily replaceable with production IDs  

---

<h2 id="team-and-roles">👥 Team and Roles</h2>

| Photo | Name | Role | Major |
|------|------|------|-------|
| <img width="120" src="https://github.com/user-attachments/assets/bd206768-80f8-4806-96d7-847ae9b1f5c3" /> | Haasini Paparaji | Project Manager | Economics & Data Science |
| <img width="120" src="https://github.com/user-attachments/assets/0e822272-3504-42f6-8175-afb6fc108a96" /> | Ava Shah | Project Manager | Industrial Engineering & Operations Research |
| <img width="120" src="https://github.com/user-attachments/assets/51ae4c74-f934-4d85-a2a6-aeb8f62e7111" /> | Joyce Kei | Senior Analyst | Business Administration |
| <img width="120" src="https://github.com/user-attachments/assets/2c2ce120-61bb-4f01-82c3-83a76315d8f5" /> | Ethan Varghese | Analyst | Data Science |
| <img width="120" src="https://github.com/user-attachments/assets/f75e950d-7cdd-4fa6-943a-3f469d1db335" /> | Mohammed Jasim | Analyst | Data Science |

---

<h2 id="prerequisites">🧰 Prerequisites</h2>

### General
- VS Code  
- Git  

### Frontend
- Node.js (v18+)  
- npm  

### Backend
- Python 3.10+  
- pip  

---

<h2 id="installation-setup">⬇️ Installation & Setup</h2>

### Frontend
```bash
git clone https://github.com/<your-frontend-repo>.git
cd <frontend-repo>
npm install
npm run dev
