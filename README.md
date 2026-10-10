# Subodhmadhupati.sahityka — React + Node.js Author Website

A multi-page, responsive author website for a naval officer and writer, using a navy-blue, ivory and muted-gold visual system. The supplied author portrait and book cover are included in `client/public/images/`.

## Public website pages
- `/` — Home, featured book, author introduction and latest writing
- `/books` — Book catalogue and book enquiry
- `/about` — Author biography page
- `/journal` and `/journal/:id` — Journal index and individual entries
- `/blog` — Blog / long-form writing listing
- `/gallery` — Author and book gallery
- `/events` — Events and appearances
- `/contact` — Contact form; submissions appear in the admin panel
- `/admin/login` and `/admin` — Protected admin login and dashboard

## Admin panel features
- Dashboard counts for books, entries, messages and newsletter subscribers
- Add, edit and delete book records
- Create, edit, publish/unpublish and delete journal/blog entries
- Review and delete contact messages
- View newsletter subscribers
- Token-based admin sessions that expire after eight hours

The API stores editable content in `server/data/content.json`, which is created automatically on first run. Back up this file regularly. This lightweight JSON store is suitable for a small demo; use a database such as PostgreSQL/MySQL and stronger operational controls for a production website with multiple administrators or high traffic.

## Requirements
- Node.js 18+ (Node 20 LTS recommended)
- npm

## 1. Start the API
Open PowerShell/Terminal:
```powershell
cd server
Copy-Item .env.example .env
npm install
```
Edit `server/.env` and change `ADMIN_EMAIL`, `ADMIN_PASSWORD`, and `ADMIN_TOKEN_SECRET` before using the admin panel. Use a long random secret and a strong unique password. Never commit `.env` to a public repository.

Then start the API:
```powershell
npm run dev
```
API runs at `http://localhost:5000` by default.

## 2. Start the frontend
In a second terminal:
```powershell
cd client
npm install
npm run dev
```
Open `http://localhost:5173`.

## 3. Admin sign in
Visit `http://localhost:5173/admin/login` and use the email/password configured in `server/.env`.

## Optional Razorpay checkout
Set `RAZORPAY_KEY_ID` and `RAZORPAY_KEY_SECRET` in `server/.env`. Start with test keys, test the complete flow and configure verified webhooks before accepting real payments. Never expose the secret key to the frontend. The public site currently directs book buyers to contact the author; the API payment endpoints are retained as a foundation for a future order flow. Confirm actual prices, stock, shipping, refunds, tax, and fulfilment policy before enabling purchases.

## Before production launch
- Replace sample biography and sample journal entries with author-approved content.
- Verify book title, price, description, ISBN, stock, shipping and payment policies.
- Replace placeholder social links with official accounts and configure the verified contact email.
- Host the frontend and API on HTTPS, set `CLIENT_URL` to the real frontend origin, and configure `VITE_API_URL` at build time if needed.
- JSON persistence is not a substitute for database backups, validation/rate limiting, monitoring, and deployment hardening. Add CAPTCHA/rate limiting to public forms before production.
- Only publish approved photographs and public-facing naval/service information. Do not publish restricted operational information.

## Project layout
```text
client/
  public/images/       # supplied author portrait and book cover
  src/App.jsx          # public routes and admin panel
  src/styles.css       # responsive navy/ivory/gold styling
server/
  index.js             # REST API, admin auth, JSON content store
  data/books.js        # initial featured book record
  data/content.json    # created on first API startup; admin-managed content
  .env.example         # environment template
```
