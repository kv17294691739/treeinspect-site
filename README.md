# Tree Inspect website

Simple static site for the Tree Inspect app, hosted free on GitHub Pages.
No build step, no scripts, no trackers – just plain HTML and one CSS file.

| File | Page |
| --- | --- |
| `index.html` | Home page (company, app description, contact) |
| `privacy.html` | Privacy Policy |
| `terms.html` | Terms of Use (incl. subscription terms and Apple Standard EULA) |
| `style.css` | Shared styling |

Live at https://movingtree.download/ (custom domain; set in Settings → Pages). Before DNS is set up, https://kv17294691739.github.io/treeinspect-site/ redirects there.

## 1. Company details

The pages show **Moving Tree Ltd**, registered office **82A James Carter Road, Mildenhall, IP28 7DE, United Kingdom** (in the footer of all three pages, section 1 and section 15 of `privacy.html`, and the intro and section 14 of `terms.html`).

### Add the company number later
The company is still being registered, so the number is not shown yet. When Companies House issues it, add ` (company number 12345678)` straight after "a company registered in England and Wales" in these places:
- the footer of `index.html`, `privacy.html` and `terms.html`
- section 1 of `privacy.html`

Or on a computer with git:
```bash
sed -i 's/a company registered in England and Wales/a company registered in England and Wales (company number 12345678)/g' *.html
```
(On a Mac use `sed -i ''`.) Then commit and push. Each page has a comment near the top as a reminder.

Also check:
- **Contact email** – currently `kv17294691739@gmail.com`. A domain address such as `support@movingtree.download` looks more professional. Find/replace it on all pages.
- **Store badges** – `index.html` says "App Store – coming soon" / "Google Play – coming soon". Replace with real links when the listings are public.
- **"Last updated"** dates at the top of `privacy.html` and `terms.html` whenever you change them.

### Editing from a phone
Open the file on github.com → pencil icon (Edit) → change the text → **Commit changes**. The site updates in about a minute.

## 2. Add your custom domain

Do these in this order (GitHub recommends adding the domain in GitHub **before** creating DNS records):

1. *(Recommended)* Verify the domain for your account: GitHub → your profile picture → **Settings → Pages → Add a domain**. GitHub shows a TXT record to add at your registrar. This stops anyone else using your domain on GitHub.
2. In this repo: **Settings → Pages → Custom domain**, type `movingtree.download` (already done), **Save**. (This creates a `CNAME` file in the repo automatically – don't create it by hand.)
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
   - `https://movingtree.download/`
   - `https://movingtree.download/privacy.html`
   - `https://movingtree.download/terms.html`

   Use these in App Store Connect (Privacy Policy URL, and the Terms link in the description), Google Play Console (Privacy policy, website) and in the app's paywall links.

## Notes
- This repo is **public** (required for free GitHub Pages). Never put passwords, keys or private information in it.
- Docs: https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site
