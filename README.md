# Website Discovery Questionnaire

Live form: https://mrchreesa.github.io/website-questionnaire/

Hosted via GitHub Pages, repo: https://github.com/mrchreesa/website-questionnaire

## How it works
1. Send your client that link.
2. They fill it out in their browser (~5 min, no login, nothing saves until the end — they should finish in one sitting; unsure sections can be left blank).
3. At the end they hit **Compile my answers**, then either:
   - **Download as a text file** and attach it to an email, or
   - **Copy to clipboard** and paste it into an email body, or
   - **Open an email to send it** (pre-fills a mailto to you, they still need to attach/paste the answers).
4. Either way, it's addressed to **mrchreesa@gmail.com**.

## If you want to change the destination email
It's hardcoded in `index.html` in three spots — search for `mrchreesa@gmail.com` and replace all three. Then:
```
git add index.html
git commit -m "Update contact email"
git push
```
GitHub Pages will rebuild automatically (usually live within a minute or two).

## If you want to reuse this for other clients
The sections cover: business basics, site goals, services/offerings (booking, shop, digital products, memberships, content, client logins), existing content, design/branding, technical setup, compliance/trust, budget/timeline, and an open-ended catch-all. It's written generically enough to reuse — only the "Trust & compliance" section (medical/nutrition disclaimer wording) is specific to nutrition clients.

## Editing the page
`index.html` is a single self-contained file (HTML/CSS/JS, no build step). Edit it directly, commit, and push — no other tooling needed.
