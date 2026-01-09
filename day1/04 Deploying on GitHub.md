# Deploying Your Hugo Site to GitHub Pages

You have been building and viewing your Hugo site locally using the development server. Your site exists only on your computer. This section shows how to publish your site so others can access it on the web.

Hugo generates static HTML files that can be hosted on any web server. GitHub Pages provides free hosting for static sites. GitHub Actions automates the build and deployment process. When you push changes to your repository, GitHub Actions runs Hugo automatically and publishes the updated site.

You will initialize your Hugo site as a Git repository, connect it to GitHub, adjust the configuration for production, set up GitHub Actions to build the site automatically, and enable GitHub Pages to serve the built site.

---

## Section 1: Initializing Git and Connecting to GitHub

Your Hugo site exists as a directory containing source files on your computer. Git provides version control for these files. GitHub stores the repository remotely and provides access to GitHub Actions and GitHub Pages services.

### Creating a Git repository

Git tracks changes to your files through a hidden `.git` directory. When you initialize Git in your Hugo site directory, it creates this directory and begins tracking your project.

**Steps:**

1. Open your terminal and navigate to your Hugo site directory.
2. Run `git init` to initialize a Git repository.
3. Run `git status` to see the untracked files in your project.

You should see a list of files and directories including `content/`, `hugo.toml`, and other Hugo files.

---

### Creating a GitHub repository

GitHub repositories store your files remotely. A new empty repository provides a destination for your Hugo site files and access to GitHub services.

**Steps:**

1. Go to GitHub in your browser and log in.
2. Click the "+" icon in the top right corner.
3. Select "New repository" from the dropdown menu.
4. Name the repository `my-portfolio`.
5. Keep the repository **public**.
6. Do **not*- check any boxes to initialize with README, .gitignore, or license.
7. Click "Create repository".

GitHub displays a page with setup instructions and your repository URL. Keep this page open.

---

### Connecting your local repository to GitHub

Git uses a remote URL to know where to send files. The `git remote add` command connects your local repository to the GitHub repository you just created.

**Steps:**

1. In your terminal (still in your Hugo site directory), run `git add .` to stage all files.
2. Run `git commit -m "Initial Hugo site"` to commit the files.
3. Copy the repository URL from the GitHub page (it looks like `https://github.com/username/my-portfolio.git`).
4. Run `git remote add origin <repo-url>` (replace `<repo-url>` with the URL you copied).
5. Run `git push -u origin main` to push your files to GitHub.
6. Refresh the GitHub repository page in your browser.

Your Hugo files should now appear in the repository. You should see directories like `content/`, files like `hugo.toml`, and any other files from your project.

---

## Section 2: Adjusting Hugo Configuration for Production

Hugo generates links and resource paths based on the `baseURL` parameter in your configuration file. When you run Hugo locally, `baseURL` points to `localhost:1313`. For production, it must point to where your site will be hosted.

GitHub Pages serves sites at URLs in the format `https://username.github.io/repository-name/`. Setting `baseURL` to match this URL ensures that all generated links, stylesheets, and scripts point to the correct location.

### Setting the production base URL

The `baseURL` parameter in `hugo.toml` defines your site's final URL. Hugo uses this value to generate absolute URLs throughout the HTML output. Without the correct `baseURL`, CSS files, JavaScript, and internal links may fail to load or point to incorrect locations.

**Steps:**

1. Open `hugo.toml` in your text editor.
2. Find the line `baseURL = 'http://localhost:1313/'`.
3. Change it to `baseURL = 'https://username.github.io/my-portfolio/'` (replace `username` with your actual GitHub username).
4. Save the file.
5. Run `git add hugo.toml` to stage the configuration change.
6. Run `git commit -m "Update baseURL for GitHub Pages"` to commit.
7. Run `git push` to push the change to GitHub.

You can verify the change on GitHub by navigating to your repository, clicking on `hugo.toml`, and confirming the `baseURL` line shows your GitHub Pages URL.

---

## Section 3: Configuring GitHub Actions for Automated Builds

GitHub Actions reads workflow files from the `.github/workflows/` directory to determine what tasks to run when files are pushed. A workflow file defines the steps needed to build your site: checking out source files, installing Hugo, running the build command, and uploading the generated output.

### Creating the workflow file

GitHub Actions requires workflow files to be placed in a specific location. Each YAML file in `.github/workflows/` defines a workflow that runs on specified events.

**Steps:**

1. In your Hugo site root directory, create a new directory named `.github`.
2. Inside `.github`, create a subdirectory named `workflows`.
3. Inside `.github/workflows/`, create a new file named `hugo.yml`.
4. Open `.github/workflows/hugo.yml` in your text editor.

---

### Defining the workflow structure

Every GitHub Actions workflow requires a name, a trigger that specifies when to run, and a job definition. This structure is the same for any workflow regardless of what it does.

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

This workflow will run every time you push to the main branch. The `build` job will run on an Ubuntu server provided by GitHub.

---

### Adding the checkout step

The workflow needs to access your repository files. The checkout step downloads your repository, including all submodules. Hugo themes are often added as submodules, so this step ensures theme files are available.

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

Navigate to the "Actions" tab on your GitHub repository. You should see a workflow run appear. It will complete successfully but will not build the site yet because we have not added the Hugo build steps.

---

### Installing Hugo in the workflow

The GitHub Actions runner does not have Hugo installed by default. You must add a step that installs Hugo before you can run build commands.

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

Check the Actions tab again. The workflow should complete successfully with the Hugo installation step.

---

### Adding the build command

The build step runs the `hugo` command to generate your site. The `--minify` flag reduces file sizes by removing unnecessary whitespace and comments.

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

Navigate to the Actions tab and click on the most recent workflow run. You should see the "Build" step appear and run the `hugo --minify` command successfully.

---

### Configuring GitHub Pages deployment

Deploying to GitHub Pages requires specific permissions and a deployment job. The permissions allow the workflow to write to GitHub Pages. The upload step packages the built site. The deploy job depends on the build job completing successfully.

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

Navigate to the Actions tab and click on the most recent workflow run. You should see two jobs: "build" and "deploy". Both should complete successfully.

Your complete `hugo.yml` file should now contain: the workflow name and trigger, permissions for GitHub Pages, a build job that checks out code, installs Hugo, builds the site, and uploads the result, and a deploy job that publishes to GitHub Pages.

---

## Section 4: Enabling GitHub Pages and Verifying Deployment

GitHub Pages serves static files from your repository as a public website. Pages can serve files from a branch or from artifacts uploaded by GitHub Actions. You must configure GitHub Pages to use GitHub Actions as the source.

### Enabling GitHub Pages

GitHub Pages configuration specifies where to find the files to serve. Choosing GitHub Actions tells Pages to serve files from workflow artifacts rather than from a branch.

**Steps:**

1. On GitHub, navigate to your repository.
2. Click the "Settings" tab.
3. In the left sidebar, scroll down and click "Pages".
4. Under "Build and deployment", find the "Source" dropdown.
5. Select "GitHub Actions" from the dropdown.
6. Wait a few seconds for the settings to save.

GitHub Pages assigns URLs in the format `https://username.github.io/repository-name/`. This URL is determined by your GitHub username and repository name.

---

### Verifying your site is live

After the workflow completes and Pages is enabled, your site becomes accessible at the GitHub Pages URL.

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

Now that your site is deployed, any changes you push to GitHub will automatically trigger a rebuild and redeployment.

**Steps:**

1. Make a small change to `content/_index.md` (add a sentence or change some text).
2. Run `git add content/_index.md`.
3. Run `git commit -m "Update homepage content"`.
4. Run `git push`.
5. Navigate to the Actions tab on GitHub.
6. Watch the new workflow run appear and progress through the build and deploy steps.
7. Once the workflow completes (green checkmark appears), refresh your GitHub Pages URL in the browser.
8. Verify that the change you made now appears on the live site.

If a workflow fails, it will show a red X icon. Click on the failed run, then click on the failed job, and click on the failed step to read the error log. Common failures include incorrect Hugo version, missing files, or syntax errors in the workflow file.

Your Hugo site is now published and configured for automatic deployment. Every time you push changes to GitHub, your site will rebuild and update automatically.

---