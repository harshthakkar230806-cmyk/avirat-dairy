# Supabase Setup Guide (Stage 1)

Follow these steps in order. Nothing here requires writing code — you're just
clicking buttons on the Supabase website and pasting text into one box.

## Step 1 — Create your Supabase account and project

1. Go to https://supabase.com and click **Start your project**.
2. Sign up (GitHub or email both work).
3. Click **New project**.
4. Fill in:
   - **Name**: `avirat-dairy` (or anything you like)
   - **Database Password**: click "Generate a password" and **save it somewhere safe** (a notes app). You won't need to type this often, but keep it.
   - **Region**: pick the one closest to your customers (e.g. Mumbai/Singapore if you're in India).
5. Click **Create new project**. Wait 1–2 minutes while it sets up.

## Step 2 — Run the database schema

1. In your new Supabase project, look at the left sidebar and click the icon that looks like `>_` labelled **SQL Editor**.
2. Click **New query**.
3. Open the file `supabase/01_schema.sql` (I've written this for you), select all its text, copy it, and paste it into the SQL Editor box.
4. Click **Run** (bottom right, or press Ctrl+Enter / Cmd+Enter).
5. You should see "Success. No rows returned." That means all your tables were created.

## Step 3 — Turn on security (Row Level Security)

1. Still in the SQL Editor, click **New query** again (this keeps things clean).
2. Open `supabase/02_rls_policies.sql`, copy all of it, paste it in.
3. Click **Run**.
4. You should again see "Success."

This step is critical — it's what guarantees one customer can never see another
customer's orders or bills, even by accident.

## Step 4 — Add your real milk types and prices

1. Open `supabase/03_seed_milk_types.sql`.
2. **Edit the two numbers** (60.00 and 80.00) to your actual current prices per litre for Cow Milk and Buffalo Milk.
3. Copy the edited file into a new SQL Editor query and click **Run**.

You can always change these prices later from the app itself (in a future
stage) — this is just to get you started with real numbers instead of empty
tables.

## Step 5 — Turn on the sign-in methods you want customers to use

1. In the left sidebar, click **Authentication**, then **Providers** (or **Sign In / Providers**, depending on the Supabase version).
2. Find **Email** and make sure it's turned **on**.
3. If you also want customers to log in with their **phone number** (SMS OTP), find **Phone** and turn it on. Phone login requires connecting an SMS provider (like Twilio) later — email login alone is enough to get started, and we can add phone login in a later stage without breaking anything.

## Step 6 — Collect the three keys the app needs

1. In the left sidebar, click the gear icon **Project Settings**, then **API**.
2. You'll see three values. Keep this page open, you'll copy these in a moment:
   - **Project URL** — looks like `https://xxxxxxxxxxxx.supabase.co`
   - **anon public** key — a long string of letters/numbers
   - **service_role** key — another long string (⚠️ never share this one, never put it in any public file)

## Step 7 — Put those keys into your project (on your computer)

1. On your computer, inside the `avirat-dairy` project folder, find the file named `.env.local.example`.
2. Make a **copy** of it and rename the copy to exactly `.env.local` (no ".example").
3. Open `.env.local` in any text editor and paste in the three values from Step 6, so it looks like:
   ```
   NEXT_PUBLIC_SUPABASE_URL=https://xxxxxxxxxxxx.supabase.co
   NEXT_PUBLIC_SUPABASE_ANON_KEY=eyJhbGciOि...(long string)
   SUPABASE_SERVICE_ROLE_KEY=eyJhbGciOि...(a different long string)
   ```
4. Save the file. **Never** commit or upload this file anywhere public — it's already excluded from git via `.gitignore`, so this happens automatically if you use git/GitHub later.

## ✅ Checklist before moving to Stage 2

Go through this list and make sure every box is true:

- [ ] Supabase project created and "active" (green dot) on your Supabase dashboard
- [ ] Ran `01_schema.sql` successfully — no red error text
- [ ] Ran `02_rls_policies.sql` successfully — no red error text
- [ ] In **Table Editor** (left sidebar), you can see these 7 tables: `profiles`, `milk_types`, `recurring_orders`, `recurring_order_skips`, `orders`, `bills`, `payments`
- [ ] `milk_types` table has 2 rows (Cow Milk, Buffalo Milk) with your real prices
- [ ] Email sign-in is turned on under Authentication → Providers
- [ ] You have your Project URL, anon key, and service_role key saved somewhere
- [ ] `.env.local` file created on your computer with those 3 values pasted in

Once every box above is checked, tell me and we'll move to **Stage 2: user
sign-up/login pages + the customer/admin profile system.**
