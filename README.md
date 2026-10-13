# Eventora - Full-Stack Event Booking Platform

A comprehensive, production-grade MERN (MongoDB, Express, React, Node.js) application designed for modern event discovery, automated booking management, and administrative oversight. Both the frontend and backend are housed within this single unified repository.

---

## ⚡ Quick Evaluation & Testing Guide

For evaluators and reviewers, you can quickly spin up both the frontend and backend and test with pre-seeded demo accounts without manual registration or OTP setup.

### 🔑 Pre-Seeded Demo Credentials
After running the seed command (`npm run seed`), use the following credentials to test all roles immediately:

| Role | Email | Password | Access / Capabilities |
| :--- | :--- | :--- | :--- |
| **Admin** | `admin@eventora.com` | `password123` | Full access to Admin Dashboard, create/edit/delete events, approve/reject bookings, mark payments as Paid/Unpaid, live revenue analytics. |
| **User** | `user@eventora.com` | `password123` | Browse events, view seats, submit booking requests, view personal ticket status in User Dashboard, cancel bookings. |

---

## 🚀 Getting Started in 3 Steps

### 1. Prerequisites
- [Node.js](https://nodejs.org/) (v16 or higher)
- [MongoDB](https://www.mongodb.com/) (Local instance running at `mongodb://localhost:27017` or free [MongoDB Atlas](https://www.mongodb.com/cloud/atlas/register) cluster)

### 2. Configure Environment (`server/.env`)
Copy the example environment configuration into `server/.env`:
```bash
cp server/.env.example server/.env
```
Fill in your configuration in `server/.env`:
```env
MONGO_URI=mongodb://localhost:27017/eventora
JWT_SECRET=supersecretjwtkey_eventora
EMAIL_USER=your_email@gmail.com
EMAIL_PASS=your_gmail_app_password
PORT=5000
```
> **Note**: For local evaluation, if `MONGO_URI` is left empty, the server automatically defaults to `mongodb://localhost:27017/eventora`.

### 3. Install & Run (Single Terminal from Root)
From the root repository folder, run:

```bash
# Install dependencies for both root, server, and client
npm run install:all

# Seed dummy database data (creates 10 verified users, 6 sample events, and demo bookings)
npm run seed

# Start both Backend (port 5000) and Frontend (Vite) simultaneously
npm run dev
```

- **Frontend Application**: [http://localhost:5173](http://localhost:5173)
- **Backend API**: [http://localhost:5000](http://localhost:5000)

---

## 📂 Project Architecture (Monorepo Structure)

This single repository contains both the client and server applications:

```
Eventoraa/
├── client/                     # Frontend (React 18 + Vite + Tailwind CSS)
│   ├── src/
│   │   ├── components/         # Reusable UI elements (Navbar, Modals, etc.)
│   │   ├── context/            # AuthContext (JWT & state management)
│   │   ├── pages/              # Home, AdminDashboard, UserDashboard, EventDetail, etc.
│   │   └── utils/              # Axios instance configured with interceptors
│   ├── package.json
│   └── vite.config.js
├── server/                     # Backend (Node.js + Express + Mongoose)
│   ├── controllers/            # authController, eventController, bookingController
│   ├── middleware/             # JWT auth & admin authorization
│   ├── models/                 # User, Event, Booking, OTP schemas
│   ├── routes/                 # Express API routes
│   ├── utils/                  # Nodemailer email & OTP delivery
│   ├── seed.js                 # Database populator script
│   └── server.js               # Main Express entrypoint
├── Eventora_Postman_Collection.json # Complete API testing collection
├── dfd.png                     # Data Flow Diagram (DFD)
├── fc.png                      # Architecture Flowchart
├── package.json                # Root package with unified concurrently scripts
└── SETUP_GUIDE.md              # Detailed step-by-step setup walkthrough
```

---

## ✨ Core Features

- **Authentication & Authorization**:
  - Secure signup and login with hashed passwords (`bcryptjs`) and signed JWT tokens (`jsonwebtoken`).
  - Strict role-based route protection for standard Users and Administrators.
- **2FA OTP Verification**:
  - Mandatory Email OTP to activate your account upon registration.
  - Mandatory Email OTP to authorize and finalize event ticket booking requests.
- **Event Lifecycle Management**:
  - Event organizers (Admin) can create, update, and delete events with high-resolution images, dates, seating limits, and ticket prices.
  - Dynamic seat countdown ensuring no overbooking occurs.
- **Admin Command Center**:
  - Review all incoming booking requests in a real-time 'Pending' queue.
  - Approve, reject, and confirm paid/unpaid statuses.
  - Live analytics for total revenue, confirmed attendees, and pending inquiries.
- **User Dashboard**:
  - View all personal bookings with statuses (`pending`, `confirmed`, `cancelled`).
  - Self-service booking cancellation.
- **Automated Email Notifications**:
  - Instant dispatch of booking confirmations and one-time passwords via Nodemailer.

---

## 📮 API Documentation & Postman Collection

A complete, pre-configured Postman collection is included directly in the root directory:
👉 **`Eventora_Postman_Collection.json`**

### How to use:
1. Open [Postman](https://www.postman.com/) and click **Import**.
2. Select `Eventora_Postman_Collection.json`.
3. The collection has pre-configured environment variables that automatically capture your JWT token on login and pass it to protected endpoints.

---

## 📊 System Architecture & Diagrams

- **Data Flow Diagram (DFD)**: See [`dfd.png`](./dfd.png) for data pipeline and role interactions.
- **Flowchart**: See [`fc.png`](./fc.png) for user registration, event booking, and approval workflows.
