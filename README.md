# Arun-Portfolio
Portfolio
# Arunpratap Singh — Portfolio Website

## What's in this folder

```
arunpratap-portfolio/
├── index.html                 ← the website (design, content, animations)
├── Arunpratap_Singh_CV.pdf    ← served by the "Download CV" button
├── api/
│   └── contact.js             ← backend: contact form → your Gmail inbox
├── package.json               ← tells Vercel to use modern Node
├── vercel.json                ← clean URLs + security headers
└── .gitignore
```

No build step and no npm install — Vercel serves `index.html` directly and turns
`api/contact.js` into a free serverless endpoint at `/api/contact`.

---

## Step 1 — Get a free email API key (Resend)

The contact form sends messages through Resend (free: 3,000 emails/month).

1. Go to https://resend.com and **sign up using arunpratap.rv007@gmail.com**.
   Important: on the free plan without your own domain, Resend can only deliver
   to the email address you signed up with, so use the same inbox you want
   messages in.
2. In the Resend dashboard open **API Keys → Create API Key**.
   Name it `portfolio`, permission **Sending access**, then copy the key
   (starts with `re_`). You only see it once, so paste it somewhere safe.

## Step 2 — Put the code on GitHub

1. Create a free account at https://github.com if you don't have one.
2. Click **+ → New repository**. Name it `portfolio`, keep it Public or Private,
   and click **Create repository**.
3. On the new repo page click **uploading an existing file**.
4. Drag in **everything inside** the `arunpratap-portfolio` folder
   (index.html, the PDF, package.json, vercel.json, and the `api` folder).
   Make sure `api/contact.js` stays inside an `api` folder.
5. Click **Commit changes**.

## Step 3 — Deploy on Vercel (free)

1. Go to https://vercel.com and click **Sign Up → Continue with GitHub**
   (choose the free **Hobby** plan).
2. Click **Add New… → Project**, find your `portfolio` repo, click **Import**.
3. Leave Framework Preset as **Other**. Leave Build and Output settings empty.
4. Open **Environment Variables** and add:

   | Name              | Value                              |
   |-------------------|------------------------------------|
   | `RESEND_API_KEY`  | your `re_...` key from Step 1      |
   | `CONTACT_TO_EMAIL`| arunpratap.rv007@gmail.com         |

5. Click **Deploy**. After ~30 seconds you get a live link like
   `https://portfolio-xxxx.vercel.app`.

## Step 4 — Test it

1. Open your live link, scroll to **Contact**, send yourself a test message.
2. Check Gmail (and the Spam folder the first time — mark it "Not spam").
3. If it fails: Vercel → your project → **Logs** shows the exact error.
   Most common cause: the env variable was added *after* deploying. Fix by
   going to **Deployments → ⋯ → Redeploy**.

## Step 5 — Nicer free URL (optional)

Vercel → project → **Settings → Domains** → edit the `.vercel.app` name, e.g.
`arunpratapsingh.vercel.app`.

If you later buy a domain (e.g. arunpratapsingh.com, ~₹800/year), add it in the
same Domains screen and follow Vercel's DNS instructions. You can then verify
the domain in Resend and set `CONTACT_FROM` to `Arunpratap <hello@yourdomain.com>`.

---

## Your CV on the site

The CV is already attached: the file `Arunpratap_Singh_CV.pdf` sits next to
`index.html`, and three places use it:

- **Hero "View CV" button** opens it in a viewer on top of the page, with a
  Download PDF button. On phones it opens in a new tab instead, since mobile
  browsers can't show PDFs inside a page well.
- **Contact section "CV" card** does the same.
- Anyone can also go directly to `https://your-site.vercel.app/Arunpratap_Singh_CV.pdf`.

**To update your CV:** on GitHub, open the repo, click the PDF → ⋯ → Delete,
then **Add file → Upload files** and upload the new PDF with exactly the same
name `Arunpratap_Singh_CV.pdf`. Vercel redeploys on its own.

---

## Adding your LinkedIn recommendations

LinkedIn doesn't allow other sites to pull recommendations automatically, so
you copy them in once.

1. Log in to LinkedIn, open your profile, scroll to **Recommendations**,
   choose the **Received** tab, and click **Show all**.
2. Open `index.html` (on GitHub: click the file → pencil icon).
3. Press Ctrl+F and search for `RECOMMENDATIONS = [`.
4. For each recommendation, fill in one block:

```js
{
  name: "Priya Shah",
  title: "Head of Talent, Example Bank",
  relation: "Was a client of Arunpratap",
  date: "March 2025",
  photo: "",
  text: "Paste their full recommendation here."
},
```

   - `relation` is the grey line LinkedIn shows, e.g. "managed Arun directly".
   - If the text contains a double quote `"`, write it as `\"`.
   - For a photo, upload an image (e.g. `priya.jpg`) next to `index.html` and
     write `photo: "priya.jpg"`. Leave it `""` to show initials.
5. Delete the three example entries, then **Commit changes**.

Add as many as you like; the dots and counter update automatically. If you
delete them all, the section and its nav link hide themselves.

Before adding someone's recommendation to a public site, it's courteous to let
them know, since their name and job title will appear on it.

---

## Updating the site later

Edit `index.html` on GitHub (pencil icon → Commit). Vercel redeploys
automatically within a minute. To replace your CV, upload a new PDF with the
exact same filename `Arunpratap_Singh_CV.pdf`.

## Alternative: deploy from your computer (Vercel CLI)

```bash
npm i -g vercel
cd arunpratap-portfolio
vercel            # answer the prompts, accept defaults
vercel env add RESEND_API_KEY
vercel --prod
```

## Preview locally

Just double-click `index.html`. Everything works except the contact form
(which needs Vercel). Run `vercel dev` to test the form locally too.
