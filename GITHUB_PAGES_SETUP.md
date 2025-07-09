# How to Deploy This Cheat Sheet to GitHub Pages

## Quick Steps:

1. **Create a GitHub repository**
   - Go to https://github.com/new
   - Name it something like `claude-code-cheatsheet`
   - Make it public
   - Don't initialize with README (we already have one)

2. **Push your code**
   ```bash
   git remote add origin https://github.com/YOUR-USERNAME/claude-code-cheatsheet.git
   git branch -M main
   git push -u origin main
   ```

3. **Enable GitHub Pages**
   - Go to your repository on GitHub
   - Click Settings (⚙️) tab
   - Scroll down to "Pages" in the left sidebar
   - Under "Source", select "Deploy from a branch"
   - Choose "main" branch and "/ (root)" folder
   - Click Save

4. **Access your site**
   - Wait 2-5 minutes for deployment
   - Your site will be available at:
     `https://YOUR-USERNAME.github.io/claude-code-cheatsheet/`

## Alternative: Use as username.github.io

If you want it at just `https://YOUR-USERNAME.github.io/`:
1. Name your repository `YOUR-USERNAME.github.io`
2. Follow the same steps above
3. Your site will be at the root domain

## Updating the Site

Any time you push changes to the main branch, GitHub Pages will automatically update your site within a few minutes.

```bash
git add -A
git commit -m "Update cheat sheet"
git push
```