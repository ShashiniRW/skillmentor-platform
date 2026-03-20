# SkillMentor Platform

> An online mentoring platform that connects students with expert mentors for specialised subjects. Students can browse mentors, book one-on-one sessions, make payments, and track their learning progress through a personalised dashboard.

---

## Features

### Student Features
- Browse and discover available mentors with their expertise and subjects
- View detailed mentor profile pages with bio, subjects, stats, and reviews
- Book one-on-one sessions with preferred mentors
- Select session date, time, and duration
- Upload payment proof (bank slip) for session confirmation
- Student dashboard to track all enrolled sessions
- View session status (Pending, Confirmed, Completed)
- Write reviews for completed sessions
- Double-booking prevention (cannot book overlapping sessions)

### Admin Features
- Role-based access control (Admin vs Student)
- Admin dashboard with sidebar navigation
- Create and manage subjects (name, description, image, assigned mentor)
- Create and manage mentor profiles with complete information
- View all student bookings across the platform in a data table
- Approve pending payment confirmations
- Mark sessions as completed
- Add meeting links to confirmed sessions
- Filter and search bookings by status, student name, or mentor name

### Platform Features
- Clerk authentication (sign up, sign in, role-based access)
- Protected routes for students and admins
- JWT-based API security
- Responsive design (mobile-friendly)
- Loading states and error handling throughout

---

## Tech Stack

| Layer | Technology |
|-------|-----------|
| Frontend | React 18 + TypeScript + Vite |
| Styling | Tailwind CSS + shadcn/ui |
| Forms | React Hook Form + Zod |
| Authentication | Clerk |
| Backend | Spring Boot (Java) |
| Database | PostgreSQL (Supabase) |
| ORM | Spring Data JPA |
| API Docs | SpringDoc OpenAPI (Swagger) |
| Security | Spring Security + Clerk JWT |
| Frontend Deployment | Vercel |
| Backend Deployment | Railway |

---

## Project Structure

```
skillmentor-platform/
├── frontend/
│   ├── public/
│   ├── src/
│   │   ├── assets/
│   │   ├── components/
│   │   │   ├── ui/              # shadcn/ui components
│   │   │   ├── Footer.tsx
│   │   │   ├── Layout.tsx
│   │   │   ├── MentorCard.tsx
│   │   │   ├── Navigation.tsx
│   │   │   ├── SchedulingModel.tsx
│   │   │   ├── SignUpDialog.tsx
│   │   │   └── StatusPill.tsx
│   │   ├── pages/
│   │   │   ├── HomePage.tsx
│   │   │   ├── DashboardPage.tsx
│   │   │   ├── PaymentPage.tsx
│   │   │   ├── LoginPage.tsx
│   │   │   └── admin/
│   │   ├── lib/
│   │   ├── types.ts
│   │   └── App.tsx
│   ├── package.json
│   └── vite.config.ts
├── backend/
│   └── src/main/java/com/stemlink/skillmentor/
│       ├── configs/             # CORS, Security, OpenAPI, Redis
│       ├── controllers/         # REST controllers
│       ├── dto/                 # Data Transfer Objects
│       ├── entities/            # JPA entities
│       ├── exceptions/
│       ├── repositories/
│       ├── security/            # Clerk JWT validation
│       ├── services/
│       └── utils/
└── README.md
```

---

## Getting Started (Local Development)

### Prerequisites
- Node.js 18+
- Java 17+
- Maven
- PostgreSQL database (or Supabase account)
- Clerk account

### Backend Setup

```bash
# Navigate to backend
cd backend

# Copy environment file and fill in your values
cp .env.example .env

# Run the application
./mvnw spring-boot:run
```

The backend will start on `http://localhost:8080`

### Frontend Setup

```bash
# Navigate to frontend
cd frontend

# Install dependencies
npm install

# Copy environment file and fill in your values
cp .env.example .env.local

# Start development server
npm run dev
```

The frontend will start on `http://localhost:5173`

---

## Environment Variables

### Backend (`backend/.env`)

```env
SPRING_DATASOURCE_URL=jdbc:postgresql://<host>:<port>/<database>
SPRING_DATASOURCE_USERNAME=your_db_username
SPRING_DATASOURCE_PASSWORD=your_db_password
CLERK_JWKS_URL=https://<your-clerk-domain>/.well-known/jwks.json
SPRING_PROFILES_ACTIVE=dev
```

### Frontend (`frontend/.env.local`)

```env
VITE_CLERK_PUBLISHABLE_KEY=pk_test_xxxxxxxxxxxxxxxx
VITE_API_BASE_URL=http://localhost:8080
```

---

## API Documentation

Full interactive API documentation is available via Swagger UI at:
`<backend-url>/swagger-ui.html`

### Endpoints Overview

| Method | Endpoint | Auth Required | Purpose |
|--------|----------|---------------|---------|
| GET | `/api/v1/mentors` | No | List all mentors with subjects |
| GET | `/api/v1/mentors/{id}` | No | Get single mentor details |
| POST | `/api/v1/mentors` | Yes (Admin) | Create a new mentor |
| GET | `/api/v1/subjects` | No | List all subjects |
| POST | `/api/v1/subjects` | Yes (Admin) | Create a new subject |
| POST | `/api/v1/sessions/enroll` | Yes (Student) | Create new session booking |
| GET | `/api/v1/sessions/my-sessions` | Yes (Student) | Get student's sessions |
| GET | `/api/v1/sessions` | Yes (Admin) | Get all sessions |
| PATCH | `/api/v1/sessions/{id}/confirm` | Yes (Admin) | Confirm session payment |
| PATCH | `/api/v1/sessions/{id}/complete` | Yes (Admin) | Mark session as completed |
| GET | `/api/v1/students` | Yes (Admin) | List all students |

### Authentication

All protected endpoints require a valid Clerk JWT token in the Authorization header:
```
Authorization: Bearer <clerk_jwt_token>
```

Admin endpoints additionally require the user to have `roles: ["ADMIN"]` in their Clerk public metadata.

---

## Database Schema

| Table | Description |
|-------|-------------|
| `mentors` | Mentor profiles (name, bio, title, company, experience) |
| `subjects` | Subjects/courses taught (name, description, image, mentor) |
| `students` | Student profiles linked to Clerk user ID |
| `sessions` | Booking records (student, mentor, subject, date, status, payment) |

---

## Deployment

### Frontend — Vercel
1. Connect GitHub repository to Vercel
2. Set root directory to `frontend`
3. Add environment variables in Vercel dashboard
4. Deploy

### Backend — Railway
1. Connect GitHub repository to Railway
2. Set root directory to `backend`
3. Add environment variables in Railway dashboard
4. Railway auto-detects Spring Boot and deploys

### Database — Supabase
1. Create a new Supabase project
2. Copy the PostgreSQL connection string
3. Add to backend environment variables

---

## Deployed Links

- **Frontend:** `https://your-app.vercel.app` *(update after deployment)*
- **Backend Swagger:** `https://your-app.railway.app/swagger-ui.html` *(update after deployment)*

---

## Sample Data

The database is seeded with:
- 3+ mentor profiles with complete information
- 5+ subjects across different technology areas
- 1 admin user configured in Clerk

---

## Acknowledgements

Built as part of a Full-Stack Development assignment demonstrating REST API design, database relationships, authentication, and production deployment.
