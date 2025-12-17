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

  * Act as the system’s source of truth and automation engine
  * Process invoice submissions from the frontend
  * Update multiple Airtable bases in a consistent, deterministic manner
  * Generate contract PDFs based on submitted data
  * Expose REST APIs consumed by the frontend

---

## 🎯 Frontend Overview

### Initial Goals

The frontend was designed to be the primary interface for both creators and administrators, replacing direct interaction with Airtable and reducing friction in the invoice submission process. The core goals were to:

* Build a **secure invoice submission form** that allows creators to enter payment details and upload invoice PDFs without exposing internal tools.
* Enforce **basic validation and structure** on submitted data so that incomplete or malformed submissions are caught early.
* Automatically sync submitted data with the backend so Airtable records stay consistent without manual admin intervention.
* Provide administrators with a **real-time dashboard** to monitor invoice status, payments, and purchase orders from a single interface.

### Core Pages

* **Home Page** – An Adobe-themed landing page that routes users to either the invoice submission form or the admin login.
* **Login Page** – A protected authentication page that restricts access to internal tools to authorized admins.
* **Invoice Submission Form** – A public-facing form where creators submit payment information and upload invoice PDFs, which are then sent to the backend for processing.
* **Admin Dashboard** – An internal dashboard that displays synced Airtable data, including payments, purchase orders, and community leader records, as well as visibility into in-progress contract generation.

The frontend intentionally contains minimal business logic. All payment handling, Airtable updates, and contract generation are delegated to the backend via REST APIs to keep the client lightweight and secure.

---

## ⚙️ Backend Overview

### Initial Goals

The backend was built to replace a multi-step, human-driven invoice workflow with a single automated pipeline. Before this system, administrators manually reviewed submissions, updated multiple Airtable bases, and tracked balances by hand. The backend goals were to:

* **Automate the entire invoice workflow** so that one submission triggers all required downstream updates.
* Eliminate manual Airtable edits by centralizing update logic in a FastAPI service.
* Reduce latency and human error by enforcing consistent business rules server-side.
* Enable **programmatic contract generation** based on invoice and creator data.

### Core Backend Logic

Using **PyAirtable**, the backend:

1. Adds a new record to the **Payments** Airtable upon invoice submission.
2. Updates the **Community Leaders** Airtable by changing invoice status and attaching uploaded invoice PDFs.
3. Adjusts balances in the **Purchase Orders** Airtable by subtracting the submitted payment amount.
4. Generates personalized PDF contracts using **ReportLab** (future-facing but partially implemented).

Each submission is treated as a single transaction so that partial updates do not leave Airtable in an inconsistent state.

### Known Integration Notes

* The backend is hosted on Render using a paid tier to avoid cold-start delays during periods of inactivity.
* Airtable base IDs are currently mocked for development but are designed to be replaced with Adobe production Airtable IDs without requiring frontend changes.

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

| Route          | Description                                                                                                                                                                                                                                                                    |
| -------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `/`            | Entry point to the application. Displays the admin login screen and acts as the gateway to all protected functionality. Users who are already authenticated are redirected to the dashboard.                                                                                   |
| `/dashboard`   | Protected admin dashboard that surfaces real-time, Airtable-backed data. Admins can review submitted invoices, monitor payment and purchase order status, inspect Community Leader records, and track the progress of contract generation without directly accessing Airtable. |
| `/invoiceform` | Public-facing invoice submission page for creators. Collects structured payment information and invoice PDFs, performs basic client-side validation, and sends submissions to the backend for automated processing and Airtable synchronization.                               |
| `/thankyou`    | Confirmation page shown after a successful invoice submission. Provides creators with clear feedback that their invoice has been received and processed, reducing duplicate submissions and follow-up questions.                                                               |


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
