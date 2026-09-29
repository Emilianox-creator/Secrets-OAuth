# Secrets Project

## About

Secrets Project is a server-rendered web application for creating an account, signing in, and keeping a personal secret. After authentication, a user can submit a secret and return to view or replace it later. Each account has one saved secret, stored with its user record in PostgreSQL.

The project brings together a few common web-development building blocks: Express handles routes and form submissions, EJS renders the pages, and PostgreSQL stores account and secret data. Passport manages local email-and-password sign-in as well as optional Google OAuth. Passwords for local accounts are hashed with bcrypt, and Passport sessions keep users signed in as they move between pages.

### Features

- Register with an email and password, or sign in to an existing account.
- Optionally authenticate through Google OAuth.
- Save, view, and update a personal secret after signing in.
- Restrict secret pages to authenticated users and redirect visitors to sign-in.
- Render the home, login, registration, secret, and submission pages with EJS.

This is a learning project that ties together authentication, server-side rendering, form handling, and relational database access in a single application.

## Requirements

- Node.js and npm
- PostgreSQL
- Google OAuth credentials if you want to use Google sign-in

## Setup

1. Install dependencies:

   ```sh
   npm install
   ```

2. Create a PostgreSQL database and a `users` table. For a new database, run:

   ```sql
   CREATE TABLE users (
     id SERIAL PRIMARY KEY,
     email TEXT UNIQUE NOT NULL,
     password TEXT NOT NULL,
     secret TEXT
   );
   ```

   The included [solution-queries.sql](solution-queries.sql) adds the `secret` column to an existing `users` table. Run that statement only if your table does not already have the column.

3. Create a `.env` file in the project root:

   ```env
   SESSION_SECRET=replace-with-a-long-random-value
   PG_USER=your-postgres-user
   PG_HOST=localhost
   PG_DATABASE=your-database-name
   PG_PASSWORD=your-postgres-password
   PG_PORT=5432
   GOOGLE_CLIENT_ID=your-google-client-id
   GOOGLE_CLIENT_SECRET=your-google-client-secret
   ```

   Google sign-in uses the callback URL `http://localhost:3000/auth/google/secrets`; configure this URL in your Google OAuth client. Local email/password sign-in does not require Google credentials.

4. Start the server:

   ```sh
   node index.js
   ```

5. Open [http://localhost:3000](http://localhost:3000).

## Routes

- `/` - Home
- `/register` and `/login` - Create an account or sign in
- `/secrets` - View the signed-in user's secret
- `/submit` - Save or update a secret
- `/auth/google` - Sign in with Google
- `/logout` - Sign out

The server listens on port `3000`. The package does not currently define a start or test script.
