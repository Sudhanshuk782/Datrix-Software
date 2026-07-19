# Deploy Datrix Software Website to GitHub Pages

## The site is a single self-contained file
`index.html` has the Datrix logo embedded as base64.
Works offline, zero build step, no npm required.

---

## Step 0 — Set up the contact form (REQUIRED — do this first)

The contact form uses **Formspree** — a free service that receives form submissions
and emails them to you. Without this step, the Send button will show an error.

### A. Create a free Formspree account
1. Go to **https://formspree.io** and click **Sign Up**
2. Use your email: **Sudhanshuk782@gmail.com**
3. Confirm your email address

### B. Create a new form
1. In your Formspree dashboard, click **+ New Form**
2. Give it a name: **Datrix Website Contact**
3. Click **Create Form**
4. You will see a form endpoint like:
   ```
   https://formspree.io/f/xpwzabcd
   ```
   Copy the **ID** at the end — in this example it is `xpwzabcd`

### C. Put your form ID into the website
1. Open `index.html` in VS Code (Ctrl+H to open Find & Replace)
2. Find:    `mykrwlzb`
3. Replace: `xpwzabcd`   (use your actual ID)
4. Save the file

That is it. The form will now email every submission directly to Sudhanshuk782@gmail.com.
**Free plan: 50 submissions/month. Upgrade to 1000/month if needed ($8/mo).**

---

## Step 1 — Create a GitHub repository

1. Go to **https://github.com/new**
2. Your repo: **`Datrix-Software`** (already created) → URL will be `https://Sudhanshuk782.github.io/datrix/`
   — OR name it **`Sudhanshuk782.github.io`** for the root URL (no /datrix suffix)
3. Set to **Public** (required for free GitHub Pages)
4. Leave all checkboxes unchecked → **Create repository**

---

## Step 2 — Push from your PC (PowerShell)

```powershell
cd C:\path\to\datrix-site

git config --global user.name  "Sudhanshu Kumar"
git config --global user.email "Sudhanshuk782@gmail.com"

git init
git add .
git commit -m "Launch Datrix Software website"
git branch -M main
git remote add origin https://github.com/Sudhanshuk782/Datrix-Software.git
git push -u origin main
```

---

## Step 3 — Enable GitHub Pages

1. In the repo → **Settings** → **Pages** (left sidebar)
2. Source: **Branch: main** / **Folder: / (root)**
3. Click **Save**
4. Wait ~2 minutes → live at `https://Sudhanshuk782.github.io/datrix/`

---

## Step 4 — Verify the contact form works

1. Open your live site
2. Fill in the contact form and click Send message
3. You should see the green "✓ Message sent!" confirmation
4. Check your Sudhanshuk782@gmail.com inbox — the email arrives within seconds
5. Also check your Formspree dashboard → Submissions tab

If the form shows an error:
- Make sure you replaced mykrwlzb with your actual Formspree ID
- Make sure your Formspree email is confirmed
- Check the browser console for error details

---

## Step 5 — Custom domain www.datrix.com (optional)

1. Settings → Pages → Custom domain → type `www.datrix.com` → Save
2. At your DNS registrar (GoDaddy, Namecheap etc.):
   - Add a **CNAME** record: Name = `www` / Value = `Sudhanshuk782.github.io`
3. Wait 10–30 minutes for DNS
4. Tick **Enforce HTTPS**

---

## Step 6 — Push updates

```powershell
git add .
git commit -m "Your update description"
git push
```
Site updates within 30 seconds.

---

## How the contact form works (technical)

```
User fills form → clicks Send
  ↓
Browser sends POST to https://formspree.io/f/mykrwlzb
  ↓
Formspree server receives it
  ↓
Formspree emails you at Sudhanshuk782@gmail.com
  ↓
User sees green ✓ "Message sent!" on the page
```

No server needed on your side. Formspree handles everything.
The user never has to open their email client.
