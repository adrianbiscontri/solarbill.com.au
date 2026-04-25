# ☀️ SolarIQ — Solar & Battery Calculator

A web app that reads your electricity bill using AI and calculates your optimal solar panel system and battery storage.

---

## Quick Start (Run Locally)

### Prerequisites
- [Node.js](https://nodejs.org/) version 18 or higher
- An Anthropic API key → [console.anthropic.com](https://console.anthropic.com/)

### Steps

```bash
# 1. Install dependencies
npm install

# 2. Create your environment file
cp .env.example .env

# 3. Open .env and paste your Anthropic API key
#    ANTHROPIC_API_KEY=sk-ant-...

# 4. Start the server
npm start

# 5. Open your browser to:
#    http://localhost:3000
```

---

## Deploy to the Web (Free Options)

### Option 1 — Railway (Recommended, easiest)

Railway gives you a free hosted URL in about 2 minutes.

1. Create a free account at **railway.app**
2. Click **"New Project"** → **"Deploy from GitHub repo"**
   - Or use **"Deploy from template"** → select Node.js
3. Upload your project files (or connect GitHub)
4. Go to **Variables** tab and add:
   ```
   ANTHROPIC_API_KEY = your_key_here
   ```
5. Railway auto-detects Node.js and runs `npm start`
6. Click the generated URL — your app is live! ✅

---

### Option 2 — Render (Free tier)

1. Create account at **render.com**
2. Click **"New"** → **"Web Service"**
3. Connect your GitHub repo (or upload files)
4. Set:
   - **Build Command:** `npm install`
   - **Start Command:** `node server.js`
5. Under **Environment Variables**, add:
   ```
   ANTHROPIC_API_KEY = your_key_here
   ```
6. Click **"Create Web Service"** — live in ~2 min ✅

---

### Option 3 — Fly.io (Free tier)

```bash
# Install Fly CLI
curl -L https://fly.io/install.sh | sh

# Login
fly auth login

# From inside your project folder:
fly launch           # follow prompts, choose free tier
fly secrets set ANTHROPIC_API_KEY=your_key_here
fly deploy
```

Your app will be at `https://your-app-name.fly.dev` ✅

---

### Option 4 — Heroku

```bash
# Install Heroku CLI, then:
heroku login
heroku create your-app-name
heroku config:set ANTHROPIC_API_KEY=your_key_here
git push heroku main
heroku open
```

---

### Option 5 — VPS / Linux Server (DigitalOcean, Linode, etc.)

```bash
# On your server:
git clone your-repo OR upload files via SFTP
cd solariq-app
npm install

# Set environment variable
export ANTHROPIC_API_KEY=your_key_here

# Run with PM2 (keeps app alive)
npm install -g pm2
pm2 start server.js --name solariq
pm2 startup   # auto-start on reboot
pm2 save

# Optional: set up Nginx as reverse proxy on port 80/443
```

---

## Without AI Bill Reading (Static Hosting — No Server Needed)

If you only want the calculator without the PDF/image upload feature, you can host the static HTML file anywhere for free:

- **Netlify Drop:** Go to [netlify.com/drop](https://app.netlify.com/drop), drag `public/index.html` — done
- **GitHub Pages:** Push to a repo, enable Pages in Settings
- **Cloudflare Pages:** Connect repo, deploy instantly

> The calculator itself works fully without a server. Only the "Upload Bill" AI feature requires the Node.js backend.

---

## Project Structure

```
solariq-app/
├── server.js          ← Node.js backend (API proxy)
├── package.json       ← Dependencies
├── .env.example       ← Copy to .env and add your API key
├── .gitignore         ← Keeps .env out of git
└── public/
    └── index.html     ← The full app (frontend)
```

---

## How the Bill Upload Works

1. User uploads a PDF or photo of their electricity bill
2. The browser sends it (base64 encoded) to `/api/read-bill` on your server
3. Your server forwards it to the Anthropic API with your secret API key
4. Claude reads the bill and extracts: kWh usage, tariff rates, billing period, state, retailer, feed-in tariff
5. The data auto-populates the calculator fields
6. The user clicks "Calculate" to get their solar recommendation

The API key never touches the browser — it stays safely on your server. ✅

---

## Environment Variables

| Variable | Required | Description |
|---|---|---|
| `ANTHROPIC_API_KEY` | Yes (for bill upload) | Your Anthropic API key |
| `PORT` | No | Port to run on (default: 3000) |

---

## Supported Electricity Retailers

The app recognises bills from all major Australian and New Zealand retailers including:

**Australia:** AGL, Origin Energy, EnergyAustralia, Sumo, Red Energy, Powershop, Simply Energy, Alinta Energy, Amber Electric, GloBird Energy, Tango Energy, ReAmped Energy, Nectr, Diamond Energy, Momentum Energy, Energy Locals, Aurora Energy, ActewAGL, Synergy, Horizon Power, Ergon Energy, Lumo Energy, and many more.

**New Zealand:** Contact Energy, Genesis, Mercury, Meridian, Nova Energy, Flick Electric, Electric Kiwi, Powershop NZ, and more.

---

## Getting an Anthropic API Key

1. Go to [console.anthropic.com](https://console.anthropic.com/)
2. Sign up / log in
3. Click **"API Keys"** in the left sidebar
4. Click **"Create Key"**
5. Copy and paste into your `.env` file

Bill reading costs approximately **$0.01–0.03 per bill scan** using Claude Sonnet.

---

## License

MIT — free to use, modify and deploy.
