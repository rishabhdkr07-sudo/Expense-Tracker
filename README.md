# Finora 2.0 — Cloud Personal Finance Manager

A vanilla HTML/CSS/JavaScript personal finance application using Supabase Authentication and PostgreSQL.

## Included
- Email/password sign-up, login, logout and password reset email
- Cloud-saved user transactions with add/edit/delete/search/filter
- PDF transaction statements and CSV export
- Category monthly budgets and progress tracking
- Savings goals and contributions (contributions do **not** count as expenses)
- Monthly comparison of income, expenses, savings and category spending
- Rule-based spending insights generated from the user's own records
- Dashboard charts, responsive layout and dark mode
- Row Level Security (RLS) policies in the supplied SQL schema

## Important setup required before first use
This is a cloud-connected starter project. It cannot authenticate or save cloud data until you connect it to your own Supabase project. Do not publish it as a working login app before completing these steps.

### 1. Create a Supabase project
1. Go to https://supabase.com/ and create a free project.
2. Choose a strong database password and keep it private.
3. In the project dashboard, open **Project Settings → API** (or API Keys).
4. Copy the Project URL and the publishable/anon key. Never use the `service_role` or secret key in browser code.

### 2. Create database tables and security policies
1. Open **SQL Editor** in your Supabase project.
2. Open `supabase-schema.sql` from this project.
3. Copy its full contents into a new SQL query and run it.
4. Confirm that `transactions`, `budgets`, and `savings_goals` tables exist.

### 3. Configure the website
1. Open `config.js`.
2. Replace `https://YOUR-PROJECT-REF.supabase.co` with your Project URL.
3. Replace `YOUR_SUPABASE_ANON_OR_PUBLISHABLE_KEY` with your publishable/anon key.
4. Save the file.

The browser key is designed to be public. Database security depends on RLS policies. Never put a service role key in `config.js`.

### 4. Configure authentication URLs
In Supabase **Authentication → URL Configuration**:
- Set Site URL to your deployed website URL, for example `https://YOUR-USERNAME.github.io/YOUR-REPOSITORY/`.
- Add that exact URL to the Redirect URLs allow-list.
- For password reset links, also allow the URL path used by your deployment.
- For local testing, add your local development URL if needed.

For GitHub Pages, use the actual URL shown in your repository's Settings → Pages. Do not copy the example URL without replacing the username/repository.

### 5. Run locally
Open the folder in VS Code and use the Live Server extension, or serve it using any static web server. Avoid opening `index.html` as a `file://` URL because auth redirects need a web origin.

### 6. Deploy to GitHub Pages
Upload all project files to the root of a GitHub repository, including the configured `config.js` and `supabase-schema.sql`. Then enable Pages from `main` / root. Wait for deployment and visit the Pages URL.

## How persistence and logout work
- Transactions, budgets and goals are stored in Supabase PostgreSQL under the signed-in user's `user_id`.
- Logging out ends the authentication session; it does not delete the database records.
- Logging back into the same account fetches the saved records.
- The same account can access its records on another device.
- RLS policies restrict access so authenticated users can only select/insert/update/delete rows whose `user_id` matches their auth user ID.
- Download CSV/PDF reports periodically if you want an additional offline copy.

## Current scope and limitations
- This is a front-end starter, not a bank integration. Transactions are entered manually.
- Recommendations are rule-based summaries, not AI-generated financial advice.
- Budgets are monthly category limits.
- Savings-goal contributions update the goal balance and are not counted as expenses.
- The app uses CDN-hosted Supabase JS, Chart.js and jsPDF libraries, so an internet connection is needed.
- For a production financial product, add stronger operational controls, rate limiting/monitoring, verified email configuration, privacy policy, terms, and security review.
