# Nora — Legal site

Static HTML for Nora's public **Privacy Policy** and **Terms & Conditions**, designed for GitHub Pages.

## Files

```
legal/
├── index.html                 ← Landing page (links to both docs)
├── privacy-policy.html        ← Privacy Policy
├── terms-and-conditions.html  ← Terms & Conditions
├── 404.html                   ← Friendly 404 page
├── styles.css                 ← Shared stylesheet (brand peach #EEA081)
├── .nojekyll                  ← Tells GitHub Pages to serve files as-is
└── README.md
```

Pure HTML + CSS. No JS, no build step.

---

## Deploy to GitHub Pages

You have two clean options. Pick one.

### Option A — Dedicated repo (recommended)

A separate repo for the legal site keeps it independent of the iOS app and gives you a tidy URL.

1. Create a new public GitHub repo, e.g. `nora-legal` (or `nora-app-legal`).
2. From inside this `legal/` folder, push it as the repo's root:
   ```bash
   cd legal
   git init
   git add .
   git commit -m "Initial: Nora privacy policy and terms"
   git branch -M main
   git remote add origin https://github.com/<your-username>/nora-legal.git
   git push -u origin main
   ```
3. On GitHub: **Settings → Pages → Source: `main` / root → Save**.
4. Wait ~30s. Your site is live at:
   ```
   https://<your-username>.github.io/nora-legal/
   https://<your-username>.github.io/nora-legal/privacy-policy.html
   https://<your-username>.github.io/nora-legal/terms-and-conditions.html
   ```

### Option B — `docs/` folder of the main Nora repo

If you'd rather keep one repo, copy this folder to `docs/` at the root of your iOS repo:

```bash
cp -R legal/. docs/
git add docs && git commit -m "Add legal site"
git push
```

Then on GitHub: **Settings → Pages → Source: `main` / `/docs` → Save**.

URL becomes:
```
https://<your-username>.github.io/<repo-name>/
```

---

## App Store Connect URLs to paste

After deploying, App Store Connect needs these exact URLs in:

- **App Privacy → Privacy Policy URL**
- **App Information → License Agreement** (optional — Apple's default EULA covers most apps)
- **In-App Purchase → Review Information → Terms of Use (EULA) URL** (if you ship a custom EULA)

Paste the deployed URLs from above.

---

## Updating the docs

The source of truth for the language is the iOS app's bundled text:

- `Nora/Features/Legal/Documents/privacy-policy.txt`
- `Nora/Features/Legal/Documents/terms-and-conditions.txt`

When you change either of those, mirror the change here so the in-app and web versions stay in sync. Bump the `Last updated` and `Effective` dates in both the HTML files and the bundled text files.

---

## Local preview

Just open the files in your browser — no server needed:

```bash
open index.html
```

Or run a tiny local server if you want clean URLs:

```bash
cd legal
python3 -m http.server 4001
# visit http://localhost:4001
```

---

## Custom domain (optional)

If you'd rather use e.g. `legal.norahairapp.com`:

1. Add a `CNAME` file inside `legal/` containing exactly `legal.norahairapp.com`.
2. In your DNS provider, add a `CNAME` record pointing `legal` → `<your-username>.github.io`.
3. On GitHub: **Settings → Pages → Custom domain → enter the domain → Enforce HTTPS**.

Wait a few minutes for the certificate to provision, then update App Store Connect to the new domain.
