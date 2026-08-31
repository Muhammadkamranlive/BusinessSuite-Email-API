# BusinessSuite Email API

Standalone Express service for **Gmail/Nodemailer** sends and **HTML email templates**.  
Used by [BusinessSuite ERP](https://github.com/Muhammadkamranlive/BusinessSuite) via `EMAIL_API_URL` + `EMAIL_API_KEY`.

**This is its own git repository** — do not deploy from the main ERP monorepo.

## Deploy (Vercel)

1. Import **this repo** in Vercel as project `email-api` (root directory = `/`, not a subfolder).
2. Set environment variables (Production):

| Variable | Description |
|----------|-------------|
| `GMAIL_USER` | Sender Gmail |
| `GMAIL_APP_PASSWORD` | Google App Password |
| `MAIL_FROM` | Usually same as Gmail user |
| `MAIL_FROM_NAME` | e.g. BusinessSuite ERP |
| `EMAIL_API_KEY` | Shared secret with ERP |
| `EMAIL_DRY_RUN` | `false` for live send |

3. Deploy. Production URL example: `https://email-api-olive.vercel.app`

## Wire ERP

On the **businesssuite-erp-cloud** Vercel project:

```env
EMAIL_API_URL=https://your-email-api.vercel.app
EMAIL_API_KEY=<same as above>
```

## Local dev

```bash
cp .env.example .env
npm install
npm run dev
```

Health: `GET /health` · Send: `POST /send` · Templates: `/templates`

## Endpoints

- `GET /` — service info
- `GET /health` — mail transport check
- `POST /send` — send email (header `x-email-api-key`)
- `GET/PUT /templates` — template CRUD

See `.env.example` for all options.
