# Watan Designs — Vercel Deployment

This folder contains everything needed to deploy the QR landing page to Vercel.

## Files

- `index.html` — the landing page
- `vercel.json` — security headers + short cache config
- `README.md` — this file

## Deploy method 1: Drag-and-drop (fastest, no terminal)

1. Go to https://vercel.com — sign up or sign in (GitHub login is fine)
2. Click **Add New → Project**
3. On the import screen, scroll down to the section that says **"Deploy a template"** or look for **"Or browse to upload"**
   - Alternative quick path: visit https://vercel.com/new — there's a drag-zone there
4. Drag this entire `vercel-deploy` folder into the upload zone
5. Vercel detects it as a static site automatically
6. Project name suggestion: `watan-welcome`
7. Click **Deploy** — takes about 30 seconds
8. You'll get a URL like `https://watan-welcome.vercel.app` — test it works

## Deploy method 2: Vercel CLI (better for repeat deploys)

```bash
# One-time setup
npm install -g vercel

# From inside this folder
cd vercel-deploy
vercel

# Follow prompts. For subsequent updates:
vercel --prod
```

## Connect the custom subdomain

After the deploy works on the default `.vercel.app` URL:

1. In Vercel: **Project → Settings → Domains**
2. Add domain: `welcome.watandesigns.sa`
3. Vercel will show DNS records you need to add
4. Log in to your DNS provider (Bluehost, Cloudflare, or wherever `watandesigns.sa` is managed)
5. Add the record Vercel asks for. Usually one of:
   - **CNAME** record: `welcome` → `cname.vercel-dns.com`
   - (If Vercel asks for an A record instead, use that — they handle it dynamically)
6. Wait 5–60 minutes for DNS propagation
7. Vercel automatically provisions a free SSL certificate
8. Visit `https://welcome.watandesigns.sa` — should load the page

## Updating the page later

**With CLI:** edit `index.html`, then run `vercel --prod` from this folder

**With drag-and-drop:** go to your Vercel project → Deployments tab → drag the updated folder again. Or use the Vercel dashboard's web editor for tiny edits

## Important: regenerate the QR after subdomain is live

The QR currently encodes `https://watandesigns.sa/welcome/`. After deploying to `welcome.watandesigns.sa`, ask Claude to regenerate the QR with the new URL — old QR scans will break.

## Troubleshooting

**Page deployed but DNS not working:** subdomain takes time to propagate. Try `dig welcome.watandesigns.sa` in terminal or use https://dnschecker.org to confirm propagation across regions.

**Got the "Vercel" branding on the deploy:** that only happens on free plan deploys when you don't have a custom domain. After you add `welcome.watandesigns.sa` it goes away.

**Want to change the URL later:** add a new domain in Vercel settings, delete the old one. DNS only — no rebuild needed.
