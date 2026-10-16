# GyanSetu – Virtual Classroom & Learning Management System

GyanSetu is a full-stack Virtual Classroom and Learning Management System (LMS) designed to make online education easier and more accessible. It provides a platform for managing courses, enrolling students, sharing learning materials, posting announcements, and conducting live online classes.

The application is built using **FastAPI** for the backend and **React + Vite** for the frontend, with PostgreSQL for database management and LiveKit for real-time video conferencing.

## ✨ Features

- **User Authentication:** Login, registration, and OTP-based password recovery.
- **Course Management:** Create, manage, and organize courses.
- **Student Enrollment:** Support student enrollment in available courses.
- **Virtual Classrooms:** Conduct live classes using LiveKit video conferencing.
- **Announcements:** Share important updates and notifications.
- **Learning Materials:** Upload and access notes, PDFs, and other study materials.
- **REST API:** Backend APIs powered by FastAPI.
- **Database Integration:** PostgreSQL support with an optional SQLite configuration.
- **Responsive Frontend:** Modern user interface built with React and Vite.

## 🛠️ Technology Stack

### Frontend
- React
- Vite
- JavaScript
- Tailwind CSS

### Backend
- Python
- FastAPI
- Uvicorn
- SQLAlchemy and database libraries as configured in the project
- SMTP email integration

### Database and Services
- PostgreSQL 16
- SQLite (optional local development database)
- Docker and Docker Compose
- LiveKit for real-time video conferencing

## 📂 Project Structure

```text
teaching_app/
├── backend/
│   ├── app/
│   │   ├── routes/
│   │   ├── models/
│   │   └── schemas/
│   ├── static/
│   ├── docker-compose.yml
│   ├── requirements.txt
│   ├── check_db.py
│   ├── migrate_class_session.py
│   ├── reset_passwords.py
│   └── .env
├── frontend/
│   ├── src/
│   ├── public/
│   ├── package.json
│   ├── tailwind.config.cjs
│   └── .env
└── README.md
```

*Note: The directory structure above is illustrative. Actual files and folders may vary depending on the current project version.*

## ⚙️ Prerequisites

Before running the application, install the following:

- Python 3.10 or later, compatible with the project's dependencies
- Node.js and npm
- Docker Desktop (for the PostgreSQL and LiveKit containers configured in Docker Compose)
- Git

## 🚀 Getting Started

### 1. Clone the Repository

```bash
git clone YOUR_REPOSITORY_URL
cd teaching_app
```

Replace `YOUR_REPOSITORY_URL` with your GitHub repository URL.

### 2. Set Up the Backend

Navigate to the backend directory:

```bash
cd backend
```

Create and activate a Python virtual environment.

**Windows:**

```bash
python -m venv .venv
.venv\Scripts\activate
```

**macOS/Linux:**

```bash
python3 -m venv .venv
source .venv/bin/activate
```

Install the required dependencies:

```bash
pip install -r requirements.txt
```

### 3. Configure Environment Variables

Create a `.env` file inside the `backend` directory.

For PostgreSQL:

```env
DATABASE_URL=postgresql://postgres:postgres@localhost:5433/teaching_app
SECRET_KEY=replace_with_a_secure_random_secret
ACCESS_TOKEN_EXPIRE_MINUTES=1440
```

For SQLite development, use the following database URL instead:

```env
DATABASE_URL=sqlite:///./teaching_app.db
```

Use the database driver, environment variable names, and other settings expected by the actual application configuration.

**Important:** Never commit real passwords, email credentials, API keys, or production secrets to a public repository.

### 4. Start the Database Services

Ensure Docker Desktop is running. From the backend directory, execute:

```bash
docker compose up -d
```

This starts the services defined in `docker-compose.yml`, including PostgreSQL and the configured LiveKit service, if both are defined there.

If you use SQLite, configure the application accordingly and follow the project's database initialization requirements instead.

### 5. Initialize the Database

Run the database utility scripts provided by the project, if required:

```bash
python check_db.py
python migrate_class_session.py
```

These scripts are intended to check database connectivity and apply the relevant classroom-session schema changes. Review their implementation before running them against an existing or production database.

### 6. Run the Backend Server

From the backend directory, execute:

```bash
python -m uvicorn app.main:app --reload --host 127.0.0.1 --port 8000
```

The backend API will be available at:

- **API Base URL:** http://127.0.0.1:8000
- **Interactive API Documentation:** http://127.0.0.1:8000/docs

### 7. Set Up the Frontend

Open a new terminal and navigate to the frontend directory:

```bash
cd frontend
```

Install the frontend dependencies:

```bash
npm install
```

Create a `.env` file inside the frontend directory:

```env
VITE_API_URL=http://localhost:8000
VITE_LIVEKIT_URL=YOUR_LIVEKIT_SERVER_URL
```

Replace `YOUR_LIVEKIT_SERVER_URL` with the LiveKit server URL used by your deployment. For local development, use the URL and protocol supported by your LiveKit configuration.

### 8. Run the Frontend

Start the Vite development server:

```bash
npm run dev
```

Open the local URL displayed in the terminal, usually:

http://localhost:5173

## 🤖 Optional Local AI Integration

The application can be extended with local AI capabilities using [Ollama](https://ollama.com/).

Potential features include:

- Automatic summaries of lecture notes.
- AI-powered explanations of learning topics.
- Question and quiz generation.
- Study assistance based on uploaded materials.

For example, a FastAPI backend can communicate with an Ollama model through its local API or OpenAI-compatible endpoint.

```python
