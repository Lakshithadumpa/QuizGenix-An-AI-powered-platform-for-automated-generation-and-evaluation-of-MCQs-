# QuizGenix: AI-Powered Quiz Generation and Evaluation Platform

A full-stack Django application that generates quizzes from educational content using AI (Gemini/OpenAI), supports role-based access (General User, Teacher, Student), OTP verification, and performance tracking.

## Features

- **User Roles**: General User (approval required), Teacher, Student
- **OTP Login**: General users and teachers receive OTP via email (5 min expiry)
- **Quiz Creation**: Manual, AI-generated from PDF/text, personalized (weak areas)
- **Duplicate Detection**: Exact + semantic (embedding-based, 0.85 threshold)
- **Timer**: Optional for general users, settable by teachers; auto-submit on expiry
- **Excel Student Upload**: Teachers upload Name, Email → system generates credentials
- **Performance Tracking**: Used for personalized quiz generation

## Setup

1. Create virtual environment and install dependencies:
   ```bash
   python -m venv venv
   venv\Scripts\activate   # Windows
   pip install -r requirements.txt
   ```

2. Copy `.env.example` to `.env` and configure:
   - `SECRET_KEY`, `DEBUG`, `ALLOWED_HOSTS`
   - `EMAIL_*` for OTP (use console backend for dev)
   - `GOOGLE_API_KEY` or `OPENAI_API_KEY` for AI

3. Run migrations:
   ```bash
   python manage.py migrate
   ```

4. Create superuser (to approve general users):
   ```bash
   python manage.py createsuperuser
   ```

5. Run server:
   ```bash
   python manage.py runserver
   ```

## Usage

- **General User**: Register → wait for admin approval → login (OTP) → create/attempt quizzes
- **Teacher**: Register → login (OTP) → create quizzes, upload students via Excel
- **Student**: Use credentials from teacher → login (no OTP) → attempt assigned quizzes

## Excel Format for Students

| Name   | Email           |
|--------|-----------------|
| John   | john@school.edu |
| Jane   | jane@school.edu |
