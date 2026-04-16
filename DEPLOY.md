# Deploying Southern Barn Builders to GitHub Pages

This guide walks you through publishing the site so it's live on the internet.
No coding experience required — just a web browser, your GitHub account, and a terminal (Git Bash, Command Prompt, or the terminal inside VS Code all work).

---

## Prerequisites

- You have a GitHub account
- The repository is on GitHub (e.g. `github.com/YOUR-USERNAME/Southern-Barn-Builders-LLC`)
- The repository is set to **Public** (GitHub Pages requires this on free accounts)

> **Not sure if it's public?** On your repo page, click **Settings** (gear icon tab at the top), scroll all the way down to the **Danger Zone**, and look for "Change repository visibility." If the button says "Make private," you're already public — you're good.

---

## Step 1 — Push Your Code to GitHub

If your code is only on your computer and not yet on GitHub, open a terminal in the project folder and run these commands one at a time. You can copy-paste each line:

```bash
git add .
git commit -m "Update site"
git remote add origin https://github.com/YOUR-USERNAME/Southern-Barn-Builders-LLC.git
git push -u origin master
```

**What each command does:**
- `git add .` — stages all your changed files
- `git commit -m "Update site"` — saves those changes with a short description
- `git remote add origin ...` — connects your local folder to the GitHub repo (only needed the first time)
- `git push -u origin master` — uploads everything to GitHub

> **Already connected to GitHub?** You only need the first three lines for future updates:
> ```bash
> git add .
> git commit -m "Update site"
> git push
> ```

GitHub may ask you to log in the first time you push. Follow the prompts — it will either open a browser window or ask for a personal access token.

---

## Step 2 — Enable GitHub Pages

These are the exact clicks inside GitHub's website:

1. Go to your repository page on GitHub.
2. Click the **Settings** tab (gear icon along the top).
3. In the left sidebar, scroll down and click **Pages** (it's under "Code and automation").
4. Under **Source**, click the dropdown and select **Deploy from a branch**.
5. Under **Branch**, click the dropdown that currently says "None" and select **master** (or **main** — pick whichever one your repo has).
6. The folder dropdown should already say **/ (root)**. Leave it there.
7. Click **Save**.

That's it. GitHub will start building your site automatically.

---

## Step 3 — Find Your Live URL

Stay on the **Settings > Pages** screen. After about 1-2 minutes, a green banner will appear at the top showing your live URL. It will look like this:

```
https://YOUR-USERNAME.github.io/Southern-Barn-Builders-LLC/
```

Replace `YOUR-USERNAME` with your actual GitHub username and `Southern-Barn-Builders-LLC` with whatever your repository is named. Click the link to confirm the site is working. Bookmark it.

> **Don't see the banner?** Refresh the page. It can take up to 2-3 minutes the first time.

---

## How Long Do Updates Take?

| What happened | How long until it's live |
|---|---|
| First-time deploy (just enabled Pages) | 1-3 minutes |
| Pushed an update to an existing page | 30 seconds to 2 minutes |
| Added a custom domain | DNS can take 15 minutes to 48 hours |

After pushing any change to the **master** branch, GitHub Pages rebuilds automatically. You don't need to click anything in Settings again — just push and wait.

---

## Step 4 (Optional) — Use a Custom Domain

If you own a domain like `southernbarnbuilders.com` and want visitors to see that instead of `github.io`:

1. Go to **Settings > Pages** in your repo.
2. Under **Custom domain**, type your domain (e.g. `www.southernbarnbuilders.com`) and click **Save**.
3. Log in to your domain registrar (GoDaddy, Namecheap, Squarespace Domains, etc.) and add these DNS records:

   **For `www.southernbarnbuilders.com`:** add a **CNAME** record pointing to:
   ```
   YOUR-USERNAME.github.io
   ```

   **For the bare domain `southernbarnbuilders.com`:** add four **A** records pointing to:
   ```
   185.199.108.153
   185.199.109.153
   185.199.110.153
   185.199.111.153
   ```

4. Back on GitHub, check the **Enforce HTTPS** box once the DNS check passes (this can take a few hours).

---

## Pushing Future Updates

Every time you edit the site and want those changes to go live, run these three commands in your terminal:

```bash
git add .
git commit -m "Describe what you changed"
git push
```

Replace `"Describe what you changed"` with a short note like `"Updated phone number"` or `"Added new gallery photos"`. The site will update automatically within a couple of minutes.

---

## Troubleshooting

### Site shows a 404 error
- Make sure `index.html` is in the **root** of the repository, not inside a subfolder. (It already is in this project — you're fine.)
- Double-check that you selected the correct branch (master or main) in **Settings > Pages**.
- Wait 2-3 minutes and refresh. The first deploy can be slow.

### CSS isn't loading (site looks like plain text with no styling)
- Check that the `css/` folder and `styles.css` file were pushed to GitHub. Go to your repo page on GitHub and verify you can see the `css` folder.
- Make sure the link in your HTML says `href="css/styles.css"` (not an absolute path like `C:\Users\...`).
- If using a custom domain, clear your browser cache (Ctrl+Shift+R on Windows) — stale cached files are the most common cause.

### Images aren't showing up
- This site uses external image URLs (Unsplash). If images don't load, your internet connection may be blocking them, or the URLs may have changed. Replace the `src="https://..."` in the HTML with your own images in a local `images/` folder.

### Custom domain not working
- DNS changes can take 15 minutes to 48 hours to propagate worldwide. Be patient.
- Double-check that the CNAME record points to exactly `YOUR-USERNAME.github.io` (not the full repo URL).
- Make sure you typed the domain correctly in **Settings > Pages > Custom domain**.

### Old version of the site still showing
- Hard-refresh your browser: **Ctrl+Shift+R** (Windows) or **Cmd+Shift+R** (Mac).
- Check the **Actions** tab on your GitHub repo — you can see if the latest deploy succeeded or failed.
- Wait 5 minutes. GitHub caches aggressively and it sometimes takes a moment.

### "Pages" option is grayed out in Settings
- Your repo is probably set to Private. Go to **Settings > Danger Zone > Change visibility** and switch it to Public.

### `git push` is rejected or asks for a password
- GitHub no longer accepts plain passwords. You need a **Personal Access Token**. Go to GitHub > click your profile picture > **Settings > Developer settings > Personal access tokens > Tokens (classic)** > Generate new token. Use that token as your password when prompted.
