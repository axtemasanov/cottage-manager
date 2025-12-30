# GitHub Setup Instructions for ЖК Construction Chat

Follow these steps to connect your beautiful construction chat application to GitHub and deploy it.

## 1. Create a GitHub Repository

1. Go to [GitHub.com](https://github.com)
2. Click the "+" icon in the top right corner and select "New repository"
3. Give your repository a name (e.g., "zhk-construction-chat")
4. Choose "Public" or "Private" depending on your preference
5. **Do NOT** initialize with README, .gitignore, or license (you already have these)
6. Click "Create repository"

## 2. Link Your Local Repository to GitHub

In your project directory (c:\VS\чат), run these commands:

```bash
git remote add origin https://github.com/YOUR_USERNAME/zhk-construction-chat.git
git branch -M main
git push -u origin main
```

Replace `YOUR_USERNAME` with your actual GitHub username.

## 3. Deploy to GitHub Pages

### Option 1: Using GitHub Actions (Recommended)

1. Create a `.github/workflows/deploy.yml` file in your repository:

```yaml
name: Deploy to GitHub Pages

on:
  push:
    branches: [ main ]

jobs:
  build-and-deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - uses: actions/setup-node@v3
        with:
          node-version: 18
      - name: Install dependencies
        run: npm install
      - name: Build
        run: npm run build
      - name: Deploy to GitHub Pages
        uses: peaceiris/actions-gh-pages@v3
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_dir: ./dist
          publish_branch: gh-pages
```

2. Push this file to your repository:
```bash
mkdir -p .github/workflows
# Create the deploy.yml file with the content above
git add .
git commit -m "Add GitHub Actions workflow"
git push
```

### Option 2: Manual Deployment

1. Build your project:
```bash
npm run build
```

2. Create a new branch for deployment:
```bash
git checkout -b gh-pages
```

3. Add the build files:
```bash
git add dist/
git commit -m "Deploy to GitHub Pages"
```

4. Push to the gh-pages branch:
```bash
git push origin gh-pages
```

5. In your GitHub repository settings, go to "Pages" and select "gh-pages" branch as the source.

## 4. Configure GitHub Pages (if using Option 2)

1. Go to your GitHub repository
2. Click on "Settings" tab
3. Scroll down to the "Pages" section
4. Under "Source", select "Deploy from a branch"
5. Choose "gh-pages" branch and "/ (root)" folder
6. Click "Save"

Your site will be available at `https://YOUR_USERNAME.github.io/zhk-construction-chat/`

## 5. GitHub Repository Settings

For your construction company's chat application, consider these settings:

- **Repository Description**: "Professional chat application for ЖК Construction team communication"
- **Website**: Add your deployed URL once available
- **Topics/Tags**: `react`, `construction`, `chat`, `team-communication`, `vite`

## 6. Continuous Development

After setting up, you can continue developing:

1. Make changes to your code
2. Test locally with `npm run dev`
3. Build to test production version with `npm run build`
4. Commit and push changes:
```bash
git add .
git commit -m "Description of changes"
git push origin main
```

If using GitHub Actions, your site will automatically update after each push to main.

## Troubleshooting

**If your site doesn't load properly on GitHub Pages:**
- Check that `vite.config.js` has `base: './'` configuration
- Verify that all assets are loading correctly
- Make sure relative paths are used instead of absolute paths

**If you get 404 errors:**
- Ensure you're using `base: './'` in vite.config.js
- Check that GitHub Pages is configured to use the correct branch

Your beautiful construction-themed chat application is now ready to be shared with your team via GitHub!