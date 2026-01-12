# Adding Media to your Portfolio - SOLUTIONS

Hugo creates multiple pages from directories containing `index.md` files. Each directory becomes a page bundle that stores content and resources together. Multiple bundles create a multi-page website structure. Bundles can be nested to create hierarchical URL paths, and menus connect pages through navigation.

Here we will see:

- how to set up a new multi-page portfolio site
- how page bundles create multiple pages
- how menus connect pages through navigation
- how to organize pages in hierarchies
- how to store resources within bundles

---

## Initial Setup

A new Hugo site will be created for the multi-page portfolio. This site will be separate from the single-page portfolio in the first document.

This section covers creating a new Hugo site with the Beautiful Hugo theme and setting up the homepage. By the end of this section, there will be a working multi-page site ready to add additional pages.

| Command | Description |
|---------|-------------|
| `hugo new site <n>` | Create a new Hugo site with the specified name |
| `cd <directory>` | Navigate into a directory |
| `hugo mod init <module-path>` | Initialize Hugo Modules for the project |
| `hugo mod get <module-path>` | Download and add a Hugo module (like a theme) |
| `hugo server -D` | Start the Hugo development server (includes draft content) |

---

### Creating the site and installing the theme

Create a new site called `multi-page-portfolio`, install the Beautiful Hugo theme, and configure basic settings.

---

**Example** Create a new Hugo site, navigate into it, initialize Hugo Modules, and install the Beautiful Hugo theme.

```bash
hugo new site multi-page-portfolio
cd multi-page-portfolio
hugo mod init github.com/yourusername/multi-page-portfolio
hugo mod get github.com/halogenica/beautifulhugo
```

---

**Example** Create a `hugo.toml` file in the site root with the following content to enable the theme:

```toml
[module]
[[module.imports]]
path = "github.com/halogenica/beautifulhugo"
```

---

**Example** Start the server and verify the theme loads. Open `http://localhost:1313/` and you should see a page with the Beautiful Hugo theme header and footer.

```bash
hugo server -D
```

---

**Exercise** Stop the server by pressing `Ctrl+C` in the terminal, then restart it with `hugo server -D` to practice the restart process.

**Solution:**
```bash
# Press Ctrl+C, then:
hugo server -D
```

---

### Creating the homepage

The homepage is the landing page at the root URL of the site. For a multi-page portfolio, the homepage contains a brief introduction and directs visitors to other pages through navigation.

---

**Example** Create a file `content/_index.md` with the following content:

```markdown
---
title: "My Portfolio"
draft: false
---

# Hello, I'm [Your Name]

I am a Research Software Engineer working with neuroscientists in the NRW region. My background is in Astronomy and Planetary Sciences.

Explore my work using the navigation above.
```

---

**Exercise** Navigate to `http://localhost:1313/` and verify the homepage displays with the welcome message.

**Solution:**
Open browser and navigate to `http://localhost:1313/`. The homepage should display with the theme styling and the welcome message.

---

**Exercise** Change the name and description in `content/_index.md` to reflect your own background, save the file, and verify the browser automatically updates with your new text.

**Solution:**
```markdown
---
title: "My Portfolio"
draft: false
---

# Hello, I'm Jane Smith

I am a Data Scientist specializing in climate modeling and machine learning. My background is in Environmental Science and Statistics.

Explore my work using the navigation above.
```
Save the file and the browser should automatically refresh showing your changes.

---

## Section 1: Creating Multiple Pages and Resources

Hugo generates a separate page for each directory that contains an `index.md` file. These directories are called page bundles. The directory name determines the page URL, and the `index.md` file provides the content. Files placed in a bundle directory alongside `index.md` become page resources that can be referenced using relative paths.

This section covers creating page bundles, understanding front matter, and adding resources like images and PDFs to bundles. By the end of this section, you will have multiple pages with embedded resources.

| Command/Concept | Description |
|-----------------|-------------|
| `index.md` | File that defines a page bundle's content |
| `draft: true/false` | Front matter setting that controls if page is published |
| `![alt text](image.jpg)` | Markdown syntax to embed images |
| `[link text](file.pdf)` | Markdown syntax to link to files |
| Relative paths | Reference files using just the filename (e.g., `photo.jpg`) |

---

### Creating page bundles

A page bundle is a directory containing an `index.md` file. Hugo reads the `index.md` file and creates a web page at a URL matching the directory name. For example, a directory `content/about/` containing `index.md` becomes a page at `/about/`.

The `index.md` file needs front matter to tell Hugo how to handle the page. Below the front matter, content is written in Markdown. Each bundle directory with `index.md` creates an independent page.

---

**Example** Create a directory `content/about/` with an `index.md` file containing content about yourself:

```markdown
---
title: "About"
draft: false
---

# About Me

During my Ph.D., I built pipelines to download, process, and analyze TESS data. I worked mainly in Python. I enjoyed this work, not just for my own research. I also helped other researchers with their code. I found it very satisfying to help others with their work.

In my current role, I work with researchers on their programming needs. This also helps me prepare for a future in industry.

## Skills

### Programming Languages
Python, R, C++, Matlab

### Frameworks
Numpy, pandas, scipy

### Tools
Git, Jupyter, Docker, LaTeX, Pixi, conda
```

---

**Exercise** Navigate to `http://localhost:1313/about/` in a browser and verify the page displays with the content.

**Solution:**
Navigate to `http://localhost:1313/about/` in browser. The page should display with the About Me content, skills sections, and theme styling.

---

**Exercise** Change some of the text in the skills section of `content/about/index.md`, save the file, and verify the change appears in the browser.

**Solution:**
```markdown
### Programming Languages
Python, R, C++, Matlab, JavaScript

### Frameworks
Numpy, pandas, scipy, TensorFlow
```
Save the file and the browser should automatically refresh showing the updated skills.

---

**Exercise** Create directory `content/projects/` with an `index.md` file containing the following content, save the file, then navigate to `http://localhost:1313/projects/` and verify the new page appears:

```markdown
---
title: "Projects"
draft: false
---

# My Projects

I have worked on several research projects involving data analysis and software development. Below are some of my key projects.
```

**Solution:**
```bash
mkdir content/projects
```
Create `content/projects/index.md` with the content shown, save, then navigate to `http://localhost:1313/projects/`. The projects page should display.

---

**Exercise** Create directory `content/publications/` with an `index.md` file containing the following content, save the file, then navigate to `http://localhost:1313/publications/` and verify this third page exists:

```markdown
---
title: "Publications"
draft: false
---

# Publications

My research has resulted in several publications in peer-reviewed journals. These papers cover topics in astronomy, planetary science, and observational techniques.
```

**Solution:**
```bash
mkdir content/publications
```
Create `content/publications/index.md` with the content shown, save, then navigate to `http://localhost:1313/publications/`. The publications page should display.

---

**Exercise** Try navigating between all three pages (`/about/`, `/projects/`, `/publications/`) to verify they all load independently.

**Solution:**
Navigate to each URL in the browser:
- `http://localhost:1313/about/`
- `http://localhost:1313/projects/`
- `http://localhost:1313/publications/`

All three pages should load with their respective content.

---

### Understanding bundle front matter

Front matter controls how Hugo handles each page. The `draft` setting determines whether the page appears when building the site. The `title` appears in the browser tab and can be used by the theme.

---

**Example** In `content/projects/index.md`, change `draft: false` to `draft: true`, save the file, then stop the server with `Ctrl+C` and restart it with `hugo server` (without the `-D` flag).

```yaml
---
title: "Projects"
draft: true
---
```

---

**Exercise** Navigate to `http://localhost:1313/projects/` and verify the page returns a 404 error because draft pages are not published without the `-D` flag.

**Solution:**
Navigate to `http://localhost:1313/projects/`. You should see a "Page Not Found" or 404 error because the page is marked as draft and the server is running without the `-D` flag.

---

**Exercise** Change `draft: true` back to `draft: false` in `content/projects/index.md`, save the file, restart the server, then navigate to `http://localhost:1313/projects/` and verify the page now loads correctly.

**Solution:**
```yaml
---
title: "Projects"
draft: false
---
```
```bash
# Press Ctrl+C, then:
hugo server
```
Navigate to `http://localhost:1313/projects/`. The page should now display correctly.

---

**Exercise** Change the `title` in `content/about/index.md` to something different like `"About Me - Background"`, save the file, and verify the new title appears in the browser tab when viewing `/about/`.

**Solution:**
```yaml
---
title: "About Me - Background"
draft: false
---
```
Save the file, navigate to `http://localhost:1313/about/`, and check the browser tab. The title should show "About Me - Background".

---

### Adding resources to bundles

Files placed in a bundle directory alongside `index.md` become page resources. These resources are referenced using relative paths. Hugo serves resources from the bundle directory when that page loads.

Hugo offers two ways to store files. The `static` directory stores files accessible from any page using absolute paths like `/images/photo.jpg`. Bundle resources store files within each page directory using relative paths like `photo.jpg`. Bundle resources are stored with the pages that reference them.

Image files placed in the bundle directory can be referenced using relative paths in Markdown. A relative path is just the filename without any leading slash. Hugo looks for the file in the same directory as the `index.md` that references it.

---

**Example** Add an image file `research-photo.jpg` to the `content/about/` directory, then add the following to `content/about/index.md` below the skills section:

```markdown

![Working with telescope data](research-photo.jpg)
```

---

**Exercise** Navigate to `http://localhost:1313/about/` and verify the image displays on the page.

**Solution:**
Place image file in `content/about/` directory. Navigate to `http://localhost:1313/about/`. The image should display below the skills section.

---

**Exercise** Add a second image file `lab-photo.jpg` to `content/about/`, add the image reference `![Lab work](lab-photo.jpg)` below the first one in the markdown file, save, then navigate to `/about/` and verify both images display.

**Solution:**
Add to `content/about/index.md`:
```markdown
![Working with telescope data](research-photo.jpg)

![Lab work](lab-photo.jpg)
```
Save the file, navigate to `http://localhost:1313/about/`. Both images should display in order.

---

**Exercise** Add a file `cv.pdf` to the `content/about/` directory, add `[Download CV](cv.pdf)` at the end of `content/about/index.md`, save the file, then navigate to `/about/`, click the link, and verify the PDF opens or downloads.

**Solution:**
Add to end of `content/about/index.md`:
```markdown

[Download CV](cv.pdf)
```
Place `cv.pdf` in `content/about/` directory. Save, navigate to `http://localhost:1313/about/`, click the "Download CV" link. The PDF should open in browser or download.

---

**Exercise** Add another PDF file `research-statement.pdf` to the `content/about/` directory, add the link `[Download Research Statement](research-statement.pdf)` below the first PDF link, save, then navigate to `/about/` and verify both PDF links work correctly.

**Solution:**
Add to `content/about/index.md`:
```markdown
[Download CV](cv.pdf)

[Download Research Statement](research-statement.pdf)
```
Place both PDF files in `content/about/` directory. Save, navigate to `http://localhost:1313/about/`. Both links should work.

---

Resources in one bundle cannot be accessed from other bundles. Each bundle's resources remain independent. This isolation prevents conflicts when different bundles have files with the same name.

---

**Example** Try adding a link `[Download CV](cv.pdf)` to `content/projects/index.md` (without adding any PDF file to the projects directory), save, then navigate to `http://localhost:1313/projects/` and click the link. You should see a 404 error because the resource does not exist in that bundle.

---

**Exercise** Remove the broken link from `content/projects/index.md`, save the file, and verify that the CV link still works correctly on the `/about/` page.

**Solution:**
Remove `[Download CV](cv.pdf)` from `content/projects/index.md` and save. Navigate to `http://localhost:1313/about/` and verify the CV link still works. Navigate to `http://localhost:1313/projects/` and verify the broken link is gone.

---

**Exercise** Add an image file named `photo.jpg` to both `content/about/` and `content/projects/` directories, add `![Photo](photo.jpg)` to both `index.md` files, save both files, then verify that each page displays its own version of the file without conflict.

**Solution:**
Place different `photo.jpg` files in both `content/about/` and `content/projects/` directories.

Add to both `content/about/index.md` and `content/projects/index.md`:
```markdown
![Photo](photo.jpg)
```

Navigate to `http://localhost:1313/about/` - should show the about directory's photo.
Navigate to `http://localhost:1313/projects/` - should show the projects directory's photo.
Each page displays its own version independently.

---

## Section 2: Connecting Pages with Navigation

Menu entries link pages together through navigation. Menu configuration in `hugo.toml` defines which pages appear in the navigation and in what order. Menus appear on all pages and allow navigation between different sections.

This section covers adding menu entries, controlling their order, and creating homepage links. By the end of this section, your site will have a fully functional navigation system.

| TOML Syntax | Description |
|-------------|-------------|
| `[[menu.main]]` | Define a menu entry in the main menu |
| `name = "text"` | The text that appears in the navigation |
| `url = "/path/"` | Where the menu item links to |
| `weight = 1` | Order of menu items (lower numbers appear first) |

---

### Adding menu entries

Menu entries are defined in the `hugo.toml` configuration file. Each entry has a name (the text that appears), a URL (where it links to), and a weight (for ordering). Hugo displays menu entries in the navigation once configured.

Multiple menu entries create multiple navigation links. Each `[[menu.main]]` block defines one menu item. Hugo displays all menu entries together in the navigation.

---

**Example** Open `hugo.toml` and add the following above the `[module]` section to create menu entries for all three pages:

```toml
[[menu.main]]
name = "About"
url = "/about/"
weight = 1

[[menu.main]]
name = "Projects"
url = "/projects/"
weight = 2

[[menu.main]]
name = "Publications"
url = "/publications/"
weight = 3
```

---

**Exercise** Save the file, reload any page in a browser, and verify three links ("About", "Projects", "Publications") now appear in navigation.

**Solution:**
Save `hugo.toml`. Reload any page in the browser. The navigation bar should now display three links: "About", "Projects", and "Publications" in that order.

---

**Exercise** Click each navigation link to verify they all navigate to the correct pages.

**Solution:**
Click "About" - should navigate to `http://localhost:1313/about/`
Click "Projects" - should navigate to `http://localhost:1313/projects/`
Click "Publications" - should navigate to `http://localhost:1313/publications/`

---

### Controlling menu order with weight

The weight value determines where each menu item appears. Lower weight values appear first in the menu. When weights are equal, Hugo typically orders items alphabetically.

---

**Example** In `hugo.toml`, change the "Publications" weight from 3 to 1, save the file, and reload any page.

```toml
[[menu.main]]
name = "Publications"
url = "/publications/"
weight = 1
```

---

**Exercise** Verify "Publications" now appears first in the menu before "About" and "Projects".

**Solution:**
Reload the page. The navigation should now show "Publications" first, followed by "About" and "Projects".

---

**Exercise** Change "About" weight to 3 in `hugo.toml`, save, reload, and verify the menu order changed again.

**Solution:**
```toml
[[menu.main]]
name = "About"
url = "/about/"
weight = 3
```
Save and reload. The navigation should now show "Publications", "Projects", then "About".

---

**Exercise** Restore a logical weight order (About=1, Projects=2, Publications=3) in `hugo.toml`, save the file, and verify the menu displays in the preferred order.

**Solution:**
```toml
[[menu.main]]
name = "About"
url = "/about/"
weight = 1

[[menu.main]]
name = "Projects"
url = "/projects/"
weight = 2

[[menu.main]]
name = "Publications"
url = "/publications/"
weight = 3
```
Save and reload. The navigation should show "About", "Projects", "Publications" in that order.

---

### Adding page links in homepage

The homepage can contain direct links to main sections. These links provide an alternative navigation method alongside the menu and can include descriptions of each section.

---

**Example** Open `content/_index.md` and add new content after the existing content:

```markdown

## Explore My Work

- [About Me](/about/) - Learn about my background and skills
- [Projects](/projects/) - View my research projects
- [Publications](/publications/) - Read my publications
```

---

**Exercise** Save and reload the homepage. Verify the links appear below the introduction.

**Solution:**
Save `content/_index.md` and navigate to `http://localhost:1313/`. The "Explore My Work" section with three links should appear below the introduction text.

---

**Exercise** Click each link and verify they navigate to the correct pages.

**Solution:**
Click "About Me" - should navigate to `/about/`
Click "Projects" - should navigate to `/projects/`
Click "Publications" - should navigate to `/publications/`

---

**Exercise** Change the description text for one of the links (e.g., change "Learn about my background and skills" to "Discover my experience and expertise"), save, reload the homepage, and verify the change appears.

**Solution:**
```markdown
- [About Me](/about/) - Discover my experience and expertise
```
Save the file and reload `http://localhost:1313/`. The updated description should appear.

---

## Section 3: Creating List Pages for Multiple Items

Some portfolio sections contain multiple items. The projects page might list several projects. The publications page might list several papers. Hugo provides a way to automatically display these items.

Hugo handles two types of pages differently. A regular page bundle uses `index.md` and displays a single page. A list page uses `_index.md` (with underscore) and can automatically display child pages within that section.

This section covers understanding the difference between `index.md` and `_index.md`, converting pages to list pages, and adding individual items. By the end of this section, your projects and publications pages will automatically list their child pages.

| Filename | Description |
|----------|-------------|
| `index.md` | Creates a single page bundle |
| `_index.md` | Creates a list page that can display child pages |
| `page-name.md` | Creates a child page within a section |

---

### Understanding index.md vs _index.md

The filename determines how Hugo treats a directory:

- `index.md` (without underscore) creates a single page bundle. The about page uses this because it displays one cohesive piece of content.
- `_index.md` (with underscore) creates a list page. List pages can have child pages, and themes typically display links to all child pages automatically.

When you need a section to contain multiple individual pages (like multiple projects or multiple publications), you convert the parent page from `index.md` to `_index.md`.

---

**Example** Check your file system and confirm that `content/about/index.md` and `content/projects/index.md` both exist. Navigate to `http://localhost:1313/projects/` and note that it shows only static content without any listing functionality.

---

**Exercise** Note the difference: the about page is complete as-is with `index.md`, while the projects page will need to list multiple projects, so it will be converted to use `_index.md`.

**Solution:**
The about page remains as `content/about/index.md` because it's a single cohesive page. The projects page will be renamed to `content/projects/_index.md` to enable listing functionality.

---

### Converting projects to a list page

To convert a regular page to a list page, rename `index.md` to `_index.md`. Hugo will then treat it as a list page that can display child pages.

---

**Example** In your file system, rename `content/projects/index.md` to `content/projects/_index.md`, then reload `http://localhost:1313/projects/` in your browser. The page still displays but is now ready to list child pages.

---

### Adding individual project pages

Individual project pages are created as regular markdown files inside the projects directory. When the parent uses `_index.md`, the theme automatically lists all child pages.

---

**Example** Create a file `content/projects/tess-pipeline.md` with the following content:

```markdown
---
title: "TESS Data Pipeline"
draft: false
---

I built pipelines to download, process, and analyze TESS data. The pipeline includes automated quality control, error correction, and period analysis.
```

---

**Exercise** Navigate to `http://localhost:1313/projects/tess-pipeline/` and verify the page loads with the project content.

**Solution:**
Navigate to `http://localhost:1313/projects/tess-pipeline/`. The page should display with the TESS Data Pipeline content.

---

**Exercise** Navigate to `http://localhost:1313/projects/` and verify it now displays a list with a link to the TESS pipeline project.

**Solution:**
Navigate to `http://localhost:1313/projects/`. The page should now show the projects overview text plus an automatically generated list with a link to "TESS Data Pipeline".

---

**Exercise** Create `content/projects/light-curve-tool.md` with the following content, save, then reload `http://localhost:1313/projects/` and verify both projects appear in the list automatically:

```markdown
---
title: "Light Curve Analysis Tool"
draft: false
---

Tools to merge and analyze multi-sector photometric data from space missions. The tools handle large datasets and identify periodic signals.
```

**Solution:**
Create the file with the content shown and save. Reload `http://localhost:1313/projects/`. The list should now show both "TESS Data Pipeline" and "Light Curve Analysis Tool".

---

**Exercise** Click on each project link in the list to verify it navigates to the individual project page.

**Solution:**
Click "TESS Data Pipeline" - should navigate to `/projects/tess-pipeline/`
Click "Light Curve Analysis Tool" - should navigate to `/projects/light-curve-tool/`

---

**Exercise** Add a third project page of your own with a different title and content, save, reload `/projects/`, and verify it appears in the projects list automatically.

**Solution:**
Create `content/projects/data-visualization.md`:
```markdown
---
title: "Interactive Data Visualization Dashboard"
draft: false
---

Built an interactive dashboard for real-time data visualization using D3.js and Python.
```
Save and reload `http://localhost:1313/projects/`. The list should now show all three projects.

---

### Converting publications to a list page

The publications page can follow the same pattern. Convert it to a list page and add individual publication pages.

---

**Example** Rename `content/publications/index.md` to `content/publications/_index.md`, then create `content/publications/paper-one.md` with the following content:

```markdown
---
title: "Machine Learning for Climate Prediction"
draft: false
---

This paper explores machine learning applications in climate prediction. Published in Nature Climate Change, 2024.
```

---

**Exercise** Navigate to `http://localhost:1313/publications/paper-one/` and verify the publication page loads.

**Solution:**
Navigate to `http://localhost:1313/publications/paper-one/`. The page should display with the publication content.

---

**Exercise** Create `content/publications/paper-two.md` with the following content, save, then navigate to `http://localhost:1313/publications/` and verify both papers appear in the list automatically:

```markdown
---
title: "Neural Networks in Genomics"
draft: false
---

This paper presents novel approaches to analyzing large astronomical datasets. Published in Cell, 2023.
```

**Solution:**
Create the file with the content shown and save. Navigate to `http://localhost:1313/publications/`. The list should show both "Machine Learning for Climate Prediction" and "Neural Networks in Genomics".

---

**Exercise** Click on each publication link to verify they navigate to the individual publication pages.

**Solution:**
Click "Machine Learning for Climate Prediction" - should navigate to `/publications/paper-one/`
Click "Neural Networks in Genomics" - should navigate to `/publications/paper-two/`

---

### When to use each type

Use `index.md` (without underscore) when:
- The page contains one cohesive piece of content
- The page does not need to display child pages
- Example: About page with biography and skills

Use `_index.md` (with underscore) when:
- The page needs to list multiple child pages
- Individual items in that section need their own pages
- Example: Projects section with multiple project pages, Publications section with multiple paper pages

---