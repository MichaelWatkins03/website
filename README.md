# Michael Watkins — Personal Site

Static portfolio site for Michael Watkins, Mechanical Engineer & Designer (Christchurch, NZ).

## Local development

Just open `index.html` in a browser. No build step.

```bash
# Simple local server (optional)
python -m http.server 8000
# or: npx serve .
```

## Hosting on GitHub Pages (recommended setup)

This site is designed to be hosted directly on **GitHub Pages**.

### One-time setup (in the GitHub repo UI)

1. Go to your repo → **Settings** → **Pages**.
2. Under "Build and deployment":
   - **Source**: Select **GitHub Actions** (not "Deploy from a branch").
3. (Optional but for your custom domain) In the same Pages settings, add your custom domain under "Custom domain" and save. GitHub will create the necessary DNS records info / CNAME verification.

### DNS for the custom domain (www.michaelwatkins.nz)

The repo contains a `CNAME` file with `www.michaelwatkins.nz`.

You must create the corresponding DNS record at your registrar / DNS host:

- For `www` subdomain: Create a **CNAME** record pointing `www` to `<your-username>.github.io.` (or the repo project name if applicable).
- For an apex domain (michaelwatkins.nz without www): You need **A** records pointing to GitHub's Pages IPs (see GitHub docs for the current list) + the `CNAME` file can stay or you can use ALIAS/ANAME if your provider supports it.

After DNS propagates, GitHub will automatically obtain and renew a TLS cert for your custom domain.

### How deployment works

- Pushing to `main` triggers [`.github/workflows/pages-deploy.yml`](./.github/workflows/pages-deploy.yml).
- The workflow checks out with Git LFS (`lfs: true`), builds a Pages artifact from the repo root, and deploys it.
- The `CNAME` file + `.nojekyll` are included automatically.

### Notes

- All asset paths are relative (`Media/...`) so the site works whether served at the root of a custom domain or under a project subpath (`/repo-name/`).
- Video and image assets are committed directly (no LFS for the files actually used by the page). Large unused media remain in history via prior LFS for clone size reasons.
- GitHub Pages has bandwidth and build minutes quotas on the free tier. High-resolution videos and many large photos can consume bandwidth quickly.

## Tech

- Single-file `index.html` (inline CSS + vanilla JS)
- No frameworks, no build tools
- Custom contact overlay animation + canvas graph synced to hero video

## Updating the site

Edit `index.html` (and add/replace files in `Media/`), commit, and push. The GitHub Action will publish the update within a minute or two.
