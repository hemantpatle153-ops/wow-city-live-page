# WowCity website

The public website for WowCity, with five pages: Home, Services, Why us, Download and Contact (Join), plus a 404 page.

It is plain HTML, CSS and JavaScript, so there is no framework and nothing to install. It runs on any static host, including InfinityFree, GitHub Pages and Cloudflare Pages.

## Change the content

| What | Where |
|---|---|
| Phone, WhatsApp, email, support hours, app links, domain | `src/site.json` |
| Page text | `src/pages/*.html` |
| Header, footer, FAQ, the "Join us today" band | `src/partials/*.html` |
| Colours, fonts, animations | `src/assets/css/style.css` |
| Interactions (billing demo, form, tabs, menu) | `src/assets/js/main.js` |

A WhatsApp number or phone number left empty in `src/site.json` is simply hidden. Write numbers with the country code, for example `+91 98765 43210`.

## Build and preview

```bash
node build.mjs --check   # builds dist/ and fails on any broken link
node serve.mjs           # preview at http://localhost:4173
```

## Deploy

Every push to `main` runs `.github/workflows/deploy.yml`, which does three things:

1. **Builds** the site and checks every link.
2. **Publishes a preview to GitHub Pages.** Turn this on once under Settings → Pages → Source: **GitHub Actions**.
3. **Uploads to InfinityFree over FTP.** This step runs only after you add three repository secrets under Settings → Secrets and variables → Actions:
   - `FTP_SERVER`, for example `ftpupload.net`
   - `FTP_USERNAME`, for example `if0_12345678`
   - `FTP_PASSWORD`, your InfinityFree FTP password

   All three are on the InfinityFree control panel under **FTP Details**.

**Deploying by hand:** open the workflow run, download the `website-htdocs` artifact, and upload its contents (including `.htaccess`) into `htdocs` using InfinityFree's File Manager.

## Join form

The Join form sends each request to the email address in `src/site.json` through [FormSubmit](https://formsubmit.co), which is free and needs no server.

- **First submission:** FormSubmit emails that address an activation link. Click it once, and from then on every request arrives as an email.
- **WhatsApp:** if a WhatsApp number is set, the form opens a prefilled WhatsApp chat whenever email sending fails.
