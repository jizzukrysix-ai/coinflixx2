# 🐉 DefiDragon — Telegram Mini App



A **free, open-source** Telegram Mini App where users watch ads and earn coins.  
Built with pure HTML, Tailwind CSS, and vanilla JavaScript — no build tools required.

> **Demo pages**: Tasks, Refer, and Wallet show a "Get Full Version" prompt.  
> **Home page**: Fully functional — integrates AdsGram or Monetag out of the box.

---

## 📸 Features

| Feature | Status |
|---|---|
| Watch ads → earn coins | ✅ Included (full) |
| Daily ad limit & progress bar | ✅ Included (full) |
| Day streak tracking | ✅ Included (full) |
| Recent earnings history | ✅ Included (full) |
| Telegram user avatar & name | ✅ Included (full) |
| AdsGram rewarded ad integration | ✅ Included (configure block ID) |
| Monetag rewarded ad integration | ✅ Included (configure zone ID) |
| Tasks system | 🔒 Full version |
| Referral system | 🔒 Full version |
| Wallet / withdrawal | 🔒 Full version |

---

## 🚀 Quick Start (5 minutes)

### 1. Clone the repository

```bash
git clone https://github.com/defidragon2022/CoinZilla-App-Clone
cd CoinZilla-App-Clone
```

### 2. Open `index.html` in your browser

No build step needed. You can open it directly:

```bash
# On Windows
start index.html

# On macOS
open index.html

# On Linux
xdg-open index.html
```

> **Note:** Some Telegram features (user name, haptics) only work inside Telegram.  
> In a browser the app falls back gracefully.

---

## ⚙️ Configuration

Open `index.html` and find the `CONFIG` block near the top (~line 25):

```javascript
const CONFIG = {
  adNetwork:      'both',              // 'adsgram' | 'monetag' | 'both'
  adsgramBlockId: 'YOUR_ADSGRAM_BLOCK_ID',
  monetagZoneId:  'YOUR_MONETAG_ZONE_ID',
  monetagShowFn:  'show_YOUR_SHOW_FN',
  rewardPerAd:    10,                  // coins per completed ad
  maxAdsPerDay:   20,                  // 0 = unlimited
  appName:        'CoinZilla',
};
```

Change only the values you need — everything else is already wired up.

---

## 📺 Setting Up AdsGram

AdsGram is the most popular rewarded ad network for Telegram Mini Apps.

### Step 1 — Create an account

1. Go to **[https://adsgram.ai](https://adsgram.ai)**
2. Click **Sign Up** and log in with your Telegram account

### Step 2 — Add your Mini App

1. In the dashboard click **"Add App"**
2. Enter your Mini App's URL (e.g. `https://your-username.github.io/coinzilla/`)
3. Wait for approval (usually within 24 hours)

### Step 3 — Create a Block

1. Go to **Blocks → Create Block**
2. Choose format: **Rewarded Video** *(recommended for earn apps)*
3. Copy your **Block ID** (looks like `1234` or `"app-reward-1234"`)

### Step 4 — Configure the app

In `index.html` update CONFIG:

```javascript
adNetwork:      'adsgram',
adsgramBlockId: '1234',   // ← paste your Block ID here
```

The AdsGram SDK is already included via:
```html
<script src="https://sad.adsgram.ai/js/sad.min.js" async></script>
```

No further code changes needed. ✅

---

## 💵 Setting Up Monetag

Monetag is an alternative ad network that also supports Telegram Mini Apps.

### Step 1 — Create an account

1. Go to **[https://monetag.com](https://monetag.com)**
2. Click **Sign Up → Publisher**
3. Fill in your details and verify your email

### Step 2 — Add your website/app

1. Dashboard → **My Sites → Add Site**
2. Enter your Mini App's URL
3. Choose category (e.g. *Games / Entertainment*)

### Step 3 — Create a Zone (Rewarded Interstitial)

1. Go to **Zones → Create Zone**
2. Select ad format: **Rewarded Interstitial** or **In-Page Push**
3. After creation, click the zone to see its integration code

### Step 4 — Get your script tag & show function

Monetag gives you a snippet like:

```html
<script async src="//ophoacit.com/1?z=12345678"
        data-zone="12345678"
        data-sdk="show_12345678"></script>
```

- Your **Zone ID** is `12345678`
- Your **show function** is `show_12345678`

### Step 5 — Add the script to `index.html`

Find the commented Monetag block in `<head>` and uncomment + fill in your values:

```html
<!-- BEFORE (commented out) -->
<!-- <script async src="//ophoacit.com/1?z=YOUR_ZONE_ID" data-zone="YOUR_ZONE_ID" data-sdk="show_YOUR_SHOW_FN"></script> -->

<!-- AFTER (uncommented with your values) -->
<script async src="//ophoacit.com/1?z=12345678"
        data-zone="12345678"
        data-sdk="show_12345678"></script>
```

### Step 6 — Update CONFIG

```javascript
adNetwork:      'monetag',
monetagZoneId:  '12345678',
monetagShowFn:  'show_12345678',   // must match data-sdk value above
```

---

## 🌐 Hosting on GitHub Pages (free)

GitHub Pages lets you host the app for free with a public URL.

### Step 1 — Push to GitHub

```bash
git init
git add .
git commit -m "Initial commit — DefiDragon"
git branch -M main
git remote add origin https://github.com/YOUR_USERNAME/coinzilla
git push -u origin main
```

### Step 2 — Enable GitHub Pages

1. Go to your repo on GitHub
2. **Settings → Pages**
3. Under **Source**, select `main` branch, `/ (root)` folder
4. Click **Save**

After ~60 seconds your app will be live at:
```
https://YOUR_USERNAME.github.io/coinzilla/
```

---

## 🤖 Setting Up Your Telegram Bot & Mini App

### Step 1 — Create a Bot

1. Open Telegram and search for **@BotFather**
2. Send `/newbot` and follow the prompts
3. Copy your **Bot Token** (keep it secret!)

### Step 2 — Create the Mini App

Send the following to @BotFather:

```
/newapp
```

1. Choose your bot
2. Set the **Web App URL** to your GitHub Pages URL:  
   `https://YOUR_USERNAME.github.io/coinzilla/`
3. Upload a 640×360 photo for the app thumbnail
4. Give it a name (e.g. **CoinZilla**)

### Step 3 — Create a Menu Button (optional)

To add a persistent "Open App" button in the chat:

```
/mybots → [your bot] → Bot Settings → Menu Button → Configure menu button
```

Enter your Web App URL and set button text to **"🐉 Open App"**.

### Step 4 — Test your app

1. Open your bot in Telegram
2. Tap the **Menu** button or send `/start`
3. The Mini App should open and load your `index.html`

---

## 📁 Project Structure

```
defidragon/
├── index.html   ← entire app (single file, no dependencies)
└── README.md    ← this file
```

---

## 🎨 Customisation

| What | Where in index.html |
|---|---|
| App name | `CONFIG.appName` and `<title>` tag |
| Coins per ad | `CONFIG.rewardPerAd` |
| Daily ad cap | `CONFIG.maxAdsPerDay` |
| Telegram contact link | `CONFIG.telegramContact` |
| Primary colour | CSS `--primary` variable |
| Background colour | CSS `--bg` variable |

---

## 🔒 Locked Pages — Get Full Version

The **Tasks**, **Refer**, and **Wallet** pages display a promotional screen  
directing users to your Telegram contact to purchase the full version.

---

## 🛡️ Security Notes

- User data is stored only in `localStorage` (client-side, no server needed)
- No API keys or secrets are stored in the frontend
- Your ad network Block ID / Zone ID is public-facing by design (safe to commit)
- Your **Bot Token** is never used or stored in this app

---

## 📄 License

MIT License — free to use, modify, and distribute.  
Attribution appreciated but not required.

---

## 💬 Support

Questions or want the full version?  
👉 Contact **[@DefiDragon](https://t.me/DefiDragon)** on Telegram
