# CareerPilot 🧭

CareerPilot helps students discover career paths that genuinely fit their skills and personality, then hands them a personalized roadmap of resources to pursue that path — not just a quiz result.

![Status](https://img.shields.io/badge/status-MVP-blue)
![License](https://img.shields.io/badge/license-MIT-green)

## Table of Contents
- [Features](#features)
- [Tech Stack](#tech-stack)
- [Getting Started](#getting-started)
- [Project Structure](#project-structure)
- [API Overview](#api-overview)
- [Roadmap](#roadmap)
- [Team Workflow](#team-workflow)
- [Contributing](#contributing)
- [License](#license)

## Features

**MVP (implemented):**
- 🔐 JWT-based authentication (register, login, password reset)
- 📝 Skills & personality assessment
- 🎯 Rule-based career matching engine
- 🗺️ Personalized learning roadmap per matched career
- ⭐ Save/bookmark favorite careers

**Planned (post-MVP):** see [Roadmap](#roadmap) below.

## Tech Stack

| Layer | Technology |
|---|---|
| Frontend | React (SPA, client-side routing via React Router) |
| Backend | Flask REST API |
| Database | SQLite (dev) / PostgreSQL (production) |
| Auth | JWT (JSON Web Tokens) |

## Getting Started

### Prerequisites
- Node.js (v18+) and npm
- Python 3.10+ and pip

### Backend Setup
\`\`\`bash
cd backend
python -m venv venv
source venv/bin/activate      # Windows: venv\Scripts\activate
pip install -r requirements.txt
python app.py
\`\`\`

### Frontend Setup
\`\`\`bash
cd frontend
npm install
npm start
\`\`\`

### Environment Variables
Create a `.env` file inside `backend/`:
\`\`\`
JWT_SECRET_KEY=your_secret_key_here
DATABASE_URL=sqlite:///careerpilot.db
\`\`\`

## Project Structure
\`\`\`
careerpilot/
├── backend/
│   ├── models/          # SQLAlchemy models (User, Career, Roadmap, etc.)
│   ├── routes/           # Flask blueprints / endpoints
│   ├── app.py             # App entry point
│   └── requirements.txt
├── frontend/
│   ├── src/
│   │   ├── components/  # Reusable UI components
│   │   ├── pages/         # Route-level views
│   │   └── App.js
│   └── package.json
└── README.md
\`\`\`

## API Overview

| Method | Endpoint | Auth Required | Description |
|---|---|---|---|
| POST | /api/register | No | Create new user |
| POST | /api/login | No | Authenticate, return JWT |
| POST | /api/reset-request | No | Request