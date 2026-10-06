# Avirat Dairy

A mobile-first milk delivery web app being built stage-by-stage.

## What's in this folder (in plain language)

```
avirat-dairy/
├── src/
│   ├── app/                 → Every "page" of the website lives here (Next.js reads this folder)
│   │   ├── layout.tsx       → The wrapper around every page (fonts, mobile settings)
│   │   ├── page.tsx         → The homepage (currently a placeholder)
│   │   └── globals.css      → Site-wide styling rules
│   ├── lib/supabase/        → Reusable code that talks to your Supabase database
│   │   ├── client.ts        → Used in the browser (safe, public key only)
│   │   ├── server.ts        → Used on the server, respects the logged-in user's permissions
│   │   └── admin.ts         → Used ONLY for admin-only server jobs (bypasses security — handle with care)
│   └── types/
│       └── database.types.ts → TypeScript's map of what's in each database table
├── supabase/
│   ├── 01_schema.sql         → Creates all the database tables
│   ├── 02_rls_policies.sql   → Turns on the security rules
│   └── 03_seed_milk_types.sql → Adds your starting Cow/Buffalo milk prices
├── .env.local.example         → Template for your secret keys (copy to .env.local, see SUPABASE_SETUP.md)
├── package.json               → The list of software libraries the project needs
└── SUPABASE_SETUP.md           → Step-by-step Supabase instructions — start here
```

## How to run this on your own computer (once you reach that stage)

You'll need **Node.js** installed first (a free program that lets your
computer run this kind of project — download the "LTS" version from
https://nodejs.org if you don't have it).

Then, in a terminal, inside this folder:

```
npm install
npm run dev
```

Open http://localhost:3000 in your browser to see the app.

## Deployment

Later, this project will be connected to **Vercel** (a free hosting service
built by the same people who make Next.js) so real customers can visit it
from a real web address. That's covered in a later stage — no action needed
from you yet.

## Current stage

**Stage 1 complete:** project scaffold + Supabase database schema + security
policies. See `SUPABASE_SETUP.md` for what to do next.
