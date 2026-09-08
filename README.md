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
2. They fill it out in their browser (no login, nothing saves until they submit — they should finish in one sitting; unsure questions can be left blank).
3. At the end they enter their **name** and **email**, both required, and hit **Send my answers**.
4. The answers arrive in your inbox as formatted text, with the client's address set as **reply-to** — so hitting reply in Gmail goes straight to them.

If the send fails (offline, service down, blocked by an extension), the page shows the compiled answers with a **Copy to clipboard** button and asks them to email it instead, so a failed submission never loses a lead.

## Email delivery (Web3Forms)
Submissions go through [Web3Forms](https://web3forms.com), which is what lets a static site send email with no backend.

- The **access key** sits in `var ACCESS_KEY` at the top of the `<script>` block in each file. It is public by design — Web3Forms' docs state it can be exposed, and it must be, since it ships in client-side HTML.
- **The destination email is tied to the key, not the page.** To change where submissions land, generate a new key at web3forms.com with the new address and swap the value in both files.
- The key cannot be abused from a script: Web3Forms rejects non-browser submissions on the free plan and sits behind Cloudflare.
- A hidden `botcheck` honeypot is included. If spam ever gets through, hCaptcha is available on the free tier; the **Restrict to Domain** whitelist is a PRO feature.

Sent fields: `access_key`, `subject` (`Website brief — <business>`), `from_name`, `replyto`, `message` (the compiled Q&A), POSTed as JSON to `https://api.web3forms.com/submit`.

`mrchreesa@gmail.com` still appears in each file twice, but only in the **failure fallback** text — the address shown if a submission fails. Normal submissions don't use it.

## What each form covers
**`index.html` (stage 1)** — your business (name, what you do, customers, area, top 3 services), what the site needs to do (visitor actions), what they already have (website and socials, Google Business Profile, logo and colours), and look & feel (reference sites, mood, catch-all).

**`full/index.html` (stage 2)** — business basics, site goals, services/offerings (booking, shop, digital products, memberships, content, client logins), existing content, design/branding, technical setup, compliance/trust, budget/timeline, and an open-ended catch-all. Note the "Trust & compliance" section still uses medical/nutrition disclaimer wording — reword it for other industries.

## Editing the pages
Each file is self-contained (HTML/CSS/JS, no build step). Edit directly, commit, and push — no other tooling needed.

Both forms share the same stylesheet and the same compile/submit script. That script is generic: it walks every `.q-section[data-title]` and reads each `.field[data-question]` inside it, so **to add, remove or reorder a question you only touch the markup** — add a `<div class="field" data-question="...">` and it appears in the compiled output automatically. The one hardcoded id is `s1-bizname`, used for the filename and email subject.
