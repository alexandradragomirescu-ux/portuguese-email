# Portuguese Personalities Email App — Vercel Deployment

A web app where students can write emails to Portuguese personalities and receive AI-generated PR replies, language assessment, and a motivational quote. Available in English, Romanian, and Portuguese.

## What's in this folder

```
vercel-app/
├── api/
│   └── chat.js          ← Serverless function that hides your API key
├── public/
│   └── index.html       ← The app frontend
├── vercel.json          ← Vercel config
└── README.md            ← This file
```

## How to deploy (10 minutes, no coding required)

### Step 1: Create accounts (one-time)

1. Go to https://www.anthropic.com/ and create an account
2. Go to https://console.anthropic.com/settings/keys → click "Create Key" → copy the key (starts with `sk-ant-...`)
3. Add some credit to your Anthropic account (Settings → Billing → $5 is enough for hundreds of student emails)
4. Go to https://vercel.com/ and sign up (use "Continue with GitHub" or email — it's free)

### Step 2: Upload the app to Vercel

**Easiest method — drag and drop:**

1. Open https://vercel.com/new
2. Click "Browse" (under "Deploy without Git" if you see that option) or use the dropdown
3. If you only see Git options, choose "Import Third-Party Git Repository" then scroll for "Deploy from local"

**If the drag-and-drop option isn't visible, use this method instead:**

1. Install Vercel CLI: open Terminal and run `npm install -g vercel`
   (You need Node.js — download from https://nodejs.org if you don't have it)
2. In Terminal, navigate to the folder where you unzipped these files:
   `cd path/to/vercel-app`
3. Run: `vercel`
4. Follow the prompts:
   - Set up and deploy? → **Y**
   - Which scope? → choose your account
   - Link to existing project? → **N**
   - Project name? → press Enter (use default) or pick a name like `portuguese-email`
   - Directory? → press Enter (use current)
   - Override settings? → **N**

### Step 3: Add your API key as an environment variable

1. After deployment, go to https://vercel.com/dashboard
2. Click on your new project
3. Go to **Settings** → **Environment Variables**
4. Add a new variable:
   - **Name:** `ANTHROPIC_API_KEY`
   - **Value:** paste your `sk-ant-...` key
   - Apply to: Production, Preview, Development (check all)
5. Click **Save**

### Step 4: Redeploy so the key takes effect

1. Go to **Deployments** tab
2. Click the three dots on the latest deployment → **Redeploy**
3. Wait ~30 seconds

### Step 5: Share the link

Your app is now live at something like:
`https://portuguese-email.vercel.app`

Send this link to your students. They just open it and start writing!

## Costs

- Vercel hosting: **free** (you're well within their free tier)
- Anthropic API: roughly **$0.01–0.02 per student email** (each email triggers 3 API calls)
- A class of 30 students sending 1 email each ≈ **$0.30–0.60**

You can set spending limits in https://console.anthropic.com/settings/limits to prevent surprises.

## Optional: custom domain

In Vercel project settings → Domains, you can connect a custom domain like `portuguese.yourschool.com` if you own one.

## Updating the app later

If you want to change something (add a personality, edit a bio, etc.):

- **Used CLI?** Edit the files, then run `vercel --prod` again.
- **Used drag and drop?** Upload the changed files via Vercel dashboard.

## Troubleshooting

**"Could not reach the server"** in the app
→ Check that `ANTHROPIC_API_KEY` is set in Vercel environment variables and that you redeployed after adding it.

**Vercel deployment fails**
→ Make sure your folder structure has `api/chat.js` (not `api/chat/index.js` or other variants).

**"401 unauthorized" or "invalid x-api-key"**
→ Your API key may be wrong or revoked. Generate a new one at console.anthropic.com and update the environment variable.
