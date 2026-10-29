# Tree Inspect website

Simple static site for the Tree Inspect app, hosted free on GitHub Pages.
No build step, no scripts, no trackers – just plain HTML and one CSS file.

| File | Page |
| --- | --- |
| `index.html` | Home page (company, app description, contact) |
| `privacy.html` | Privacy Policy |
| `terms.html` | Terms of Use (incl. subscription terms and Apple Standard EULA) |
| `style.css` | Shared styling |

Live (until a custom domain is added): https://kv17294691739.github.io/treeinspect-site/

## 1. Fill in the placeholders

Placeholders are in square brackets and appear on all three pages (footer and contact sections):

| Placeholder | Replace with |
| --- | --- |
| `[Company Name]` | Company name exactly as on the Companies House certificate, **without** "Ltd" (the pages already add " Ltd"). If your name ends in "Limited", change the text after it too. |
| `[Company number]` | The 8-digit company number from the certificate |
| `[Registered office address]` | The company's registered office. This is public on Companies House anyway – use a registered-office / virtual-office service or your accountant's address if you don't want your home address shown. |

Also check:
- **Contact email** – currently `kv17294691739@gmail.com` (the address in the existing privacy policy). Once you have the domain, a domain address such as `support@yourdomain` looks more professional. Find/replace it on all pages.
- **Store badges** – `index.html` says "App Store – coming soon" / "Google Play – coming soon". Replace with real links when the listings are public.
- **"Last updated"** dates at the top of `privacy.html` and `terms.html` whenever you change them.

### Easiest way: edit on GitHub (works from a phone)
Open the file on github.com → pencil icon (Edit) → change the text → **Commit changes**. The site updates in about a minute.

### Replace everything at once (on a computer with git)
```bash
git clone https://github.com/kv17294691739/treeinspect-site.git
cd treeinspect-site
sed -i 's/\[Company Name\]/Acme Trees/g; s/\[Company number\]/12345678/g; s/\[Registered office address\]/1 Example Street, London, AB1 2CD/g' *.html
git commit -am "Fill in company details" && git push
```
(On a Mac use `sed -i ''` instead of `sed -i`.)

## 2. Add your custom domain

Do these in this order (GitHub recommends adding the domain in GitHub **before** creating DNS records):

1. *(Recommended)* Verify the domain for your account: GitHub → your profile picture → **Settings → Pages → Add a domain**. GitHub shows a TXT record to add at your registrar. This stops anyone else using your domain on GitHub.
2. In this repo: **Settings → Pages → Custom domain**, type `yourdomain.co.uk`, **Save**. (This creates a `CNAME` file in the repo automatically – don't create it by hand.)
3. At your domain registrar's DNS settings, delete any default/parking A, AAAA or CNAME records for `@` and `www`, then add:

| Type | Name / Host | Value |
| --- | --- | --- |
| A | `@` | `185.199.108.153` |
| A | `@` | `185.199.109.153` |
| A | `@` | `185.199.110.153` |
| A | `@` | `185.199.111.153` |
| CNAME | `www` | `kv17294691739.github.io` |

   Optional IPv6 (AAAA, name `@`): `2606:50c0:8000::153`, `2606:50c0:8001::153`, `2606:50c0:8002::153`, `2606:50c0:8003::153`.
   Don't use a wildcard (`*`) record. On Cloudflare, set the records to **DNS only** (grey cloud) at least until HTTPS is issued.

4. Wait for DNS (minutes to 24 hours). Back in **Settings → Pages**, tick **Enforce HTTPS** once it becomes available.
5. Your pages are then:
   - `https://yourdomain.co.uk/`
   - `https://yourdomain.co.uk/privacy.html`
   - `https://yourdomain.co.uk/terms.html`

   Use these in App Store Connect (Privacy Policy URL, and the Terms link in the description), Google Play Console (Privacy policy, website) and in the app's paywall links.

## Notes
- This repo is **public** (required for free GitHub Pages). Never put passwords, keys or private information in it.
- Docs: https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site
