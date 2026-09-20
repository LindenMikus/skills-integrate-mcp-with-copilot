# Mergington High School Activities API

A super simple FastAPI application that allows students to view and sign up for extracurricular activities.

## Features

- View all available extracurricular activities
- Staff authentication with user and admin roles
- Admin-only activity registration and removal

## Getting Started

1. Install the dependencies:

   ```
   pip install fastapi uvicorn
   ```

2. Run the application:

   ```
   python app.py
   ```

3. Open your browser and go to:
   - API documentation: http://localhost:8000/docs
   - Alternative documentation: http://localhost:8000/redoc

## API Endpoints

| Method | Endpoint                                                          | Description                                                         |
| ------ | ----------------------------------------------------------------- | ------------------------------------------------------------------- |
| GET    | `/activities`                                                     | Get all activities with their details and current participant count |
| POST   | `/auth/register`                                                  | Create a regular user account                                      |
| POST   | `/auth/login`                                                     | Start an authenticated session                                     |
| POST   | `/auth/logout`                                                    | End the current session                                            |
| GET    | `/auth/me`                                                        | Get the current user                                               |
| POST   | `/activities/{activity_name}/signup?email=student@mergington.edu` | Admin-only activity registration                                   |
| DELETE | `/activities/{activity_name}/unregister?email=student@mergington.edu` | Admin-only activity removal                                      |

Set `ADMIN_USERNAME` and `ADMIN_PASSWORD` before starting the server to configure
the initial admin account. Passwords are stored as PBKDF2-SHA256 hashes and
sessions use an HTTP-only cookie. Set `COOKIE_SECURE=true` when serving over
HTTPS.

## Data Model

The application uses a simple data model with meaningful identifiers:

1. **Activities** - Uses activity name as identifier:

   - Description
   - Schedule
   - Maximum number of participants allowed
   - List of student emails who are signed up

2. **Students** - Uses email as identifier:
   - Name
   - Grade level

Activities, user accounts, and sessions are currently stored in memory, which
means they will be reset when the server restarts. Persistent storage is tracked
in issue #13.
