# A Multi-Page Portfolio

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

### Creating the site and installing the theme

Create a new site called `multi-page-portfolio`, install the Beautiful Hugo theme, and configure basic settings.

**Exercises**

1. Create a new Hugo site with `hugo new site multi-page-portfolio`.
2. Navigate into the `multi-page-portfolio` directory.
3. Initialize Hugo Modules with `hugo mod init github.com/yourusername/multi-page-portfolio`.
4. Install the Beautiful Hugo theme with `hugo mod get github.com/halogenica/beautifulhugo`.
5. Create a `hugo.toml` file in the site root with the following content:
   ```toml
   [module]
   [[module.imports]]
   path = "github.com/halogenica/beautifulhugo"
   ```

---

### Creating the homepage

The homepage is the landing page at the root URL of the site. For a multi-page portfolio, the homepage contains a brief introduction and directs visitors to other pages through navigation.

**Exercises**

1. Create a file `content/_index.md` with the following content:
   ```markdown
   ---
   title: "My Portfolio"
   draft: false
   ---
   
   # Hello, I'm [Your Name]
   
   I am a Research Software Engineer working with neuroscientists in the NRW region. My background is in Astronomy and Planetary Sciences.
   
   Explore my work using the navigation above.
   ```
2. Start the server with `hugo server -D` and navigate to `http://localhost:1313/`.
3. Verify the homepage displays with the welcome message.

---

## Section 1: Creating Multiple Pages

Hugo generates a separate page for each directory that contains an `index.md` file. These directories are called page bundles. The directory name determines the page URL, and the `index.md` file provides the content.

### Creating a page bundle

A page bundle is a directory containing an `index.md` file. Hugo reads the `index.md` file and creates a web page at a URL matching the directory name. For example, a directory `content/about/` containing `index.md` becomes a page at `/about/`.

The `index.md` file needs front matter to tell Hugo how to handle the page. Below the front matter, content is written in Markdown.

**Exercises**

1. Create a directory `content/about/`.
2. Create a file `content/about/index.md` with content about yourself like:
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
3. Navigate to `http://localhost:1313/about/` in a browser.
4. Verify the page displays with the content.
5. Change some of the text in the skills section. Save and verify the change appears in the browser.

---

### Adding more pages

Each bundle directory with `index.md` creates an independent page. 

**Exercises**

1. Create directory `content/projects/` with an `index.md` file containing:
   ```markdown
   ---
   title: "Projects"
   draft: false
   ---
   
   # My Projects
   
   I have worked on several research projects involving data analysis and software development. Below are some of my key projects.
   ```
2. Navigate to `http://localhost:1313/projects/` and verify the new page appears.
3. Create directory `content/publications/` with an `index.md` file containing:
   ```markdown
   ---
   title: "Publications"
   draft: false
   ---
   
   # Publications
   
   My research has resulted in several publications in peer-reviewed journals. These papers cover topics in astronomy, planetary science, and observational techniques.
   ```
4. Navigate to `/publications/` and verify this third page exists.

---

### Understanding bundle front matter

Front matter controls how Hugo handles each page. The `draft` setting determines whether the page appears when building the site. The `title` appears in the browser tab and can be used by the theme.

**Exercises**

1. In `projects/index.md`, change `draft: false` to `draft: true`.
2. Stop the server with `Ctrl+C` and restart it with `hugo server` (without the `-D` flag).
3. Navigate to `/projects/` and verify the page returns a 404 error.
4. Change `draft: true` back to `draft: false` and restart the server.
5. Navigate to `/projects/` again and verify the page now loads.

---

## Section 2: Connecting Pages with Navigation

Menu entries link pages together through navigation. Menu configuration in `hugo.toml` defines which pages appear in the navigation and in what order. Menus appear on all pages and allow navigation between different sections.

### Adding a menu entry

Menu entries are defined in the `hugo.toml` configuration file. Each entry has a name (the text that appears), a URL (where it links to), and a weight (for ordering). Hugo displays menu entries in the navigation once configured.

**Exercises**

1. Open `hugo.toml` and add the following above the `[module]` section:
   ```toml
   [[menu.main]]
   name = "About"
   url = "/about/"
   weight = 1
   ```
2. Save the file and reload any page in a browser.
3. Verify an "About" link appears in the navigation.
4. Click the "About" link and verify it navigates to `/about/`.

---

### Adding multiple menu entries

Multiple menu entries create multiple navigation links. Each `[[menu.main]]` block defines one menu item. Hugo displays all menu entries together in the navigation.

**Exercises**

1. Add two more menu entries below the first one in `hugo.toml`:
   ```toml
   [[menu.main]]
   name = "Projects"
   url = "/projects/"
   weight = 2
   
   [[menu.main]]
   name = "Publications"
   url = "/publications/"
   weight = 3
   ```
2. Save and reload any page. Verify three links now appear in navigation.

---

### Controlling menu order with weight

The weight value determines where each menu item appears. Lower weight values appear first in the menu. When weights are equal, Hugo typically orders items alphabetically.

**Exercises**

1. In `hugo.toml`, change the "Publications" weight from 3 to 1.
2. Save and reload. Verify "Publications" now appears first in the menu.
3. Change "About" weight to 3. Reload and verify the menu order changed.
4. Restore a logical weight order (About=1, Projects=2, Publications=3) and verify the menu displays in the preferred order.

---

### Adding page links in homepage

The homepage can contain direct links to main sections. These links provide an alternative navigation method alongside the menu and can include descriptions of each section.

**Exercises**

1. Open `content/_index.md` and add new content after the existing content:
   ```markdown
   
   ## Explore My Work
   
   - [About Me](/about/) - Learn about my background and skills
   - [Projects](/projects/) - View my research projects
   - [Publications](/publications/) - Read my publications
   ```
2. Save and reload the homepage. Verify the links appear below the introduction.
3. Click each link and verify they navigate to the correct pages.
4. Change the description text for one of the links. Reload and verify the change appears.

---

## Section 3: Creating List Pages for Multiple Items

Some portfolio sections contain multiple items. The projects page might list several projects. The publications page might list several papers. Hugo provides a way to automatically display these items.

Hugo handles two types of pages differently. A regular page bundle uses `index.md` and displays a single page. A list page uses `_index.md` (with underscore) and can automatically display child pages within that section.

### Understanding index.md vs _index.md

The filename determines how Hugo treats a directory:

- `index.md` (without underscore) creates a single page bundle. The about page uses this because it displays one cohesive piece of content.
- `_index.md` (with underscore) creates a list page. List pages can have child pages, and themes typically display links to all child pages automatically.

When you need a section to contain multiple individual pages (like multiple projects or multiple publications), you convert the parent page from `index.md` to `_index.md`.

**Exercises**

1. Verify the current files: `content/about/` uses `index.md`, and `content/projects/` currently uses `index.md`.
2. Navigate to `http://localhost:1313/projects/` and note that it shows only the overview content.
3. The projects page will be converted to a list page to accommodate individual project pages.

---

### Converting projects to a list page

To convert a regular page to a list page, rename `index.md` to `_index.md`. Hugo will then treat it as a list page that can display child pages.

**Exercises**

1. In your file system, rename `content/projects/index.md` to `content/projects/_index.md`.

---

### Adding individual project pages

Individual project pages are created as regular markdown files inside the projects directory. When the parent uses `_index.md`, the theme automatically lists all child pages.

**Exercises**

1. Create a file `content/projects/tess-pipeline.md` with:
   ```markdown
   ---
   title: "TESS Data Pipeline"
   draft: false
   ---
   
   I built pipelines to download, process, and analyze TESS data. The pipeline includes automated quality control, error correction, and period analysis.
   ```
2. Navigate to `http://localhost:1313/projects/tess-pipeline/` and verify the page loads.
3. Navigate to `http://localhost:1313/projects/` and verify it now displays a list with a link to the TESS pipeline project.
4. Create `content/projects/light-curve-tool.md` with:
   ```markdown
   ---
   title: "Light Curve Analysis Tool"
   draft: false
   ---
   
   Tools to merge and analyze multi-sector photometric data from space missions. The tools handle large datasets and identify periodic signals.
   ```
5. Reload `/projects/` and verify both projects appear in the list automatically.
6. Click on each project link to verify it navigates to the individual project page.

---

### Converting publications to a list page

The publications page can follow the same pattern. Convert it to a list page and add individual publication pages.

**Exercises**

1. Rename `content/publications/index.md` to `content/publications/_index.md`.
2. Create `content/publications/paper-one.md` with:
   ```markdown
   ---
   title: "Machine Learning for Climate Prediction"
   draft: false
   ---
   
   This paper explores machine learning applications in climate prediction. Published in Nature Climate Change, 2024.
   ```
3. Create `content/publications/paper-two.md` with:
   ```markdown
   ---
   title: "Neural Networks in Genomics"
   draft: false
   ---
   
   This paper presents novel approaches to analyzing large astronomical datasets. Published in Cell, 2023.
   ```
4. Navigate to `/publications/` and verify both papers appear in the list automatically.

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

## Section 4: Adding Resources to Bundles

Files placed in a bundle directory alongside `index.md` become page resources. These resources are referenced using relative paths. Hugo serves resources from the bundle directory when that page loads.

Hugo offers two ways to store files. The `static` directory stores files accessible from any page using absolute paths like `/images/photo.jpg`. Bundle resources store files within each page directory using relative paths like `photo.jpg`. Bundle resources are stored with the pages that reference them.

### Adding images to bundles

Image files placed in the bundle directory can be referenced using relative paths in Markdown. A relative path is just the filename without any leading slash. Hugo looks for the file in the same directory as the `index.md` that references it.

**Exercises**

1. Add an image file `research-photo.jpg` to the `content/about/` directory.
2. In `about/index.md`, below the skills section, add:
   ```markdown
   
   ![Working with telescope data](research-photo.jpg)
   ```
3. Navigate to `/about/` and verify the image displays on the page.
4. Add a second image file `lab-photo.jpg` to `content/about/`.
5. In `about/index.md`, add another image reference below the first one using just the filename `lab-photo.jpg`.
6. Navigate to `/about/` and verify both images display.

---

### Adding PDF documents to bundles

PDF files in bundle directories work like images. Link to them using relative paths, and Hugo serves the PDF when someone clicks the link.

**Exercises**

1. Add a file `cv.pdf` to the `content/about/` directory.
2. In `about/index.md`, add at the end:
   ```markdown
   
   [Download CV](cv.pdf)
   ```
3. Navigate to `/about/` and click the link. Verify the PDF opens or downloads.
4. Add another PDF file `research-statement.pdf` to the same directory.
5. Add a second link below the first one: `[Download Research Statement](research-statement.pdf)`.
6. Navigate to `/about/` and verify both PDF links work correctly.

---

### Understanding resource isolation

Resources in one bundle cannot be accessed from other bundles. Each bundle's resources remain independent. This isolation prevents conflicts when different bundles have files with the same name.

**Exercises**

1. Try adding a link `[Download CV](cv.pdf)` to `content/projects/_index.md` (without adding any PDF file to the projects directory).
2. Navigate to `/projects/` and click the link. Verify it fails because the resource does not exist in that bundle.
3. Remove the broken link from `projects/_index.md`.
4. Verify that the CV link still works correctly on the `/about/` page.
5. Add an image file named `photo.jpg` to both `content/about/` and `content/projects/` directories. Reference both using `photo.jpg` in their respective `index.md` or `_index.md` files. Verify that each page displays its own version of the file without conflict.

---