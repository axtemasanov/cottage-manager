# Troubleshooting Guide: White Screen on GitHub Pages

If you're experiencing a white screen when visiting your deployed construction chat application, here are the steps to resolve the issue:

## Common Causes and Solutions

### 1. JavaScript Errors
The most common cause of a white screen is JavaScript errors that prevent the React app from rendering.

**Solution:**
- Open browser developer tools (F12)
- Check the Console tab for any error messages
- Look for errors related to missing files or failed imports

### 2. Base Path Configuration
GitHub Pages serves content from a subdirectory (username.github.io/repo-name), which can cause path issues.

**Solution:**
- The `vite.config.js` file already has `base: './'` which should handle this
- This allows the app to work in subdirectories

### 3. Missing Dependencies in Build
Sometimes dependencies don't get properly bundled in the production build.

**Solution:**
- We've already ensured React Icons are properly included in the build
- The build output shows `icons-vendor.js` is being generated

### 4. GitHub Pages Configuration

**Verify your GitHub Pages settings:**
1. Go to your repository on GitHub
2. Click "Settings" tab
3. Scroll down to "Pages" section
4. Ensure the source is set to "gh-pages" branch (if using manual deployment) or the correct branch if using GitHub Actions
5. Ensure it's pointing to the correct folder (usually "/ (root)" or "docs/")

### 5. Deployment Process

**If using GitHub Actions (recommended):**
- Ensure the `.github/workflows/deploy.yml` file exists and is properly configured
- The workflow will automatically build and deploy your site when you push to main
- Check the "Actions" tab in your repository to see if the build/deploy workflow ran successfully

**If deploying manually:**
1. Run `npm run build` locally
2. Push the generated `dist` folder contents to the `gh-pages` branch

### 6. Verify Build Files
Make sure all necessary files were built:
- `dist/index.html` (should reference assets with relative paths)
- `dist/assets/` folder with JS and CSS files
- All file paths in `index.html` should start with `./` for relative paths

### 7. Test Locally
Before deploying, test the production build locally:
```bash
npm run build
npx serve -s dist
```

## Quick Fix Steps

1. **Check the console** for JavaScript errors (press F12 in browser)
2. **Verify GitHub Pages** is configured to use the correct branch
3. **Rebuild and redeploy** your project:
   - Make a small change to your code
   - Commit and push to trigger GitHub Actions
   - Or manually rebuild and push to gh-pages branch

## Additional Debugging

If the problem persists:

1. Check the Network tab in developer tools to see if any assets failed to load
2. Verify that all paths in the built `index.html` file are relative (start with `./`)
3. Ensure your GitHub repository name doesn't have special characters that might cause path issues

## Successful Deployment Check

Your site should be available at:
`https://[your-username].github.io/[your-repo-name]/`

For example: `https://construction-team.github.io/zhk-construction-chat/`

The beautiful construction-themed chat interface with the ЖК branding should load properly with:
- Blue construction-themed header with hard hat icon
- Message bubbles with user avatars
- Functional message input at the bottom
- Grid background pattern evoking construction blueprints