# Deploy tolias.online to Cloudflare Pages

A complete, beginner-friendly walkthrough. ~15 minutes start to finish.

You'll do this in **3 phases**:

1. Put your code in GitHub (so Cloudflare can pull from it)
2. Connect Cloudflare Pages to that repo
3. Point your `tolias.online` domain at the site

---

## Phase 1 — Put your site on GitHub

### 1.1 Create a free GitHub account
If you don't have one: go to https://github.com/signup and create an account.

### 1.2 Create a new empty repository
1. Go to https://github.com/new
2. **Repository name:** `tolias-online`
3. **Visibility:** Public (free Pages + simpler) or Private (also works)
4. Leave everything else blank (no README, no .gitignore, no license)
5. Click **Create repository**

### 1.3 Upload the site files
The easiest way for a first-timer is the web uploader:

1. On your new empty repo page, click **uploading an existing file** (the link in the quick-setup box).
2. Open Finder on your Mac and go to `/Users/nick/Documents/Clawpilot/tolias-online/`
3. Drag **all the files inside that folder** (not the folder itself) into the GitHub upload area:
   - `index.html`
   - `README.md`
   - `DEPLOY.md`
   - `assets/` folder (drag the whole folder — it contains `profile.jpg`)
4. Scroll down → commit message: `Initial site` → click **Commit changes**.

✅ Your code is now on GitHub.

---

## Phase 2 — Connect Cloudflare Pages

### 2.1 Create a free Cloudflare account
If you don't have one: https://dash.cloudflare.com/sign-up

### 2.2 Add tolias.online to Cloudflare (DNS)
This is so Cloudflare can manage your domain. You'll need to do this **once**, regardless of where you bought the domain.

1. In the Cloudflare dashboard, click **+ Add a domain** (or **Websites** → **Add a site**).
2. Enter `tolias.online` and click **Continue**.
3. Choose the **Free** plan → Continue.
4. Cloudflare will scan your existing DNS records. Click **Continue**.
5. Cloudflare will show you **2 nameservers** (e.g. `xxx.ns.cloudflare.com` and `yyy.ns.cloudflare.com`). **Copy these.**
6. Now go to **wherever you bought tolias.online** (Namecheap, GoDaddy, Porkbun, etc.), log in, find domain DNS settings, and **replace the existing nameservers with the two Cloudflare ones**. Save.
7. Back in Cloudflare, click **Done, check nameservers**. DNS propagation can take from a few minutes up to 24 hours, but is usually fast.

> You can continue with Phase 2.3 even while waiting for nameservers to propagate.

### 2.3 Create the Cloudflare Pages project
1. In Cloudflare dashboard left sidebar → **Workers & Pages**.
2. Click **Create application** → **Pages** tab → **Connect to Git**.
3. Click **Connect GitHub**, authorize Cloudflare, select your `tolias-online` repo.
4. **Set up builds and deployments:**
   - **Project name:** `tolias-online` (this becomes `tolias-online.pages.dev`)
   - **Production branch:** `main`
   - **Framework preset:** **None**
   - **Build command:** *(leave empty)*
   - **Build output directory:** *(leave empty, or put `/`)*
5. Click **Save and Deploy**.
6. Wait ~30 seconds. You'll see a deployment running. When done, you'll get a URL like `https://tolias-online.pages.dev` — open it. **Your site is live!** 🎉

---

## Phase 3 — Point tolias.online at the site

### 3.1 Add the custom domain in Cloudflare Pages
1. In your Pages project → **Custom domains** tab → **Set up a custom domain**.
2. Enter `tolias.online` → **Continue** → **Activate domain**.
3. Cloudflare auto-creates the DNS record because your domain is already on Cloudflare. ✅
4. Repeat for `www.tolias.online` if you want both to work.

That's it. Within a minute or two, **https://tolias.online** will load your site, with a free auto-renewing HTTPS certificate from Cloudflare.

---

## Updating your site later

Edit `index.html`, then on the GitHub repo page:
1. Click the file → pencil icon → make changes → **Commit changes**.

OR upload a new version: **Add file** → **Upload files** → drag new `index.html` → commit.

Cloudflare Pages auto-rebuilds in ~20 seconds. Refresh tolias.online.

---

## Optional: set up a real email at hello@tolias.online

The site lists `hello@tolias.online` as the contact email. To actually receive mail there:

1. In Cloudflare dashboard → your `tolias.online` domain → **Email** → **Email Routing**.
2. Click **Get started**.
3. Add a custom address: `hello` → forwards to → `your-real-personal-email@gmail.com`.
4. Cloudflare will auto-add the required DNS records. Approve them.
5. Click the verification email Cloudflare sends to your real email.

Done. Email sent to `hello@tolias.online` lands in your normal inbox. Free.

---

## Troubleshooting

**"My domain still shows my old registrar page"**
→ Nameservers haven't propagated yet. Wait a few hours. Check status: https://www.whatsmydns.net/#NS/tolias.online

**"Cloudflare Pages says 'Build failed'"**
→ You probably set a build command or framework. Go to Pages project → Settings → Builds & deployments → make sure **Framework preset = None** and **Build command** is empty.

**"My profile photo is broken"**
→ Make sure `assets/profile.jpg` was uploaded into an `assets/` folder, not at the top level.

**"I want to change something but I'm scared"**
→ GitHub keeps full history. Every change is reversible from the **Commits** tab. You literally cannot break anything permanently.
