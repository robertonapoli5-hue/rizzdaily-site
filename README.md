# rizzdaily-site

The public website for the **RizzDaily** Android app, served at **https://rizzdaily.com** by
GitHub Pages. Plain HTML and CSS — no framework, no build step, no external fonts or scripts.

| File | URL |
|---|---|
| `index.html` | `https://rizzdaily.com/` — landing page |
| `privacy-policy.html` | `https://rizzdaily.com/privacy-policy` — the app's Privacy Policy |
| `404.html` | shown for any unknown path |
| `assets/css/styles.css` | the only stylesheet (light and dark mode via `prefers-color-scheme`) |
| `assets/img/` | logo, favicon and touch icon |
| `CNAME` | tells GitHub Pages the custom domain (`rizzdaily.com`) |
| `.nojekyll` | serves the files as they are, without Jekyll processing |

This repository must stay **public** (GitHub Pages is free only for public repositories) and must
contain **only** the website. The app's source code lives in a separate, private repository.

---

## 1. Enable GitHub Pages

1. On GitHub, open this repository → **Settings** → **Pages**.
2. Under **Build and deployment**, set **Source** to **Deploy from a branch**.
3. Choose branch **`main`** and folder **`/ (root)`**, then **Save**.
4. After a minute the page shows *"Your site is live at …"*. Until the domain is connected it is
   reachable at `https://robertonapoli5-hue.github.io/rizzdaily-site/`.

## 2. Connect `rizzdaily.com` (domain registered at Namecheap)

**On GitHub** — Settings → Pages → **Custom domain**: enter `rizzdaily.com` and **Save**. (The
`CNAME` file in this repository already contains it, so the field is usually pre-filled.)

**On Namecheap** — Domain List → **Manage** next to `rizzdaily.com` → **Advanced DNS**:

1. **Delete** the records Namecheap adds by default: the `CNAME Record` for `www` pointing to
   `parkingpage.namecheap.com`, and the `URL Redirect Record` for `@`.
2. **Add four `A Record`s**, each with Host `@` and TTL *Automatic*:

   | Type | Host | Value |
   |---|---|---|
   | A Record | `@` | `185.199.108.153` |
   | A Record | `@` | `185.199.109.153` |
   | A Record | `@` | `185.199.110.153` |
   | A Record | `@` | `185.199.111.153` |

3. **Add one `CNAME Record`**: Host `www`, Value `robertonapoli5-hue.github.io.`

DNS changes usually apply within minutes, sometimes up to 24–48 hours. Check progress with:

```bash
dig +short rizzdaily.com
```

It should list the four `185.199.x.153` addresses.

**Turn on HTTPS** — once GitHub shows the DNS check as successful (Settings → Pages), tick
**Enforce HTTPS**. GitHub issues the certificate automatically; it can take up to an hour the
first time. Google Play and the Google Cloud consent screen require the `https://` address.

## 3. Make `/privacy-policy` publicly accessible

Nothing else is needed: GitHub Pages serves `privacy-policy.html` at **`/privacy-policy`**
(and at `/privacy-policy.html`), to everyone, with no login, from every country. To confirm:

```bash
curl -sI https://rizzdaily.com/privacy-policy
```

The first line should be `HTTP/2 200`.

Use **`https://rizzdaily.com/privacy-policy`** in:

- Google Play Console → Policy → App content → **Privacy policy**
- Google Cloud Console → OAuth consent screen → **Privacy policy link**
- the store listing, and anywhere else a privacy link is asked for

Google Play requires this page to stay **live, public, not geofenced, not a PDF, and not editable
by visitors** — keep the repository public and Pages enabled for as long as the app is published.

---

## Updating the Privacy Policy

The single source of the policy text is `docs/PRIVACY_POLICY.md` in the (private) Android
repository; the app shows an identical copy inside the app. When the policy changes:

1. Update `docs/PRIVACY_POLICY.md` in the app repository (and its in-app copy — a test there fails
   if the two differ), including the **Last updated** date.
2. Regenerate `privacy-policy.html` from it so the website, the app and Play Console always say the
   same thing, then commit and push here. GitHub Pages republishes automatically.

The developer named in the policy and in the site footer is **Level Up Solution LLC**; privacy
questions go to **contact@level-up-solution.com**. If either changes, update it in the app's policy
first, then here.
