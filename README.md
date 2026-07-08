# Block HQ

A shared, no-login workspace for the block: case digest maker, digest library, case tracker, assignments, and notes.

This is a single static `index.html` file — no build step, no backend to manage. Data is stored in Supabase (shared, no login).

## Database setup (Supabase)

Run this once in the Supabase SQL Editor for this project:

```sql
create table block_hq (
  key text primary key,
  value jsonb not null,
  updated_at timestamptz default now()
);

alter table block_hq enable row level security;

create policy "Anyone can read" on block_hq for select using (true);
create policy "Anyone can write" on block_hq for insert with check (true);
create policy "Anyone can update" on block_hq for update using (true);
create policy "Anyone can delete" on block_hq for delete using (true);
```

## Deploy on Vercel

1. Push this folder to a new GitHub repo (see below).
2. Go to https://vercel.com/new
3. Import the GitHub repo.
4. Framework preset: **Other** (or leave as detected — it's a static site).
5. Leave build command empty, output directory as root (`.`).
6. Click **Deploy**.

Vercel will give you a live URL like `block-hq.vercel.app` — share that with your block.

## Push to GitHub (first time)

```bash
cd block-hq
git init
git add .
git commit -m "Initial commit: Block HQ"
git branch -M main
git remote add origin https://github.com/YOUR_USERNAME/block-hq.git
git push -u origin main
```

Replace `YOUR_USERNAME` with your GitHub username, and create the empty repo on github.com first (no README/gitignore, so it doesn't conflict with this push).

## Updating later

Any time you or a classmate wants to change the app, edit `index.html` and:

```bash
git add .
git commit -m "Update"
git push
```

Vercel auto-redeploys on every push to `main`.
