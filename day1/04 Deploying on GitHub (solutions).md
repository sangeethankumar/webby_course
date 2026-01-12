# Deploying Your Hugo Site to GitHub Pages - SOLUTIONS

Deployment means making your website accessible on the internet so others can visit it. Until now, your Hugo site has only existed on your local computer. GitHub Pages provides free hosting for static websites, making it an ideal platform for Hugo sites.

This workshop covers deploying your Hugo portfolio to GitHub Pages using GitHub Actions for automated builds. You will see your site live on the internet, understand how the deployment process works, and practice continuous deployment where changes automatically go live.

Here we will see:

- how to prepare your site for deployment using Git and GitHub
- how to deploy your Hugo site to GitHub Pages using the official Hugo workflow
- how GitHub Actions automates building and deploying your site
- how to practice continuous deployment by making changes that automatically go live

---

## Initial Setup: Preparing Your Site for Deployment

Before deploying to GitHub Pages, your Hugo site needs to be in a GitHub repository. GitHub is a platform for hosting code and collaborating on projects. Git is the version control system that tracks changes to your files.

This initial setup covers initializing Git in your Hugo site directory, creating a repository on GitHub, and pushing your site files to GitHub. These steps prepare your site for deployment.

| Command | Description |
|---------|-------------|
| `git init` | Initialize a Git repository in the current directory |
| `git status` | Show which files are tracked, untracked, or changed |
| `git add <file>` | Stage files for commit |
| `git add .` | Stage all files in the current directory |
| `git commit -m "message"` | Save staged changes with a descriptive message |
| `git remote add origin <url>` | Connect your local repository to GitHub |
| `git push -u origin main` | Push commits to GitHub (first time) |
| `git push` | Push commits to GitHub (after initial setup) |

---

### Understanding Git and Version Control

Git is a version control system that tracks changes to files over time. When you initialize Git in a directory, it creates a hidden `.git` folder that stores the complete history of changes. This allows you to see what changed, when it changed, and revert to previous versions if needed.

Version control is essential for deployment because it provides a reliable way to track what code is running on your live site. Every change is recorded with a message describing what was done.

---

**Example** Navigate to your Hugo site directory and initialize Git. Check the status to see all the untracked files that Git can now track.

```bash
cd my-portfolio
git init
git status
```

You should see output showing many untracked files including `hugo.toml`, the `content/` directory, `themes/`, and other Hugo files.

---

### Creating a GitHub Repository

GitHub is a web platform that hosts Git repositories. It stores your code online, provides collaboration tools, and offers GitHub Pages for free website hosting. To deploy your Hugo site, you need to create a repository on GitHub where your code will live.

A repository (or "repo") is a project folder that contains all your files and their complete history. For GitHub Pages to work, your repository must be public so GitHub can serve the files as a website.

---

**Example** Go to GitHub in your browser (https://github.com) and log in to your account. In the top right corner, click the "+" icon and select "New repository" from the dropdown menu. Name your repository `my-portfolio`, keep it public, and do not check any boxes to initialize with a README, .gitignore, or license. Click "Create repository".

After creating the repository, GitHub shows a page with setup instructions. You will see a URL that looks like `https://github.com/username/my-portfolio.git` where `username` is your GitHub username.

---

### Pushing Your Site to GitHub

After creating a GitHub repository, you need to connect your local Hugo site to it and upload (push) your files. This involves three Git commands: `add` stages files for commit, `commit` saves the changes with a message, and `push` uploads to GitHub.

The first push requires `git push -u origin main` which sets up tracking between your local `main` branch and GitHub's `main` branch. After this initial setup, you can use just `git push` for future uploads.

---

**Example** In your terminal (still in your Hugo site directory), stage all files, commit them with a message, connect to your GitHub repository, and push everything to GitHub.

```bash
git add .
git commit -m "Initial Hugo site"
git remote add origin https://github.com/YOUR-USERNAME/my-portfolio.git
git push -u origin main
```

Replace `YOUR-USERNAME` with your actual GitHub username in the repository URL. You may be prompted to authenticate with GitHub.

---

## Section 1: Deploying to GitHub Pages

Now that your Hugo site is on GitHub, you can deploy it to GitHub Pages to make it accessible on the internet. Hugo's official documentation provides a complete GitHub Actions workflow that automates building and deploying your site.

GitHub Actions is a system that runs automated tasks (workflows) when specific events happen, like pushing code. The workflow file tells GitHub Actions to build your Hugo site and publish it to GitHub Pages every time you push changes.

This section covers copying the official Hugo deployment workflow, configuring your site's base URL, enabling GitHub Pages in your repository settings, and verifying your live site. By the end of this section, your portfolio will be accessible at a public URL.

Reference: Hugo's official GitHub Pages hosting documentation at https://gohugo.io/hosting-and-deployment/hosting-on-github/

| Command | Description |
|---------|-------------|
| `mkdir -p <path>` | Create a directory and any necessary parent directories |
| `git add <file>` | Stage specific files for commit |
| `git commit -m "message"` | Save staged changes with a descriptive message |
| `git push` | Push commits to GitHub (triggers deployment) |

| File/Directory | Description |
|----------------|-------------|
| `.github/workflows/` | Directory where GitHub Actions workflow files are stored |
| `hugo.yml` | Workflow file that defines build and deployment steps |
| `baseURL` | Configuration setting in `hugo.toml` for the site's final URL |

---

### Copying the Deployment Workflow from Hugo Docs

GitHub Actions workflows are defined in YAML files stored in the `.github/workflows/` directory of your repository. When GitHub detects a workflow file, it automatically runs the workflow according to its trigger conditions.

Hugo's official documentation provides a complete, tested workflow file that handles everything needed to deploy a Hugo site to GitHub Pages. The workflow installs necessary tools (Hugo, Go, Node.js, Dart Sass), builds the site with caching for faster builds, and deploys it to GitHub Pages.

---

**Example** Visit Hugo's GitHub Pages hosting documentation at https://gohugo.io/hosting-and-deployment/hosting-on-github/ and locate the complete workflow YAML code under the "GitHub Actions" section.

In your terminal, create the necessary directory structure for GitHub Actions workflows:

```bash
mkdir -p .github/workflows
```

Create a new file named `hugo.yml` in the `.github/workflows/` directory using your text editor. Copy the complete workflow YAML from Hugo's documentation and paste it into your `.github/workflows/hugo.yml` file. The workflow should start with:

```yaml
name: Build and deploy
on:
  push:
    branches:
      - main
  workflow_dispatch:
```

Save the file.

---

### Configuring Your Site's Base URL

The `baseURL` setting in `hugo.toml` tells Hugo what the final URL of your website will be. This is important because Hugo uses this URL to generate correct links for navigation, stylesheets, and other assets.

For GitHub Pages, the URL format is `https://username.github.io/repository-name/` where `username` is your GitHub username and `repository-name` is your repository name. The trailing slash at the end is important for proper URL generation.

---

**Example** Open `hugo.toml` in your text editor. At or near the top of the file, add or modify the `baseURL` line:

```toml
baseURL = 'https://YOUR-USERNAME.github.io/my-portfolio/'
```

Replace `YOUR-USERNAME` with your actual GitHub username. Make sure there is a trailing slash at the end. Save the file.

---

### Deploying Your Site

Now you will push both the workflow file and the updated configuration to GitHub. This will trigger the GitHub Actions workflow for the first time. You will then enable GitHub Pages in your repository settings to allow the workflow to deploy your site.

---

**Example** Stage, commit, and push both files to GitHub:

```bash
git add .github/workflows/hugo.yml hugo.toml
git commit -m "Add deployment workflow and configure baseURL"
git push
```

Navigate to your repository on GitHub. Click the "Actions" tab at the top. You should see a workflow run starting with the name "Build and deploy". The workflow will show as running (yellow circle) or may fail (red X) because GitHub Pages is not enabled yet.

Now enable GitHub Pages. Click the "Settings" tab, scroll down in the left sidebar and click "Pages". Under "Build and deployment", find the "Source" dropdown and select "GitHub Actions".

Go back to the "Actions" tab. The workflow should automatically run again. Wait for it to complete with a green checkmark.

---

**Exercise** After the workflow completes successfully, go to Settings → Pages. At the top, you should see "Your site is live at" followed by your URL. Click "Visit site" or copy the URL and open it in a new browser tab. Verify:
1. Your site loads without errors
2. Your theme styling is applied correctly
3. Your content is visible on the homepage
4. The site title appears in the browser tab

**Solution:**
Your live site should be accessible at: `https://YOUR-USERNAME.github.io/my-portfolio/`

Expected results:
1. ✅ Page loads with Beautiful Hugo theme styling
2. ✅ Navigation bar appears at top
3. ✅ Your homepage content displays
4. ✅ Browser tab shows your site title from `hugo.toml`

If the site doesn't load:
- Verify the workflow has a green checkmark in Actions tab
- Check that GitHub Pages source is set to "GitHub Actions" in Settings → Pages
- Verify your `baseURL` in `hugo.toml` matches the GitHub Pages URL exactly (including trailing slash)

---

**Exercise** Bookmark your GitHub Pages URL (https://YOUR-USERNAME.github.io/my-portfolio/). Keep this tab open. You will use this URL throughout the workshop to verify changes.

**Solution:**
Use your browser's bookmark feature (Ctrl+D or Cmd+D) to save:
```
https://YOUR-USERNAME.github.io/my-portfolio/
```

Keep this tab open and positioned next to your text editor for easy reference throughout the workshop.

---

## Section 2: Understanding and Modifying the Workflow

Your site is now deployed and accessible on the internet. The GitHub Actions workflow handles the entire build and deployment process automatically. Now you will understand what the workflow does by making changes to it and observing the results.

This section focuses on modifying the workflow file, seeing how those modifications affect the build process in the logs, and verifying the site still works. Each exercise follows a complete cycle: modify the workflow → commit and push → watch the workflow run → examine the logs → verify the live site.

| YAML Syntax | Description |
|-------------|-------------|
| `name:` | Human-readable name for the workflow or step |
| `on:` | Events that trigger the workflow to run |
| `jobs:` | Collection of related tasks that run in the workflow |
| `steps:` | Individual tasks within a job |
| `uses:` | Runs a pre-built action from GitHub Marketplace |
| `run:` | Executes a shell command |
| `env:` | Environment variables for the job |
| `needs:` | Specifies job dependencies (which jobs must complete first) |

---

### Understanding Workflow Structure Through Modification

The workflow you copied has two main jobs: `build` and `deploy`. The build job installs tools, builds the Hugo site, and uploads the result. The deploy job publishes the built site to GitHub Pages. The workflow uses environment variables to specify exact versions of tools.

You will understand how the workflow is structured by making small modifications and observing what changes in the build process.

---

**Example** Open `.github/workflows/hugo.yml` and examine the `env:` section in the build job:

```yaml
env:
  DART_SASS_VERSION: 1.97.2
  GO_VERSION: 1.25.5
  HUGO_VERSION: 0.154.4
  NODE_VERSION: 24.12.0
  TZ: Europe/Oslo
```

These environment variables define which versions of tools to install. The workflow references these variables in the installation steps.

---

**Exercise** Change the `HUGO_VERSION` to a different version. You can find Hugo versions at https://github.com/gohugoio/hugo/releases (choose any recent version like `0.140.0`). Save the file, commit with message "Update Hugo version", and push. Watch the workflow run in the Actions tab. Once it completes:
1. Verify the workflow has a green checkmark
2. Click on the workflow run, click the "build" job, expand the "Verify installations" step
3. Verify the log shows your specified Hugo version (look for "Hugo: v0.140.0" or similar)
4. Refresh your live site and verify it still loads correctly

**Solution:**

In `.github/workflows/hugo.yml`, change:
```yaml
env:
  DART_SASS_VERSION: 1.97.2
  GO_VERSION: 1.25.5
  HUGO_VERSION: 0.140.0
  NODE_VERSION: 24.12.0
  TZ: Europe/Oslo
```

Commands:
```bash
git add .github/workflows/hugo.yml
git commit -m "Update Hugo version"
git push
```

Verification:
1. Go to Actions tab → See new workflow run starting
2. Wait for green checkmark (30-90 seconds)
3. Click the workflow run → Click "build" job
4. Expand "Verify installations" step
5. Look for output line: `Hugo: v0.140.0/extended linux/amd64 BuildDate=...`
6. Refresh live site → Verify it loads correctly

Expected log output:
```
Dart Sass: 1.97.2 compiled with dart2js 3.x.x
Go: go version go1.25.5 linux/amd64
Hugo: v0.140.0/extended linux/amd64 BuildDate=...
Node.js: v24.12.0
```

---

**Exercise** Change the `TZ` environment variable to your local timezone (like `America/New_York`, `Asia/Tokyo`, or `Europe/London`). Commit with message "Update timezone", push, and verify:
1. Workflow completes successfully (green checkmark)
2. In the build job logs, the timezone is reflected in timestamps
3. Your live site still works correctly

**Solution:**

In `.github/workflows/hugo.yml`, change:
```yaml
env:
  DART_SASS_VERSION: 1.97.2
  GO_VERSION: 1.25.5
  HUGO_VERSION: 0.140.0
  NODE_VERSION: 24.12.0
  TZ: America/New_York
```

Commands:
```bash
git add .github/workflows/hugo.yml
git commit -m "Update timezone"
git push
```

Verification:
1. Actions tab → New workflow run appears
2. Green checkmark after completion
3. Click workflow → "build" job
4. Look at timestamps in any step - they should reflect your timezone
5. Refresh live site → Still works

Note: The timezone primarily affects timestamps in the build logs and any date/time operations during the build process.

---

### Adding Debugging Information to the Workflow

The workflow includes a "Verify installations" step that prints version information for installed tools. You can add additional debugging steps to understand what happens during the build process. Adding echo statements helps you see what the workflow is doing at each stage.

---

**Exercise** Add a new step after the "Checkout" step to print the current directory and list files. Open `hugo.yml` and add this step after the Checkout step (maintain proper YAML indentation - it should align with other steps):

```yaml
- name: Debug - Show repository contents
  run: |
    echo "Current directory: $(pwd)"
    echo "Files in repository:"
    ls -la
```

Commit with message "Add debug step to show files", push, and verify:
1. Workflow runs successfully (green checkmark in Actions)
2. In the build job logs, expand the "Debug - Show repository contents" step
3. Verify you can see your repository files listed in the output (hugo.toml, content/, .github/, etc.)
4. Refresh your live site and verify it still works

**Solution:**

In `.github/workflows/hugo.yml`, find the "Checkout" step and add the debug step immediately after it:

```yaml
jobs:
  build:
    runs-on: ubuntu-latest
    env:
      # ... environment variables ...
    steps:
      - name: Checkout
        uses: actions/checkout@v6
        with:
          submodules: recursive
          fetch-depth: 0
      - name: Debug - Show repository contents
        run: |
          echo "Current directory: $(pwd)"
          echo "Files in repository:"
          ls -la
      - name: Setup Go
        # ... rest of workflow ...
```

Commands:
```bash
git add .github/workflows/hugo.yml
git commit -m "Add debug step to show files"
git push
```

Verification:
1. Actions tab → New workflow run
2. Green checkmark after completion
3. Click workflow → "build" job
4. Find and expand "Debug - Show repository contents" step
5. Should see output like:
```
Current directory: /home/runner/work/my-portfolio/my-portfolio
Files in repository:
total 32
drwxr-xr-x  7 runner docker 4096 Jan 12 10:00 .
drwxr-xr-x  3 runner docker 4096 Jan 12 10:00 ..
drwxr-xr-x  2 runner docker 4096 Jan 12 10:00 archetypes
drwxr-xr-x  2 runner docker 4096 Jan 12 10:00 content
drwxr-xr-x  3 runner docker 4096 Jan 12 10:00 .github
-rw-r--r--  1 runner docker  234 Jan 12 10:00 hugo.toml
...
```
6. Refresh live site → Still works

---

**Exercise** Add another debug step after "Build the site" to show what files were generated. Add this step after the "Build the site" step:

```yaml
- name: Debug - Show built files
  run: |
    echo "Built site files in public/ directory:"
    ls -la public/
```

Commit with message "Add debug step to show built files", push, and verify:
1. Workflow completes successfully
2. In the build logs, expand the "Debug - Show built files" step
3. Verify you see HTML files, CSS files, and other assets in the public/ directory listing
4. Live site still works correctly

**Solution:**

In `.github/workflows/hugo.yml`, find the "Build the site" step and add the debug step immediately after it:

```yaml
- name: Build the site
  run: |
    hugo \
      --gc \
      --minify \
      --baseURL "${{ steps.pages.outputs.base_url }}/" \
      --cacheDir "${{ runner.temp }}/hugo_cache"
- name: Debug - Show built files
  run: |
    echo "Built site files in public/ directory:"
    ls -la public/
- name: Cache save
  # ... rest of workflow ...
```

Commands:
```bash
git add .github/workflows/hugo.yml
git commit -m "Add debug step to show built files"
git push
```

Verification:
1. Actions tab → New workflow run
2. Green checkmark
3. Click workflow → "build" job
4. Expand "Debug - Show built files" step
5. Should see output showing generated HTML, CSS, JS files:
```
Built site files in public/ directory:
total 248
drwxr-xr-x 8 runner docker  4096 Jan 12 10:05 public
drwxr-xr-x 2 runner docker  4096 Jan 12 10:05 css
drwxr-xr-x 2 runner docker  4096 Jan 12 10:05 js
-rw-r--r-- 1 runner docker 12345 Jan 12 10:05 index.html
-rw-r--r-- 1 runner docker  8192 Jan 12 10:05 sitemap.xml
...
```
6. Refresh live site → Still works

---

### Understanding Build Steps Through Modification

The "Build the site" step runs the Hugo command with several flags. You can modify these flags to change how Hugo builds your site. Understanding what each flag does helps you troubleshoot issues and optimize your build.

---

**Exercise** The build step includes `--minify` which reduces file sizes by removing unnecessary whitespace and compressing code. Temporarily remove this flag to see the difference. Find the "Build the site" step and change it to:

```yaml
- name: Build the site
  run: |
    hugo \
      --gc \
      --baseURL "${{ steps.pages.outputs.base_url }}/" \
      --cacheDir "${{ runner.temp }}/hugo_cache"
```

(Notice `--minify` is removed). Commit with message "Test build without minify", push, and verify:
1. Workflow runs successfully
2. In the build logs, the "Build the site" step shows the command without --minify
3. Live site still works (but files may be slightly larger if you inspect them)

Now add `--minify` back to the build command, commit with message "Restore minify flag", push, and verify workflow succeeds and site still works.

**Solution:**

First, remove `--minify`:

In `.github/workflows/hugo.yml`:
```yaml
- name: Build the site
  run: |
    hugo \
      --gc \
      --baseURL "${{ steps.pages.outputs.base_url }}/" \
      --cacheDir "${{ runner.temp }}/hugo_cache"
```

Commands:
```bash
git add .github/workflows/hugo.yml
git commit -m "Test build without minify"
git push
```

Verification:
1. Actions tab → New workflow run
2. Green checkmark
3. Click workflow → "build" job → Expand "Build the site"
4. Command shown should be:
```
hugo --gc --baseURL "https://YOUR-USERNAME.github.io/my-portfolio/" --cacheDir "/tmp/hugo_cache"
```
(no --minify flag)
5. Refresh live site → Still works (HTML source may have more whitespace if you inspect)

Then, restore `--minify`:

In `.github/workflows/hugo.yml`:
```yaml
- name: Build the site
  run: |
    hugo \
      --gc \
      --minify \
      --baseURL "${{ steps.pages.outputs.base_url }}/" \
      --cacheDir "${{ runner.temp }}/hugo_cache"
```

Commands:
```bash
git add .github/workflows/hugo.yml
git commit -m "Restore minify flag"
git push
```

Verification:
1. New workflow run → Green checkmark
2. Build log shows `--minify` flag back in command
3. Live site still works

---

### Understanding Workflow Triggers

The workflow has two triggers: it runs when you push to the main branch (`push:`), and it can be manually triggered (`workflow_dispatch:`). Understanding triggers helps you control when deployments happen.

---

**Exercise** Manually trigger the workflow without making any code changes. Go to the Actions tab on GitHub, click on "Build and deploy" in the left sidebar, then click the "Run workflow" button (this button appears because of `workflow_dispatch`). Select the main branch and click "Run workflow". Verify:
1. A new workflow run appears and completes successfully (green checkmark)
2. The workflow run shows "workflow_dispatch" as the trigger event (not "push")
3. Your live site is unchanged (since no code changed)
4. This demonstrates you can trigger deployments manually without pushing code

**Solution:**

Steps:
1. Go to your repository on GitHub
2. Click "Actions" tab
3. In the left sidebar, click "Build and deploy"
4. On the right side, click the "Run workflow" dropdown button
5. Select branch: "main"
6. Click green "Run workflow" button
7. A new workflow run appears immediately

Verification:
1. Workflow run appears in the list
2. After ~30-90 seconds, green checkmark appears
3. Click on the workflow run title
4. Under the run title, you'll see "workflow_dispatch" instead of commit message
5. Refresh live site → No changes (expected, since no code changed)

This is useful for:
- Re-deploying without making changes
- Testing the deployment pipeline
- Manually triggering after fixing GitHub Pages settings

---

## Section 3: Practicing Continuous Deployment

Continuous Deployment (CD) means your changes automatically go live on the internet without manual intervention. Every time you push to GitHub, your workflow rebuilds the site and deploys the updates. This section focuses on practicing this workflow repeatedly to build muscle memory.

You will make various types of changes - content updates, configuration modifications - following the same pattern each time: edit files locally, stage changes, commit with a descriptive message, push to GitHub, watch the workflow run, and verify on the live site.

| Git Workflow | Description |
|--------------|-------------|
| Edit → Save | Make changes to files in your text editor |
| `git status` | Check which files changed |
| `git add <file>` | Stage specific files |
| `git commit -m "message"` | Commit with descriptive message |
| `git push` | Push to GitHub (triggers deployment) |
| Watch Actions | Monitor workflow run |
| Verify | Check live site after workflow completes |

---

### Making Content Changes

Content changes are the most common updates you will make to your portfolio. These include adding new paragraphs, updating existing text, or modifying your bio. Each content change follows the complete CD workflow: edit → commit → push → watch workflow → verify live site.

---

**Exercise** Add a new paragraph to your homepage about a skill or interest. Open `content/_index.md` and add a paragraph at the end like:

```markdown
I am particularly interested in machine learning applications and have experience working with Python and data visualization libraries.
```

Save, commit with message "Add information about ML skills", push, and verify:
1. Watch the workflow run in the Actions tab (starts automatically after push)
2. Wait for the green checkmark (typically 30-90 seconds)
3. Refresh your live site
4. Verify the new paragraph appears on your homepage

**Solution:**

In `content/_index.md`, add to the end (after your existing content, before any closing delimiters):

```markdown
---
title: "Home"
date: 2025-01-10T12:00:00+01:00
draft: false
---

[Your existing content here...]

I am particularly interested in machine learning applications and have experience working with Python and data visualization libraries.
```

Commands:
```bash
git add content/_index.md
git commit -m "Add information about ML skills"
git push
```

Verification:
1. Actions tab → New workflow run starts immediately
2. Wait for green checkmark (~30-90 seconds)
3. Go to your live site tab
4. Refresh the page (Ctrl+R or Cmd+R)
5. Scroll to bottom of homepage
6. ✅ New paragraph appears: "I am particularly interested in machine learning..."

Time the cycle: Start timer at `git push`, stop when you see the change live. Typical time: 30-90 seconds total.

---

**Exercise** Edit existing text on your homepage. Change a sentence, fix a typo, or reword something. Commit with message "Update homepage text", push, and verify:
1. Workflow runs successfully
2. Workflow completes in similar time as before
3. Your edit appears on the live site
4. Time how long the complete cycle takes from push to seeing the change live

**Solution:**

In `content/_index.md`, modify any existing sentence. For example, change:
```markdown
I am a researcher working on interesting problems in data science.
```
To:
```markdown
I am a computational researcher specializing in data science and machine learning.
```

Commands:
```bash
git add content/_index.md
git commit -m "Update homepage text"
git push
```

Verification:
1. Actions tab → New workflow run
2. Green checkmark after ~30-90 seconds
3. Refresh live site
4. ✅ Modified text appears

Timing exercise:
- Start stopwatch when you run `git push`
- Stop when you see the change on the live site
- Typical time: 30-90 seconds (varies based on GitHub Actions queue)

---

**Exercise** Add another paragraph about your educational background. Commit with message "Add education background", push, and verify the complete cycle (workflow runs, completes with green check, change appears live).

**Solution:**

In `content/_index.md`, add:

```markdown
I hold a PhD in Computer Science from Stanford University, where I focused on machine learning applications in computational biology. Prior to that, I completed my undergraduate degree in Mathematics and Computer Science.
```

Commands:
```bash
git add content/_index.md
git commit -m "Add education background"
git push
```

Verification:
1. Actions tab → Workflow runs
2. Green checkmark appears
3. Refresh live site
4. ✅ Education paragraph appears on homepage

---

### Making Configuration Changes

Configuration changes affect how your site behaves or appears. These changes happen in `hugo.toml`. Like content changes, they follow the same CD workflow pattern.

---

**Exercise** Change your site title. Open `hugo.toml` and modify the `title` line (near the top):

```toml
title = 'Your Name - Data Science Portfolio'
```

Commit with message "Update site title", push, and verify:
1. Workflow runs successfully (green checkmark)
2. Workflow completes
3. Refresh your live site
4. Verify the new title appears in the browser tab and site header

**Solution:**

In `hugo.toml`, change the title line:

```toml
baseURL = 'https://YOUR-USERNAME.github.io/my-portfolio/'
title = 'Jane Smith - Data Science Portfolio'

[module]
[[module.imports]]
path = "github.com/halogenica/beautifulhugo"

[params]
# ... rest of config ...
```

Commands:
```bash
git add hugo.toml
git commit -m "Update site title"
git push
```

Verification:
1. Actions tab → Workflow runs → Green checkmark
2. Refresh live site
3. ✅ Browser tab shows: "Jane Smith - Data Science Portfolio"
4. ✅ Site header shows the new title

---

**Exercise** If you have a `subtitle` parameter in the `[params]` section, update it to describe your work. If you don't have one, add it:

```toml
[params]
subtitle = "Machine Learning Engineer | Data Scientist"
```

Commit with message "Update subtitle", push, and verify:
1. Workflow completes successfully
2. Subtitle appears on your live site in the header area

**Solution:**

In `hugo.toml`, add or modify in the `[params]` section:

```toml
[params]
subtitle = "Machine Learning Engineer | Data Scientist"
author = "Your Name"
# ... rest of params ...
```

If `[params]` doesn't exist, add it after the `[module]` section:

```toml
[module]
[[module.imports]]
path = "github.com/halogenica/beautifulhugo"

[params]
subtitle = "Machine Learning Engineer | Data Scientist"
```

Commands:
```bash
git add hugo.toml
git commit -m "Update subtitle"
git push
```

Verification:
1. Actions tab → Workflow runs → Green checkmark
2. Refresh live site
3. ✅ Subtitle appears below site title in header: "Machine Learning Engineer | Data Scientist"

---

**Exercise** Make multiple changes at once: update your site title AND add/modify a paragraph in your content. Stage both files with `git add hugo.toml content/_index.md`, commit with message "Update site title and content", push, and verify:
1. Single workflow run handles both changes (only one workflow appears in Actions)
2. Workflow completes successfully
3. Both changes appear on the live site after deployment
4. In your GitHub repository, view the commit history to see one commit containing both file changes

**Solution:**

1. In `hugo.toml`, change the title:
```toml
title = 'Dr. Jane Smith - Research Portfolio'
```

2. In `content/_index.md`, add or modify content:
```markdown
My research interests span machine learning, computational biology, and data visualization. I am particularly focused on developing interpretable AI models for healthcare applications.
```

Commands:
```bash
git add hugo.toml content/_index.md
git commit -m "Update site title and content"
git push
```

Verification:
1. Actions tab → Only ONE new workflow run appears
2. Green checkmark after completion
3. Refresh live site
4. ✅ Title changed in browser tab and header
5. ✅ New/modified content appears on homepage
6. Go to repository → Click on commit count (e.g., "42 commits")
7. ✅ Most recent commit shows both files changed

This demonstrates efficiency: multiple changes can be deployed in a single cycle.

---

### Understanding the Complete Git Workflow

By now you have followed the CD workflow many times. This subsection reinforces understanding of each step in the workflow and why each step matters.

---

**Exercise** Make a small change to your content (add a sentence or fix punctuation). Before committing, run `git status` to see which files changed (should show `content/_index.md` as modified). Stage the file with `git add content/_index.md`, then run `git status` again (should show file staged for commit in green). Commit with a descriptive message, run `git status` again (should show "nothing to commit, working tree clean"), then push. Observe how `git status` shows different information at each stage of the workflow.

**Solution:**

1. Edit `content/_index.md` - add a sentence:
```markdown
I enjoy collaborating with researchers from diverse backgrounds.
```

2. Check status before staging:
```bash
git status
```
Output shows:
```
On branch main
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   content/_index.md

no changes added to commit (use "git add" and/or "git commit -a")
```

3. Stage the file:
```bash
git add content/_index.md
git status
```
Output shows:
```
On branch main
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        modified:   content/_index.md
```

4. Commit:
```bash
git commit -m "Add sentence about collaboration"
git status
```
Output shows:
```
On branch main
Your branch is ahead of 'origin/main' by 1 commit.
  (use "git push" to publish your local commits)

nothing to commit, working tree clean
```

5. Push:
```bash
git push
```

6. Check status after push:
```bash
git status
```
Output shows:
```
On branch main
Your branch is up to date with 'origin/main'.

nothing to commit, working tree clean
```

Key observations:
- Before staging: file shown in red as "modified"
- After staging: file shown in green as "Changes to be committed"
- After commit: "nothing to commit" but ahead of origin
- After push: everything up to date

---

**Exercise** Make three small changes to different files: one content change in `_index.md`, one config change in `hugo.toml`, and one comment in your workflow file `hugo.yml`. Use `git status` to verify all three files show as modified. Stage all three with `git add .`, commit them together in a single commit with message "Multiple site updates", push, and verify:
1. Single workflow run (one entry in Actions tab)
2. Workflow completes successfully
3. All changes are included in the deployment
4. All changes appear on the live site

**Solution:**

1. Make three changes:

In `content/_index.md`:
```markdown
I have published research in top-tier conferences and journals.
```

In `hugo.toml`:
```toml
title = 'Dr. Jane Smith - ML Research'
```

In `.github/workflows/hugo.yml`, add a comment:
```yaml
# This workflow builds and deploys the Hugo site to GitHub Pages
name: Build and deploy
```

2. Check all files are modified:
```bash
git status
```
Output should show:
```
On branch main
Changes not staged for commit:
        modified:   .github/workflows/hugo.yml
        modified:   content/_index.md
        modified:   hugo.toml
```

3. Stage all at once:
```bash
git add .
git status
```
Output shows all three in green:
```
Changes to be committed:
        modified:   .github/workflows/hugo.yml
        modified:   content/_index.md
        modified:   hugo.toml
```

4. Commit and push:
```bash
git commit -m "Multiple site updates"
git push
```

Verification:
1. Actions tab → ONE workflow run appears (not three)
2. Green checkmark after completion
3. Refresh live site
4. ✅ Title changed
5. ✅ New content sentence appears
6. Click the workflow run in Actions
7. The build still succeeds (comment doesn't affect functionality)
8. On GitHub, view the commit - shows all 3 files in one commit

---

**Exercise** Practice the complete workflow one more time with any change you want (content, config, or both). Focus on executing the pattern smoothly without referring to notes: edit → save → `git add` → `git commit -m` → `git push` → watch Actions → refresh live site → verify. This pattern is fundamental to modern web development.

**Solution:**

Choose your own change. Example:

1. Edit `content/_index.md` - add interests:
```markdown
Outside of research, I enjoy hiking, photography, and contributing to open source projects.
```

2. Execute the workflow from memory:
```bash
git add content/_index.md
git commit -m "Add personal interests"
git push
```

3. Verify:
- Actions tab → workflow runs
- Green checkmark
- Refresh live site
- New content appears

Goal: Execute this pattern smoothly in under 2 minutes from edit to verification. This muscle memory is essential for continuous deployment workflows.

Common workflow shortcuts:
- `git add .` - stages all changes
- `git commit -am "message"` - stages and commits tracked files in one command
- Set up VS Code or your editor to run git commands with shortcuts

---

**Exercise** Visit 3-5 other students' portfolios at their GitHub Pages URLs. Note what you like about each portfolio. Share feedback with your peers about what makes each portfolio effective - consider content clarity, design choices, professional presentation, and technical implementation.

**Solution:**

Visit portfolio URLs in format: `https://USERNAME.github.io/my-portfolio/`
---