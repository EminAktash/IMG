# IMG Editors — Website

Static site (plain HTML/CSS/JS). No build step, no framework. Drops straight onto Vercel.

## Files
```
index.html      → Home page (hero, stats, expert, pricing, FAQ, contact form)
book.html       → "Book a Call" page (Calendly embed + ebooks). Hero "Learn More" links here.
styles.css      → All styling (shared by both pages)
assets/         → Images
  hero-doctors.png
  debra.jpg
```

---

## ⚠️ ONE thing to know about the contact form

The form on `index.html` is set to **mailto**: when a visitor clicks "Send Inquiry," it opens
their email app with a message pre-filled to **d.anazonwu@gmail.com** containing all their answers.
This works the moment you upload — no setup, no signup.

Tradeoff: mailto relies on the visitor having an email app configured on their device, and it does
**not** save leads on a server. If you want submissions to land in your inbox automatically every
time (regardless of the visitor's setup), upgrade to Formspree:
1. https://formspree.io → sign up → New Form → use `d.anazonwu@gmail.com`, copy the form ID.
2. In `index.html`, change the form tag from `<form class="form-card reveal" id="inquiryForm">`
   to `<form class="form-card reveal" action="https://formspree.io/f/YOUR_ID" method="POST">`
   and delete the "Contact form -> open email client" script block near the bottom.

### Calendly is already wired
`book.html` embeds `https://calendly.com/d-anazonwu`. It won't show when you open the file
locally (needs a real https domain) but renders fine once live on Vercel.

---

## Deploy: GitHub → Vercel → your domain

### A. Push to GitHub
1. Create a new repo on GitHub (e.g. `imgeditors`).
2. From this folder:
   ```bash
   git init
   git add .
   git commit -m "IMG Editors site"
   git branch -M main
   git remote add origin https://github.com/YOUR_USERNAME/imgeditors.git
   git push -u origin main
   ```
   (Or just drag-and-drop all files into the repo via GitHub's web "Add file → Upload files".)

### B. Deploy on Vercel
1. Go to https://vercel.com → **Add New → Project** → import your GitHub repo.
2. Framework Preset: **Other** (it's a static site — leave build settings empty).
3. Click **Deploy**. You'll get a `something.vercel.app` URL in ~30 seconds.

### C. Connect your domain
1. In the Vercel project → **Settings → Domains** → add your domain.
2. Vercel shows you DNS records (an `A` record and/or `CNAME`).
3. Add those records at your domain registrar (GoDaddy, Namecheap, etc.).
4. Wait for it to verify (minutes to a couple hours). SSL is automatic.

Done.

---

## Editing copy / prices later
Everything is plain text in `index.html` and `book.html`. Change a price, a feature line, or
the FAQ answers right in the HTML and re-push to GitHub — Vercel redeploys automatically.

The FAQ answers were written to match your service (the live site had them collapsed, so I couldn't
copy them verbatim). Read them in `index.html` and tweak to your exact wording if needed.
