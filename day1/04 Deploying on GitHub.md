# Deploying Your Hugo Site to GitHub Pages

---

## Section 1: Initializing Git and Connecting to GitHub

### Creating a Git repository

Git tracks changes to your files through a hidden `.git` directory. When you initialize Git in your Hugo site directory, it creates this directory and begins tracking your project.

**Steps:**

1. Open your terminal and navigate to your Hugo site directory.
2. Run `git init` to initialize a Git repository.
3. Run `git status` to see the untracked files in your project.

---

### Creating a GitHub repository

**Steps:**

1. Go to GitHub in your browser and log in.
2. Click the "+" icon in the top right corner.
3. Select "New repository" from the dropdown menu.
4. Name the repository `my-portfolio`.
5. Keep the repository **public**.
6. Do **not*- check any boxes to initialize with README, .gitignore, or license.
7. Click "Create repository".

---

### Connecting your local repository to GitHub

**Steps:**

1. In your terminal (still in your Hugo site directory), run `git add .` to stage all files.
2. Run `git commit -m "Initial Hugo site"` to commit the files.
3. Copy the repository URL from the GitHub page (it looks like `https://github.com/username/my-portfolio.git`).
4. Run `git remote add origin <repo-url>` (replace `<repo-url>` with the URL you copied).
5. Run `git push -u origin main` to push your files to GitHub.
6. Refresh the GitHub repository page in your browser.

---

## Section 2: Adjusting Hugo Configuration for Production


### Setting the production base URL

**Steps:**

1. Open `hugo.toml` in your text editor.
2. `baseURL = 'https://username.github.io/my-portfolio/'` (replace `username` with your actual GitHub username).
3. Save the file.
4. Run `git add hugo.toml` to stage the configuration change.
5. Run `git commit -m "Update baseURL for GitHub Pages"` to commit.
6. Run `git push` to push the change to GitHub.

---

## Section 3: Configuring GitHub Actions for Automated Builds

### Creating the workflow file

**Steps:**

1. In your Hugo site root directory, create a new directory named `.github`.
2. Inside `.github`, create a subdirectory named `workflows`.
3. Inside `.github/workflows/`, create a new file named `hugo.yml`.
4. Open `.github/workflows/hugo.yml` in your text editor.

---

### Defining the workflow structure

**Steps:**

1. Add the following to `hugo.yml`:
   ```yaml
   name: Deploy Hugo site to Pages

   on:
     push:
       branches:
         - main

   jobs:
     build:
       runs-on: ubuntu-latest
       steps:
   ```
2. Save the file.

---

### Adding the checkout step

**Steps:**

1. Add the following under `steps:` in `hugo.yml`:
   ```yaml
         - name: Checkout
           uses: actions/checkout@v4
           with:
             submodules: recursive
             fetch-depth: 0
   ```
2. Save the file.
3. Run `git add .github/workflows/hugo.yml`.
4. Run `git commit -m "Add workflow with checkout step"`.
5. Run `git push`.

---

### Installing Hugo in the workflow

**Steps:**

1. Open `.github/workflows/hugo.yml`.
2. Add the following after the Checkout step:
   ```yaml
         - name: Setup Hugo
           uses: peaceiris/actions-hugo@v2
           with:
             hugo-version: 'latest'
             extended: true
   ```
3. Save the file.
4. Run `git add .github/workflows/hugo.yml`.
5. Run `git commit -m "Add Hugo installation step"`.
6. Run `git push`.

---

### Adding the build command

**Steps:**

1. Open `.github/workflows/hugo.yml`.
2. Add the following after the Setup Hugo step:
   ```yaml
         - name: Build
           run: hugo --minify
   ```
3. Save the file.
4. Run `git add .github/workflows/hugo.yml`.
5. Run `git commit -m "Add Hugo build command"`.
6. Run `git push`.

---

### Configuring GitHub Pages deployment

**Steps:**

1. Open `.github/workflows/hugo.yml`.
2. Add the following after the `on:` section and before `jobs:`:
   ```yaml
   permissions:
     contents: read
     pages: write
     id-token: write
   ```
3. Add the following after the Build step (at the end of the build job's steps):
   ```yaml
         - name: Upload artifact
           uses: actions/upload-pages-artifact@v3
           with:
             path: ./public
   ```
4. Add the following after the entire build job (at the same indentation level as `build:`):
   ```yaml
     deploy:
       environment:
         name: github-pages
         url: ${{ steps.deployment.outputs.page_url }}
       runs-on: ubuntu-latest
       needs: build
       steps:
         - name: Deploy to GitHub Pages
           id: deployment
           uses: actions/deploy-pages@v4
   ```
5. Save the file.
6. Run `git add .github/workflows/hugo.yml`.
7. Run `git commit -m "Add GitHub Pages deployment"`.
8. Run `git push`.

---

## Section 4: Enabling GitHub Pages and Verifying Deployment

### Enabling GitHub Pages

**Steps:**

1. On GitHub, navigate to your repository.
2. Click the "Settings" tab.
3. In the left sidebar, scroll down and click "Pages".
4. Under "Build and deployment", find the "Source" dropdown.
5. Select "GitHub Actions" from the dropdown.
6. Wait a few seconds for the settings to save.

---

### Verifying your site is live

**Steps:**

1. On the Pages settings page, look at the top section where it says "Your site is live at" or "Your site is ready to be published at".
2. Note the URL displayed. It should match the `baseURL` you set in `hugo.toml`.
3. Open a new browser tab.
4. Navigate to your GitHub Pages URL (for example, `https://username.github.io/my-portfolio/`).
5. Verify your Hugo site loads with the correct theme applied.
6. Check that the title, navigation, and content all appear correctly.
7. Click through your navigation links to verify all sections load correctly.

---

### Understanding the deployment workflow

**Steps:**

1. Make a small change to `content/_index.md` (add a sentence or change some text).
2. Run `git add content/_index.md`.
3. Run `git commit -m "Update homepage content"`.
4. Run `git push`.
5. Navigate to the Actions tab on GitHub.
6. Watch the new workflow run appear and progress through the build and deploy steps.
7. Once the workflow completes (green checkmark appears), refresh your GitHub Pages URL in the browser.
8. Verify that the change you made now appears on the live site.


---