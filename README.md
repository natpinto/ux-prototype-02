# Prizm Consulting Website

This folder is the complete, self-contained code for the Prizm Consulting website. It's plain HTML/CSS with no build step, no dependencies, and no server-side code required — it can be previewed by opening the files directly, and published as-is.

## What's in here

```
website-package/
├── index.html       (Home)
├── about.html       (About)
├── services.html    (Services)
├── projects.html    (Projects)
├── careers.html     (Careers)
├── contact.html     (Contact)
├── images/          (every photo, logo, and graphic used across the site)
└── README.md        (this file)
```

Each page used to carry its images embedded directly in the code, which made the files huge and hard to read. They've since been pulled out into the `images/` folder as normal image files, and each page just references the file it needs (e.g. `<img src="images/about-the-prizm-team-reviewing-engineering-pla.jpg">`). This keeps the code readable and makes it easy to swap out a photo later — replace the file in `images/` with the same filename, no code edit needed.

## Previewing it locally

Double-clicking a file in Finder will open it in a browser and mostly work, but the contact form and application form won't behave correctly without a local server (this is a browser security restriction, not a bug). To preview it properly:

1. Open Terminal, `cd` into this folder.
2. Run `python3 -m http.server 8000`
3. Open `http://localhost:8000` in a browser.

Or use VS Code's "Live Server" extension and click "Go Live" from any of the HTML files.

## Publishing it on Cloudflare Pages

The domain (prizmland.com) is already registered with Cloudflare, so hosting and the domain live in the same account — no DNS hand-off between two different companies.

1. Log in to the Cloudflare dashboard.
2. Go to **Workers & Pages** in the left sidebar → **Create** → **Pages** → **Upload assets** (Direct Upload).
3. Name the project (e.g. `prizm-website`).
4. Drag this entire folder (or a zip of it) into the upload window and deploy.
5. Cloudflare gives you a working `*.pages.dev` URL immediately — check the live pages before connecting the real domain.
6. In the project's **Custom domains** settings, add `prizmland.com`. Since the domain is already in this Cloudflare account, the DNS records needed for the website get added automatically.
7. **Before that last step**, check the domain's existing DNS records for an MX record (this is what makes hello@prizmland.com work) and make sure it's still there afterward. Adding the site shouldn't touch it, but it's worth a 30-second look before and after, and a test email to hello@ once it's live.

Total size of this package: about 8 MB (25 images). Cloudflare's direct upload allows files up to 25 MB each and up to 1,000 files total, so this fits comfortably.

## Making updates after launch

Because this is a Direct Upload project (not connected to GitHub), a new deploy means repeating step 4 above with the updated folder — there's no automatic rebuild. If updates become frequent, moving this folder into a GitHub repository and connecting Cloudflare Pages to it would make every future change auto-deploy on save, but that's an optional upgrade, not something needed to launch.
