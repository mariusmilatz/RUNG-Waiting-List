# RUNG — Waitlist landing page

Static German pre-launch waitlist page. Hosted free on **GitHub Pages**, emails captured into your **Supabase** `waitlist` table (you own the data; the list can't be read/scraped through the public API — insert-only).

## Files
- `index.html` — the page (self-contained; Supabase URL + publishable key are inline, which is safe — that key is meant for the browser).
- `assets/` — RUNG wordmark + mark (trimmed, transparent PNGs).

## Deploy to GitHub Pages (free)
1. Create a new **public** repo on GitHub, e.g. `rung-waitlist`.
2. Upload everything in this folder (keep the `assets/` folder alongside `index.html`).
   ```
   git init
   git add .
   git commit -m "RUNG waitlist landing page"
   git branch -M main
   git remote add origin https://github.com/<you>/rung-waitlist.git
   git push -u origin main
   ```
3. In the repo: **Settings → Pages → Build and deployment → Source: Deploy from a branch**, branch `main`, folder `/ (root)`. Save.
4. Wait ~1 min. Your page is live at `https://<you>.github.io/rung-waitlist/`.

## Custom domain (rung.money)
1. In **Settings → Pages → Custom domain**, enter `rung.money` (or `www.rung.money`) and save. This writes a `CNAME` file into the repo.
2. At your domain registrar, add DNS records:
   - Apex `rung.money`: four **A** records → `185.199.108.153`, `185.199.109.153`, `185.199.110.153`, `185.199.111.153`
   - or `www`: a **CNAME** → `<you>.github.io`
3. Back in Pages, tick **Enforce HTTPS** once the cert is issued.

## Checking sign-ups
The list lives in Supabase (project `ykblaaedpqdvzzzdbfdp`). View/export it in the Supabase dashboard → Table editor → `waitlist`, or via SQL:
```sql
select email, created_at, locale from public.waitlist order by created_at desc;
```
Export to CSV from the dashboard when it's time to email everyone at launch.

## TODO before going fully public (Germany)
- **Impressum + Datenschutzerklärung are legally required** in Germany for a public site collecting emails. The page links to `impressum.html` and `datenschutz.html` — those pages still need to be created with your real details (Round Circle Films / GbR). Ask Claude to generate them.
- Optional: paste your public **TestFlight** link into `TESTFLIGHT_URL` in `index.html` to show a "join the beta" button.
