# Setting Up Your Website

*A simple, secure starting point — hosting, site structure, and getting the contact form right*

This is a straightforward way to get a website live: free hosting, a clean file structure, and a bit of extra care around the contact form. None of it requires paying for hosting, and none of it requires learning a framework — the whole site can be plain HTML, CSS, and JavaScript.

---

## Decisions made for this site

This guide was a starting reference, not the final word — here's what was actually decided for yaakovbolel.co.za, which may differ from the generic advice below:

- **Contact form:** dual submission — the same "Send Message" click opens WhatsApp *and* submits to Formspree by email. Not WhatsApp-only, not Formspree-only.
- **Cloudflare:** skipped. Not in front of the site.
- **Analytics:** none. No Plausible, no Fathom, no tracking of any kind.
- **Hosting/domain:** live at both `www.yaakovbolel.co.za` and `yaakovbolel.co.za`, deploying from the `claude/google-drive-website-folder-7cv93c` branch (not `main`).

---

## 1. Hosting: GitHub Pages

GitHub Pages is free hosting built directly into a GitHub repository. It's a great fit for a small, simple site like this — no server to manage, no hosting bill.

### Getting the site live
- Create a plain repository on GitHub for the site.
- Go to **Settings → Pages** and set it to deploy from a branch (usually **main**, from either the root folder or a **/docs** folder).
- That's it — GitHub automatically rebuilds and republishes the site every time changes are pushed.

### Using a custom domain
- Add a file named **CNAME** to the root of the repo, containing just the domain name (e.g. `yoursite.com`).
- At the domain registrar, point the apex domain to GitHub's published Pages IP addresses (listed in GitHub's Pages documentation) as A records, and point **www** to `<username>.github.io` as a CNAME record.
- Once the DNS change has propagated, go back to the Pages settings and tick **Enforce HTTPS**. GitHub issues a free SSL certificate automatically.

### Optional: an extra layer with Cloudflare
- Cloudflare's free plan can sit in front of the site (DNS-only or "proxied") to add basic DDoS protection and a web application firewall.
- It's also the way to add security headers — Content-Security-Policy, X-Frame-Options, Referrer-Policy — that GitHub Pages doesn't let you set directly, via a Cloudflare Transform Rule or Worker.
- This step is entirely optional. The site works fine without it.

---

## 2. Keep the Site Structure Simple

- For a handful of pages, skip frameworks and build tools entirely — plain HTML, CSS, and JavaScript is easier to write and easier to edit. Repeat the shared header and footer on each page by hand; a build step is only worth it if the site grows to many pages.
- Keep the repository public. GitHub Pages requires a public repo unless you're paying for GitHub Pro/Team (which supports private Pages). Being public just means: **never commit anything sensitive** — no client names, no real emails or phone numbers you don't want scraped, and no API keys or `.env` files, ever.
- Add a **.gitignore** file from day one, even before there's anything to ignore. It costs nothing now and stops future tools from accidentally leaking junk into the commit history later.

---

## 3. The Contact Form — Handle With Care

GitHub Pages only serves static files, so a working contact form needs an outside service to actually receive submissions.

- Use a form backend such as **Formspree**, **Netlify Forms**, or **Getform** — all have free tiers and need no server of your own.
- Add a honeypot field or hCaptcha to cut down on spam submissions.

> **If this site is for something like a therapy or health practice**, add a clear line near the form, such as: *"This form is not for urgent matters or clinical information. If you're in crisis, please call [local crisis line]."* This is standard practice for practitioner websites — it protects visitors and reduces liability, since a plain contact form has no guarantee of encryption or secure storage.

- If real appointment booking or client intake is needed — not just a "get in touch" message — use a proper practice-management platform instead (e.g. SimplePractice, TherapyNotes, Jane), rather than building anything custom. Those tools are built to handle that kind of data properly; a GitHub Pages site shouldn't be asked to.

---

## 4. Privacy Basics

- Add a short Privacy Policy page explaining what the contact form collects, that it isn't for clinical information, and whether any analytics tool is used.
- Skip Google Analytics. For a site whose visitors may be researching something sensitive, a privacy-respecting alternative — **Plausible**, **Fathom**, or no analytics at all — is a better fit. Third-party trackers on that kind of traffic carry real privacy weight.

---

## 5. A Little Repo Hygiene

- Branch protection isn't necessary for a one-person project, but two free safety nets are worth switching on in the repo settings: **Dependabot alerts** (flags outdated or vulnerable dependencies) and **secret scanning** (on by default for public repos, but worth confirming).

None of this requires ongoing cost or a background in web development. The whole setup comes down to: a free GitHub repo, a domain pointed at it, a form service for the contact page, and a bit of care about what gets shared publicly.

---

## Quick Checklist (actual status for this site)

- [x] Create the GitHub repo and enable Pages
- [x] Add the CNAME file and point the domain's DNS at GitHub
- [ ] Tick "Enforce HTTPS" in Pages settings — waiting on GitHub to finish issuing the certificate
- [x] Add a .gitignore file
- [x] Set up the contact form — WhatsApp + Formspree, both fire on the same click (needs a real Formspree form ID dropped into `index.html` to go live — see `FORMSPREE_ENDPOINT` near the bottom of the file)
- [x] Add a crisis-line disclaimer near the form
- [x] Add a Privacy Policy page
- [ ] Turn on Dependabot alerts and confirm secret scanning — confirmed currently OFF, needs a manual toggle in repo settings
- [x] Cloudflare — decided against, skipped
- [x] Analytics — decided against, none in use
