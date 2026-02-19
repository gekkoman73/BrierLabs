# BrierLabs

Simple landing page for [BrierLabs](https://brierlabs.io).

## Run locally

Open `index.html` in a browser, or use a local server:

```bash
# Python
python3 -m http.server 8000

# Node (npx)
npx serve .
```

Then visit `http://localhost:8000`.

---

## Deploy with GitHub Pages + Cloudflare

### 1. Create the GitHub repo and push

```bash
git init
git add .
git commit -m "Initial BrierLabs landing page"
git branch -M main
git remote add origin https://github.com/gekkoman73/BrierLabs.git
git push -u origin main
```

The repo is already created at `https://github.com/gekkoman73/BrierLabs.git`.

### 2. Turn on GitHub Pages

- Repo → **Settings** → **Pages**
- **Source**: Deploy from a branch
- **Branch**: `main` / root (or `/ (root)`)
- **Save**

GitHub will serve the site at `https://gekkoman73.github.io/BrierLabs/`.

### 3. Set custom domain in GitHub

- Still in **Settings** → **Pages**
- **Custom domain**: `brierlabs.io`
- Check **Enforce HTTPS** (after DNS is set)
- Save

### 4. Point Cloudflare to GitHub

In [Cloudflare Dashboard](https://dash.cloudflare.com) → your zone **brierlabs.io** → **DNS** → **Records**:

| Type  | Name       | Content                    | Proxy |
|-------|------------|----------------------------|-------|
| CNAME | `@` (apex) | `YOUR_USERNAME.github.io`  | Proxied (orange) or DNS only |
| CNAME | `www`      | `YOUR_USERNAME.github.io`  | Proxied or DNS only          |

- For **apex** (`brierlabs.io`), Cloudflare’s CNAME flattening lets you use a CNAME on `@`; if your plan doesn’t support it, use GitHub’s A records instead (see [GitHub’s custom domain docs](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site)).
- Replace `YOUR_USERNAME` with your GitHub username (and use the same value as in your GitHub Pages URL).

Wait a few minutes for DNS to propagate, then visit `https://brierlabs.io`. HTTPS will work once GitHub has validated the domain; you can then enable **Enforce HTTPS** in GitHub Pages.

---

## Edit the site

- **Content**: `index.html` (headline, tagline, about, contact email).
- **Styling**: `styles.css` (colors, fonts, layout).

After changes, commit and push to `main`; GitHub Pages will redeploy automatically.
