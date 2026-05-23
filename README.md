# Online Python Examination System

Full-stack online examination platform built with:

- React + Tailwind CSS frontend
- Flask + PostgreSQL backend
- JWT-protected hidden admin portal
- Public student exam access with no student login
- Python code execution with hidden test cases

## Fixed Access URLs

Student public URL:

```text
http://192.168.29.84:5000
```

Hidden admin portal:

```text
http://192.168.29.84:5000/secure-admin-portal/login
http://192.168.29.84:5000/secure-admin-portal/dashboard
```

Students do not log in. They only enter:

- Name
- Gmail
- Course/Exam Name

Admin login is separate and protected by JWT authentication.

## Architecture

### Frontend

- React
- React Router
- Tailwind CSS
- Axios
- CodeMirror for Python editor

### Backend

- Flask
- Flask-SQLAlchemy
- Flask-Migrate
- Flask-JWT-Extended
- Flask-Cors
- PostgreSQL

### Core Backend Modules

- `app/api/public.py`: public student APIs
- `app/api/admin.py`: secure admin APIs
- `app/services/exam_engine.py`: exam generation, evaluation, submission logic
- `app/services/code_runner.py`: Python code execution service
- `app/seed.py`: seeds roles, topics, questions, test cases, and default exam

## Database Model

Main tables:

- `roles`
- `users`
- `topics`
- `mcq_questions`
- `programming_questions`
- `programming_testcases`
- `exams`
- `exam_questions`
- `submissions`
- `exam_session_questions`
- `submission_answers`
- `results`
- `execution_logs`
- `time_extensions`

## Seeded Content

The seed command creates:

- 2 roles: `admin`, `student`
- 1 admin user
- 16 Python topics
- 10 MCQ questions per topic
- 10 programming questions per topic
- 3 hidden test cases per programming question
- 1 published Python exam

Current seeded totals after setup:

- 16 topics
- 160 MCQ questions
- 160 programming questions
- 480 hidden test cases

## Admin Credentials

Default admin credentials:

- Username: `admin`
- Password: `Admin@123`

Change them after first setup.

## First-Time Setup

Run these commands in PowerShell from `D:\OMES`.

### 1. Install Python dependencies

```powershell
python -m pip install -r requirements.txt
```

### 2. Install frontend dependencies

```powershell
cd frontend
npm install
cd ..
```

### 3. Apply database migrations

This project now uses a schema reset migration for the new React/API platform.

```powershell
python -m flask --app run.py db upgrade
```

### 4. Seed platform data

```powershell
python -m flask --app run.py seed-platform
```

### 5. Build the React frontend

```powershell
cd frontend
npm run build
cd ..
```

### 6. Run the Flask server

```powershell
python run.py
```

## Daily Run

After setup, usually this is enough:

```powershell
cd D:\OMES
python run.py
```

## Public Student Flow

1. Open `http://192.168.29.84:5000`
2. Enter Name, Gmail, and Course/Exam Name
3. Start the exam directly
4. Answer mixed MCQ and programming questions
5. Run Python code in the browser editor
6. Submit manually or let the timer auto-submit
7. View result analytics

## Admin Flow

1. Open `http://192.168.29.84:5000/secure-admin-portal/login`
2. Log in with admin credentials
3. Open the dashboard
4. Create topics
5. Add MCQ questions
6. Add programming questions with hidden test cases
7. Create or update exams
8. Review submissions
9. Extend time for selected students
10. Export reports

## Important Notes

- Student login is intentionally not implemented.
- Admin links are not shown on the public homepage.
- Programming test cases are never exposed to students.
- The backend currently executes Python only, but the architecture is ready for future language runners.
- React production files are built into `app/static/spa`.

## Useful Commands

Run the backend:

```powershell
python run.py
```

Find your IP address:

```powershell
ipconfig
```

Rebuild the frontend after UI changes:

```powershell
cd frontend
npm run build
cd ..
```

Reseed the platform:

```powershell
python -m flask --app run.py seed-platform
```

## Verification Performed

These checks were completed locally:

- `python -m compileall app run.py`
- `npm run build`
- public API exam listing via Flask test client
- admin login and dashboard API via Flask test client
