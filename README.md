# Website Questionnaires

Two forms, one for each stage of closing a client.

| Stage | File | Live link | Length |
|---|---|---|---|
| **1 — after the first call** | `index.html` | https://start.webm8agency.com | ~2 min, 12 questions |
| **2 — after you close the deal** | `full/index.html` | https://start.webm8agency.com/full | ~5 min, 9 sections |

Hosted on GitHub Pages at the custom domain `start.webm8agency.com`. Repo: https://github.com/mrchreesa/website-questionnaire — once the custom domain is live, `mrchreesa.github.io/website-questionnaire` redirects to it.

## Domain setup
The domain is registered at **GoDaddy**; DNS is managed there (nameservers `ns71`/`ns72.domaincontrol.com`). The apex and `www` point at Vercel for the main agency site and are untouched by this — only the `start` subdomain comes here.

| Where | Record |
|---|---|
| GoDaddy DNS | `CNAME` &nbsp; `start` &nbsp;→&nbsp; `mrchreesa.github.io` |
| This repo | `CNAME` file containing `start.webm8agency.com` |
| GitHub | Settings → Pages → Custom domain = `start.webm8agency.com`, Enforce HTTPS on |

Leave the `CNAME` file alone — deleting it unsets the custom domain.

## Two-stage flow
1. **First call — qualify.** You tell them you'll build a small demo so they can see it rather than imagine it. Send them **https://start.webm8agency.com**. It asks only what's needed to build that demo: what they do, who for, the actions the site should drive, their existing site / socials / **Google Business Profile** (reviews, hours and photos to pull in), logo and colours, and a rough look-and-feel steer. No budget or timeline questions — those stay on the call.
2. **Second call — close.** Once the deal is signed, send **https://start.webm8agency.com/full** for the full detail: services and offerings, content readiness, technical setup, compliance, budget and timeline.

Both forms are written generically for any small business.

## How it works
1. Send your client the link for the stage you're at.
2. They fill it out in their browser (no login, nothing saves until the end — they should finish in one sitting; unsure sections can be left blank).
3. At the end they hit **Compile my answers**, then either:
   - **Download as a text file** and attach it to an email, or
   - **Copy to clipboard** and paste it into an email body, or
   - **Open an email to send it** (pre-fills a mailto to you, they still need to attach/paste the answers).
4. Either way, it's addressed to **mrchreesa@gmail.com**.

## If you want to change the destination email
It's hardcoded in **each file** in four spots — search for `mrchreesa@gmail.com` in both `index.html` and `full/index.html` and replace every match. Then:
```
git add index.html full/index.html
git commit -m "Update contact email"
git push
```
GitHub Pages will rebuild automatically (usually live within a minute or two).

## What each form covers
**`index.html` (stage 1)** — your business (name, what you do, customers, area, top 3 services), what the site needs to do (visitor actions), what they already have (website and socials, Google Business Profile, logo and colours), and look & feel (reference sites, mood, catch-all).

**`full/index.html` (stage 2)** — business basics, site goals, services/offerings (booking, shop, digital products, memberships, content, client logins), existing content, design/branding, technical setup, compliance/trust, budget/timeline, and an open-ended catch-all. Note the "Trust & compliance" section still uses medical/nutrition disclaimer wording — reword it for other industries.

## Editing the pages
Each file is self-contained (HTML/CSS/JS, no build step). Edit directly, commit, and push — no other tooling needed.

Both forms share the same stylesheet and the same compile/download/copy script. That script is generic: it walks every `.q-section[data-title]` and reads each `.field[data-question]` inside it, so **to add, remove or reorder a question you only touch the markup** — add a `<div class="field" data-question="...">` and it appears in the compiled output automatically. The one hardcoded id is `s1-bizname`, used for the filename and email subject.
