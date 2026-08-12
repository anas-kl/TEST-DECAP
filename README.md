# Webnary — Test Site (GitHub Pages + Decap CMS + DecapBridge)

Minimal scaffold to test the whole chain we discussed: static site on GitHub
Pages, content editable through Decap CMS, authenticated through
DecapBridge, images uploaded straight into the repo.

## 1. Push this to GitHub

```bash
cd webnary-test-site
git init
git add .
git commit -m "Initial test site"
```

Create a **public** repo on GitHub (Free plan requires public for Pages),
then:

```bash
git branch -M main
git remote add origin https://github.com/YOUR_USERNAME/YOUR_REPO_NAME.git
git push -u origin main
```

## 2. Enable GitHub Pages

Repo → **Settings → Pages** → Source: `main` branch, `/ (root)` folder →
Save. Your test site will be live at
`https://YOUR_USERNAME.github.io/YOUR_REPO_NAME/` within a minute or two.

## 3. Register the site on DecapBridge

1. Sign up at <https://decapbridge.com/auth/signup>.
2. In the dashboard, **Add a site**:
   - Git provider: GitHub
   - Git repository: `YOUR_USERNAME/YOUR_REPO_NAME`
   - Git access token: create one at <https://github.com/settings/tokens>
     with **read/write access to Contents** on this repo (a fine-grained
     token scoped to just this repo is the safer option).
   - CMS login URL: `https://YOUR_USERNAME.github.io/YOUR_REPO_NAME/admin/index.html`
   - Auth type: **Classic** (email/password) to start — switch to **PKCE**
     later if you want "Login with Google/Microsoft."
3. DecapBridge generates a `config.yml` backend block for this exact site.
4. Copy that block and replace the placeholder `backend:` section in
   `admin/config.yml` in this repo.
5. Commit and push that change.

## 4. Invite yourself as a test user

In the DecapBridge dashboard, on the site's page, use **Manage
collaborators** to invite your own email. Follow the invite link to set a
password.

## 5. Test the full loop

- [ ] Visit `/admin` on the live GitHub Pages URL — you should see the
      DecapBridge login screen, not raw file contents.
- [ ] Log in with the account you invited.
- [ ] Open "Page d'accueil" → edit the title or body text → Publish.
- [ ] Reload the live site — the change should appear within a few seconds.
- [ ] Upload an image in the "Image principale" field → Publish.
- [ ] Confirm the image appears on the live page, and check the repo on
      GitHub — you should see a new commit with the file added under
      `images/uploads/`.

If all of those work, the architecture is proven end to end and it's safe
to replicate this scaffold for a real client site.

## Notes

- This scaffold intentionally has **no build step** — `index.html` fetches
  `content.json` directly in the browser. That's fine for testing and for a
  genuinely simple one-pager, but for a real client site you'll likely want
  a small static-site generator (or at least a build step that compresses
  uploaded images) rather than raw fetch-on-load.
- Design here is deliberately bare — this file is for proving the wiring
  works, not for client presentation.
