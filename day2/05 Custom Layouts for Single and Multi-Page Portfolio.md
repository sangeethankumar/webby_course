# Custom Layouts for Portfolio Sites

Hugo uses layouts to transform Markdown content into HTML pages. The Beautiful Hugo theme provides layouts for all page types. When layout files are added to the `layouts/` directory in the site root, Hugo uses those layouts instead of the theme's layouts. This gives control over HTML structure without modifying theme files.

Hugo follows a specific lookup order when searching for layouts. It checks the site's `layouts/` directory first, then falls back to the theme's `layouts/` directory. Creating a layout file in the site's `layouts/` directory causes Hugo to use that file instead of the theme's version.

Here we will see:

- how to access and display template variables
- how to create default layouts for all pages
- how to create section-specific layouts

---

## Section 1: Template Variables and Homepage Layout

Template variables provide access to content and configuration values. Site-level variables come from `hugo.toml` and are accessed with `.Site`. Page-level variables come from front matter and Markdown content, accessed directly with `.Title`, `.Content`, or through `.Params` for custom fields.

### Site variables from configuration

Values defined in `hugo.toml` become accessible in layouts through the `.Site` object. The site title is accessed with `{{ .Site.Title }}`. Custom parameters defined under `[params]` are accessed with `{{ .Site.Params.fieldname }}`.

**Exercises**

1. Add a custom parameter to `hugo.toml`:
   ```toml
   [params]
   tagline = "Research and Projects"
   ```
2. Create `layouts/index.html` with:
   ```html
   <html>
   <body>
     <h1>{{ .Site.Title }}</h1>
     <p>{{ .Site.Params.tagline }}</p>
   </body>
   </html>
   ```
3. Start the server with `hugo server -D` and navigate to `http://localhost:1313/`.
4. Change the tagline in `hugo.toml` to something different. Reload and verify the new tagline appears.

---

### Page variables from front matter

Page-level variables come from the front matter and content of Markdown files. The `{{ .Title }}` variable displays the title from front matter. The `{{ .Content }}` variable renders the Markdown content as HTML. Custom front matter fields are accessed through `{{ .Params.fieldname }}`.

**Exercises**

1. Add content below the front matter of `content/_index.md` if it does not exist:
   ```markdown
   ## About
   
   Brief introduction about the portfolio.
   ```
2. Add a custom field to the front matter:
   ```yaml
   title: "Home"
   subtitle: "Machine Learning Research"
   ```
3. Update `layouts/index.html` to display page variables:
   ```html
   <html>

   <body>
     <h1>{{ .Site.Title }}</h1>
     <p>{{ .Site.Params.tagline }}</p>
     <h2>{{ .Params.subtitle }}</h2>
     {{ .Content }}
   </body>

   </html>
   ```
4. Reload `http://localhost:1313/` and verify the subtitle and markdown content display.
5. Change the subtitle in `_index.md` to something different. Reload and verify the change appears.
6. Add another paragraph to the content in `_index.md`. Reload and verify it renders.

---

### Complete homepage layout

Combining site and page variables creates a complete homepage layout. Multiple sections can be added by structuring the content in `_index.md` with markdown headings.

**Exercises**

1. Update `content/_index.md` with multiple sections:
   ```markdown
   ---
   title: "Home"
   subtitle: "Machine Learning Research"
   ---
   
   ## About
   
   Research focused on machine learning and data science.
   
   ## Current Work
   
   Working on neural network optimization and computer vision projects.
   
   ## Contact
   
   Email: contact@example.com
   ```
2. Update `layouts/index.html` to add footer:
   ```html
   <html>

   <body>
     <header>
       <h1>{{ .Site.Title }}</h1>
       <p>{{ .Site.Params.tagline }}</p>
     </header>
     <main>
       <h2>{{ .Params.subtitle }}</h2>
       {{ .Content }}
     </main>
     <footer>
       <p>&copy; 2024 {{ .Site.Title }}</p>
     </footer>
   </body>
   </html>
   ```
3. Reload and verify the page shows header, main content with all sections, and footer.
4. Delete `layouts/index.html`. Reload and verify the homepage returns to Beautiful Hugo theme styling.
5. Recreate `layouts/index.html` with the same content. Reload and verify the custom layout returns.

---

## Section 2: Default Layouts

Default layouts apply to all pages of a specific type. The file `layouts/_default/single.html` controls all individual content pages. The file `layouts/_default/list.html` controls all section listing pages. These layouts use the same template variables as the homepage but apply to different page types.

A single page is an individual piece of content like `content/about/index.md` or `content/projects/project-one.md`. A list page is a section index that can display child pages, like `content/projects/_index.md` when it contains other markdown files.

### Single page layout

The file `layouts/_default/single.html` applies to all individual content pages that are not the homepage. This includes pages like About and individual project or publication pages. Template variables access the page's title, date, and content.

**Exercises**

1. Create `layouts/_default/` directory.
2. Verify the site has `content/about/index.md` (create it with title and content if needed).
3. Create `layouts/_default/single.html` with:
   ```html
   <html>
   <body>
     <h1>{{ .Title }}</h1>
     {{ .Content }}
   </body>
   </html>
   ```
4. Navigate to `http://localhost:1313/about/`.
5. Verify the page displays with the custom HTML instead of Beautiful Hugo theme styling.
6. Check the browser tab title. Verify it shows "About - My Portfolio" (combining page title and site title).
7. Navigate to the homepage. Verify it still uses `layouts/index.html` (it should not be affected by this change).

---

### Displaying page metadata

The `.Date` variable accesses the date from page front matter. The `.Format` function converts the date into a readable format.

**Exercises**

1. Add metadata to `content/about/index.md` front matter:
   ```yaml
   title: "About"
   date: 2024-01-15
   description: "Background and skills"
   ```
2. Update `layouts/_default/single.html` to display metadata:
   ```html
   <html>

   <body>
     <h1>{{ .Title }}</h1>
     <p>{{ .Params.description }}</p>
     <p>Last updated: {{ .Date.Format "January 2, 2006" }}</p>
     {{ .Content }}
   </body>

   </html>
   ```
3. Reload `http://localhost:1313/about/`.
4. Verify the description and formatted date display above the content.
5. Change the date to a different value. Reload and verify the new date appears.

---

### List page layout with child pages

The file `layouts/_default/list.html` applies to section index pages. When a directory contains `_index.md` and other markdown files, that section uses the list layout. The `{{ range .Pages }}` syntax loops through all child pages in that section.

Inside the range loop, template variables like `{{ .Title }}` and `{{ .RelPermalink }}` refer to each child page. The `.RelPermalink` variable provides the URL to that page.

**Exercises**

1. Verify the site has `content/projects/_index.md` and at least two project files (like `content/projects/project-one.md` and `content/projects/project-two.md`).
2. Create `layouts/_default/list.html` with:
   ```html
   <html>

   <body>

     <h1>{{ .Title }}</h1>
     {{ .Content }}

     <ul>
     {{ range .Pages }}
       <li><a href="{{ .RelPermalink }}">{{ .Title }}</a></li>
     {{ end }}
     </ul>

   </body>
   </html>
   ```
3. Navigate to `http://localhost:1313/projects/`.
4. Verify the page shows the content from `projects/_index.md` followed by a list of links.
5. Verify each link displays the project title from its front matter.
6. Click one of the links. Verify it navigates to that project page (which uses the single layout).

---

### Displaying child page metadata

Inside the `{{ range .Pages }}` loop, each page's front matter is accessible through `.Params`. 

**Exercises**

1. Add a year field to the front matter in the project files:
   ```yaml
   title: "Project One"
   year: 2024
   ```
2. Update `layouts/_default/list.html` to display the year:
   ```html
   <html>

   <body>
     <h1>{{ .Title }}</h1>
     {{ .Content }}
     <ul>
     {{ range .Pages }}
       <li>
         <a href="{{ .RelPermalink }}">{{ .Title }}</a>
         ({{ .Params.year }})
       </li>
     {{ end }}
     </ul>
   </body>
   </html>
   ```
3. Reload `http://localhost:1313/projects/`.
4. Verify each project link now displays its year from front matter.
---

## Section 3: Section-Specific Layouts

Section-specific layouts override default layouts for specific directories. Creating `layouts/about/single.html` applies only to the about page. Creating `layouts/projects/single.html` applies only to pages in the projects directory. Hugo checks for section-specific layouts before falling back to default layouts.

### About page custom layout

The file `layouts/about/single.html` applies only to `content/about/index.md`. This allows a different structure for the about page without affecting other single pages.

**Exercises**

1. Create `layouts/about/` directory.
2. Create `layouts/about/single.html` with:
   ```html
   <html>

   <body>
     <h1>About {{ .Site.Params.name }}</h1>
     {{ .Content }}
     <p><a href="/">Back to Home</a></p>
   </body>

   </html>
   ```
3. Navigate to `http://localhost:1313/about/`.
4. Verify the "Back to Home" link appears at the bottom.

---

### Projects list layout

The file `layouts/projects/list.html` applies only to `content/projects/_index.md`. This allows the projects listing page to have a different structure than other list pages.

**Exercises**

1. Create `layouts/projects/` directory if it does not exist.
2. Create `layouts/projects/list.html` with:
   ```html
   <html>

   <body>
     <h1>Research Projects</h1>
     {{ .Content }}

     <ul>
     {{ range .Pages }}
       <li>
         <strong><a href="{{ .RelPermalink }}">{{ .Title }}</a></strong>
         <span> ({{ .Params.year }})</span>
       </li>
     {{ end }}
     </ul>

   </body>
   </html>
   ```
3. Navigate to `http://localhost:1313/projects/`.
5. Verify the project list appears under "Project List" subheading and is bold.

---

### Individual project layout

The file `layouts/projects/single.html` applies to individual project pages in the projects directory. 

**Exercises**

1. Add custom front matter to a project file:
   ```yaml
   title: "Project One"
   year: 2024
   status: "Active"
   github: "https://github.com/username/project"
   ```
2. Create `layouts/projects/single.html` with:
   ```html
   <html>

   <body>
     <h1>{{ .Title }}</h1>
     <p>Year: {{ .Params.year }} | Status: {{ .Params.status }}</p>
     {{ if .Params.github }}
     <p><a href="{{ .Params.github }}">View on GitHub</a></p>
     {{ end }}
     {{ .Content }}
     <p><a href="/projects/">Back to Projects</a></p>
   </body>

   </html>
   ```
3. Navigate to a single project page.
4. Verify it displays the year, status, and GitHub link from front matter.
5. Navigate to `http://localhost:1313/about/`. Verify it still uses `layouts/about/single.html` without year or status fields.

---
