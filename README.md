# Customs Clearing Client Portal — GitHub Pages Edition

This version is prepared for **GitHub Pages** rather than Lovable's server runtime.

## What was fixed

- Replaced Lovable/TanStack Start server deployment with a standard Vite + React SPA.
- Added a normal `index.html` and browser entry point.
- Removed Lovable-only server middleware and server entry files from the deployment path.
- Switched routing to hash URLs (`/#/admin-login`, etc.), which prevents GitHub Pages from returning 404 on refresh.
- Kept the existing UI, Tailwind design, Supabase authentication, declaration management, item/HS-code editor, payments, attachments, dashboards and CSV export.
- Added a GitHub Actions workflow that builds and publishes `dist/` to GitHub Pages automatically.
- Added `.env.example` and stopped local `.env` files from being committed.

## How to launch

1. Create a new GitHub repository.
2. Upload the **contents of this ZIP** to the repository (not the ZIP file itself).
3. Make sure the default branch is `main`.
4. Open **Settings → Pages** and select **GitHub Actions** as the source.
5. Push/commit the files. The workflow in `.github/workflows/deploy.yml` will build and publish the site.
6. After the workflow finishes, GitHub will show the Pages URL.

### Supabase authentication

The browser build contains the Supabase **publishable** client configuration needed for the frontend. Your Supabase database security must remain enforced with Row Level Security (RLS).

In Supabase, add your GitHub Pages URL under **Authentication → URL Configuration → Redirect URLs**. For example:

`https://YOUR-GITHUB-USERNAME.github.io/YOUR-REPOSITORY/`

If you later use a custom domain, add that domain too.

## Important

GitHub Pages can host the frontend, but it is not a server. If you later need server-side jobs, private service-role operations, webhooks, or server functions, those must run on a backend such as Supabase Edge Functions or another server platform.

## Local development

```bash
npm install
npm run dev
```

Then open the local URL printed by Vite.
