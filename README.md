# Raj Art Service — Website

Single-file static website (HTML/CSS/JS all in `index.html`, no build step needed).

## Deploy on GitHub Pages

1. Create a new repository on GitHub (e.g. `raj-art-service`).
2. Upload `index.html` to the **root** of that repository.
   - On github.com: click "Add file" → "Upload files" → drag in `index.html` → Commit.
3. Go to the repo's **Settings** → **Pages** (left sidebar).
4. Under "Build and deployment" → "Source", choose **Deploy from a branch**.
5. Under "Branch", select **main** and folder **/ (root)** → Save.
6. Wait 1-2 minutes. GitHub will give you a live link like:
   `https://<your-username>.github.io/<repo-name>/`

That's it — no npm install, no build tools, since it's a plain static HTML file.

## Optional: custom domain
If you own a domain, add a `CNAME` file (containing just your domain, e.g. `rajartservice.com`) to the same folder, then point your domain's DNS to GitHub Pages per GitHub's docs.
