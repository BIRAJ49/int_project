# Job & Internship Portal

A full-stack Job & Internship Portal built with React (Vite + Tailwind), Node.js (Express), and PostgreSQL with Prisma ORM.

## Features
- JWT authentication with bcrypt password hashing
- Roles: STUDENT, COMPANY, ADMIN
- Job listings, applications, and dashboards
- Clean modern UI with responsive layout
- Prisma schema + seed data

## Local Setup

### 1) Backend
```bash
cd backend
cp .env.example .env
npm install

# Run PostgreSQL locally (or update DATABASE_URL in .env)
# Create tables + seed data
npx prisma migrate dev --name init
npx prisma db seed

npm run dev
```
Notes:
- Email verification is required before login. Configure Resend via `RESEND_API_KEY` + `RESEND_FROM`.
- New accounts require admin approval before login (see Admin Panel).
- Resume uploads are stored privately in S3 and returned as short-lived signed URLs. Configure `S3_BUCKET`, `S3_REGION`, credentials, and optionally `S3_SIGNED_URL_EXPIRES` (seconds).
- Admin login is restricted to `ADMIN_EMAIL` (set this to your admin email).
- Contact form sends to `CONTACT_TO` and auto-replies to the sender.

### 2) Frontend
```bash
cd frontend
cp .env.example .env
npm install
npm run dev
```

### Seeded accounts
- Admin: `admin@portal.com` / `password123`
- Company: `company@portal.com` / `password123`
- Student: `student@portal.com` / `password123`

## Docker Setup
```bash
docker compose up --build
```

Then in another terminal (or the running backend container):
```bash
cd backend
npx prisma migrate dev --name init
npx prisma db seed
```

## Project Structure
```
/ (root)
  /frontend
  /backend
  /docker-compose.yml
```

## Notes
- `VITE_API_URL` defaults to `http://localhost:4000`
- Jobs are created as approved by default.
