# Stocktake — Cyprus Vitamin Shop

A web app for stocktaking your Shopify store, deployable to Vercel.

## Project structure

```
stocktake/
├── api/
│   └── proxy.js        ← Serverless function (proxies Anthropic API)
├── public/
│   └── index.html      ← The stocktake app
├── vercel.json         ← Routing config
└── README.md
```

## Deploy to Vercel (3 steps)

### Option A — Vercel CLI (fastest)

1. Install the CLI:
   ```
   npm install -g vercel
   ```

2. From inside this folder, run:
   ```
   vercel
   ```
   Follow the prompts — accept all defaults.

3. Add your API key as an environment variable:
   ```
   vercel env add ANTHROPIC_API_KEY
   ```
   Paste your key (sk-ant-...) when prompted. Choose "Production".

4. Redeploy to pick up the env var:
   ```
   vercel --prod
   ```

Done — Vercel gives you a URL like `https://stocktake-xyz.vercel.app`.

---

### Option B — GitHub + Vercel Dashboard (no CLI needed)

1. Create a GitHub repo and push this folder to it.

2. In Vercel dashboard → "Add New Project" → import your GitHub repo.

3. Click "Deploy" (no build settings needed).

4. Go to Project → Settings → Environment Variables.
   Add:  Name = `ANTHROPIC_API_KEY`  /  Value = your key

5. Go to Deployments → click the three dots on latest → "Redeploy".

---

## Environment variables

| Name                | Value              | Required |
|---------------------|--------------------|----------|
| ANTHROPIC_API_KEY   | sk-ant-...         | Yes      |

## Notes

- The app loads fresh from Shopify every time it opens — always up to date.
- Use the "↺ Refresh" button to reload products mid-session.
- Stock updates write directly to Shopify via inventoryAdjustQuantities.
- The proxy (/api/proxy.js) keeps your API key server-side — it never reaches the browser.
