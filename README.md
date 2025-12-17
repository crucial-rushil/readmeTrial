# Adobe Invoice Automation Platform

## 🌟 Introduction

This project introduces an automated system for invoice submission and contract management built for Adobe. The platform replaces a largely manual, Airtable-based workflow with a streamlined, end-to-end solution that centralizes contractor data, reduces operational errors, and improves visibility across teams. By automating invoice intake, Airtable updates, and contract PDF generation, the system significantly improves efficiency and reliability for both administrators and creators.

> **Important:** The frontend and backend are maintained in **two separate repositories** and communicate via REST APIs.

---

## 🧱 System Architecture (High Level)

The system is split into two major components:

### Frontend (Client)

* **Framework:** React + TypeScript
* **Build Tool:** Vite
* **Styling:** Tailwind CSS
* **Deployment:** Vercel
* **Purpose:**

  * Collect invoice submissions from creators
  * Provide a secure admin dashboard for reviewing invoices
  * Display synced Airtable data in real time

### Backend (Server)

* **Language:** Python
* **Framework:** FastAPI
* **Integrations:** PyAirtable, ReportLab
* **Deployment:** Render
* **Purpose:**

  * Process invoice submissions
  * Update multiple Airtable bases automatically
  * Generate contract PDFs based on submitted data
  * Serve REST APIs consumed by the frontend

---

## 🎯 Frontend Overview

### Initial Goals

* Build a secure invoice submission form for creators
* Upload invoice details and PDFs
* Sync Airtable records automatically
* Provide admins with a real-time dashboard

### Core Pages

* **Home Page** – Adobe-themed landing page linking to invoice form and admin dashboard
* **Login Page** – Admin authentication (protected access)
* **Invoice Submission Form** – Public-facing form for creators to submit payment info and invoices
* **Admin Dashboard** – View payments, POs, Airtable records, and in-progress contract generation

---

## ⚙️ Backend Overview

### Initial Goals

* Automate the entire invoice workflow
* Eliminate manual Airtable updates
* Generate contracts programmatically

### Core Backend Logic

Using **PyAirtable**, the backend:

1. Adds a new record to the **Payments** Airtable
2. Updates the **Community Leaders** Airtable by changing status and attaching invoice PDFs
3. Adjusts balances in the **Purchase Orders** Airtable
4. Generates personalized PDF contracts using **ReportLab** (future-facing but partially implemented)

### Known Integration Notes

* Backend is hosted on Render using a paid tier to avoid cold-start delays
* Airtable base IDs are currently mocked but designed to be replaced with Adobe production IDs

---

## 👥 Team and Roles

| Photo                                                                                                     | Name             | Role            | Major                                        |
| --------------------------------------------------------------------------------------------------------- | ---------------- | --------------- | -------------------------------------------- |
| <img width="120" src="https://github.com/user-attachments/assets/bd206768-80f8-4806-96d7-847ae9b1f5c3" /> | Haasini Paparaji | Project Manager | Economics & Data Science                     |
| <img width="120" src="https://github.com/user-attachments/assets/0e822272-3504-42f6-8175-afb6fc108a96" /> | Ava Shah         | Project Manager | Industrial Engineering & Operations Research |
| <img width="120" src="https://github.com/user-attachments/assets/51ae4c74-f934-4d85-a2a6-aeb8f62e7111" /> | Joyce Kei        | Senior Analyst  | Business Administration                      |
| <img width="120" src="https://github.com/user-attachments/assets/2c2ce120-61bb-4f01-82c3-83a76315d8f5" /> | Ethan Varghese   | Analyst         | Data Science                                 |
| <img width="120" src="https://github.com/user-attachments/assets/f75e950d-7cdd-4fa6-943a-3f469d1db335" /> | Mohammed Jasim   | Analyst         | Data Science                                 |

---

## 🧰 Prerequisites

Ensure the following are installed before setup:

### General

* VS Code
* Git

### Frontend

* Node.js (v18+ recommended)
* npm

### Backend

* Python 3.10+
* pip

---

## ⬇️ Installation & Setup

### Frontend Setup

```bash
git clone https://github.com/<your-frontend-repo>.git
cd <frontend-repo>
npm install
npm run dev
```

The frontend will be available locally at `http://localhost:5173`.

---

### Backend Setup

```bash
git clone https://github.com/<your-backend-repo>.git
cd <backend-repo>
python3 -m venv venv
source venv/bin/activate
pip install fastapi uvicorn pyairtable reportlab
uvicorn main:app --reload
```

The backend API will be available at `http://localhost:8000`.

---

## 🚀 Deployment

### Frontend (Vercel)

1. Connect the frontend repository to Vercel
2. Set build command to `npm run build`
3. Set output directory to `dist`

### Backend (Render)

1. Create a new Web Service on Render
2. Connect the backend repository
3. Set start command:

```bash
uvicorn main:app --host 0.0.0.0 --port 10000
```

4. Use a paid tier to avoid cold start delays

---

## 🌐 Application Routes

| Route          | Description                        |
| -------------- | ---------------------------------- |
| `/`            | Admin login page                   |
| `/dashboard`   | Protected admin dashboard          |
| `/invoiceform` | Public invoice submission form     |
| `/thankyou`    | Confirmation page after submission |

---

## 🔐 Admin Login (Development)

```text
Username: admin
Password: password123
```

### Session Behavior

* Successful login issues a secure session token
* Sessions remain active for 24 hours
* Invalid or expired sessions redirect users to `/`

---

## 📌 Notes

* This project is designed to scale with Adobe’s internal Airtable infrastructure
* Airtable schemas are assumed to remain stable
* Contract generation is modular and extensible

---

## 📄 License

Internal project – not licensed for public redistribution.
