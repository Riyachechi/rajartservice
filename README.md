# Raj Art Service — Website

Single-file static website. Everything (HTML/CSS/JS, even the logo) lives in `index.html` — no build step needed.

## 1. Deploy on GitHub Pages

1. Create a new repository on GitHub (e.g. `raj-art-service`).
2. Upload `index.html` to the **root** of that repository (Add file → Upload files → Commit).
3. Repo → **Settings** → **Pages**.
4. Under "Build and deployment" → Source: **Deploy from a branch**. Branch: **main**, folder **/ (root)** → Save.
5. Wait 1–2 minutes. Your live link: `https://<your-username>.github.io/<repo-name>/`

## 2. Enquiry form → email (Formspree, free)

Right now the form is wired to Formspree but needs your form ID:

1. Go to https://formspree.io → sign up free → **New Form**.
2. Set the notification email to `rajartservice.business@gmail.com`, verify it.
3. Copy your form endpoint, e.g. `https://formspree.io/f/abcd1234`.
4. In `index.html`, find:
   ```html
   <form id="inquiryForm" action="https://formspree.io/f/YOUR_FORM_ID" method="POST">
   ```
   Replace `YOUR_FORM_ID` with your real ID.
5. Re-upload `index.html` to GitHub. Every enquiry submitted on the site now lands in that inbox.

Free Formspree tier covers up to 50 submissions/month, which is plenty to start.

## 3. Real-time admin content sync (Firebase, free)

The site has a built-in editor (🔒 button, bottom-right → login `rajartservice` / `raj123`, **change this password** in `index.html` under `ADMIN_PASS`). Edits are now saved to a shared **Firebase Firestore** database, so every visitor — and every already-open browser tab — sees the update within a second or two, no reload needed.

To activate it (~15 minutes, all free):

1. Go to https://console.firebase.google.com → **Add project** → name it anything (e.g. `raj-art-service`) → follow the prompts (Google Analytics optional, can skip).
2. Once created, click the **`</>`** (web) icon to register a web app → give it a nickname → **Register app**. Firebase will show you a `firebaseConfig` object like:
   ```js
   const firebaseConfig = {
     apiKey: "AIza...",
     authDomain: "raj-art-service.firebaseapp.com",
     projectId: "raj-art-service",
     storageBucket: "raj-art-service.appspot.com",
     messagingSenderId: "...",
     appId: "..."
   };
   ```
3. In the left sidebar: **Build → Firestore Database → Create database**. Choose a region close to India (e.g. `asia-south1`). Start in **test mode** for now.
4. Go to the **Rules** tab of Firestore and paste this, then **Publish**:
   ```
   rules_version = '2';
   service cloud.firestore {
     match /databases/{database}/documents {
       match /site/content {
         allow read: if true;
         allow write: if true;
       }
     }
   }
   ```
   ⚠️ **Note on security:** this allows anyone who inspects the page and finds your Firebase keys to write to the content document via the browser console — but that's the same practical risk level as today, since the admin password is already visible in the page's source code either way. It's fine for a simple business site. If you ever want it locked down properly, that requires adding Firebase Authentication tied to your admin account — a separate, bigger step I'm happy to help with later.
5. Back in `index.html`, find this block near the bottom and replace the placeholder values with your real `firebaseConfig`:
   ```js
   var firebaseConfig = {
     apiKey: "YOUR_API_KEY",
     authDomain: "YOUR_PROJECT.firebaseapp.com",
     projectId: "YOUR_PROJECT_ID",
     storageBucket: "YOUR_PROJECT.appspot.com",
     messagingSenderId: "YOUR_SENDER_ID",
     appId: "YOUR_APP_ID"
   };
   ```
6. Re-upload `index.html` to GitHub (overwrite the old one, or commit the change). Done — admin edits now go live for everyone instantly.

**Until you complete this step**, the CMS will silently fall back to saving in that browser only (same as before) — it won't error out or break the site.

## Contact details on this site
- WhatsApp / Call: **+91 80768 55627**
- Enquiry form delivers to: **rajartservice.business@gmail.com**

## Optional: custom domain
Add a `CNAME` file (containing just your domain, e.g. `rajartservice.com`) to the repo root, then point your domain's DNS to GitHub Pages per GitHub's docs.
