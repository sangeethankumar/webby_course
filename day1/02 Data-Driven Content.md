# Enhancing Your Portfolio with Media and Data

Hugo portfolios can display images, embed media, and manage structured content efficiently. Images are stored in the static directory and referenced in Markdown. Shortcodes provide patterns for displaying rich media like videos and code snippets. Data files separate content from presentation, allowing information to be maintained in one place and displayed automatically.

This document teaches how to enhance a Hugo portfolio with visual and structured content.

Here we will see:

- how to add and organize images
- how to use shortcodes for rich media
- how to manage structured content with data files

---

## Section 1: Adding Images

Hugo serves images from the static directory. Files placed in static are copied to the website without modification. These files are referenced using paths that start from the site root.

This section introduces basic image display and establishes the static directory as the location for site assets.

### Adding your first image

The static directory holds files that Hugo copies directly to the website. When placing an image in `static/images/profile.jpg`, it is referenced in Markdown as `/images/profile.jpg`. The leading slash tells Hugo to look from the site root.

Markdown image syntax uses square brackets for alt text and parentheses for the file path.

**Exercises**

1. Create a `static/images/` directory in the site root.
2. Add a profile photo to `static/images/profile.jpg`.
3. In the introduction section of `content/_index.md`, add:
   ```markdown
   ![Profile Photo](/images/profile.jpg)
   ```
4. Save and verify the image displays in the browser.
5. Replace `profile.jpg` with a different image (keeping the same filename). Reload and verify the new image appears without changing the Markdown.

---

### Understanding image paths

Hugo serves files from static using absolute paths. A path starting with `/` tells the browser to look from the site root. This means `/images/profile.jpg` always points to `static/images/profile.jpg` regardless of where the Markdown file is located.

**Exercises**

1. Add a second image `research.jpg` to `static/images/`.
2. In the `## Projects` section, add:
   ```markdown
   ![Research Project](/images/research.jpg)
   ```
3. Verify both images display correctly.
4. Try changing the alt text of one image. Reload and verify the change.
5. Add a third image to the same directory and reference it in the `## About Me` section.

---

### Alt text for accessibility

Alt text describes an image for people who cannot see it. Screen readers announce alt text to visually impaired users. Alt text also displays when an image fails to load.

Good alt text describes the image content concisely without saying "image of" or "picture of". It should convey the same information the image provides.

**Exercises**

1. Review the alt text for the profile image. Change it from "Profile Photo" to a descriptive phrase like "Dr. Smith in the laboratory".
2. Update the alt text for the research image to describe what the image shows.
3. Add a new image with descriptive alt text that explains its content.
4. Right-click on one of the images and select "Inspect" to see the HTML `<img>` tag and verify the alt text appears in the `alt` attribute.
5. Change one image filename in the Markdown to a non-existent file (like `/images/missing.jpg`). Reload the page and notice the alt text displays in place of the broken image. Change it back to the correct filename.

---

## Section 2: Organizing Static Resources

The static directory can hold any file type the portfolio needs. Subdirectories within static organize different resource types. Hugo preserves this directory structure when serving files.

This section covers organizing various file types and establishing patterns for resource management.

### Creating subdirectories for different resource types

Subdirectories keep related files together. Images go in one directory, documents in another. This organization makes files easier to find and maintain.

Hugo serves files based on their location in static. A file at `static/documents/cv.pdf` becomes available at `/documents/cv.pdf` on the website.

**Exercises**

1. Create a `static/documents/` directory.
2. Add a CV PDF as `static/documents/cv.pdf`.
3. In the `## Contact` section, add:
   ```markdown
   [Download CV](/documents/cv.pdf)
   ```
4. Save and click the link to verify the PDF opens.
5. Add a second PDF document `research-statement.pdf` to the same directory and link to it from the `## About Me` section.

---

### Adding different file types

Hugo serves any file type from static without processing. Research portfolios often need PDFs for papers, BibTeX files for citations, CSV files for data, and various image formats.

**Exercises**

1. Add a BibTeX file as `static/documents/publications.bib`.
2. In the `## Publications` section, add:
   ```markdown
   [Download BibTeX](/documents/publications.bib)
   ```
3. Save and verify clicking the link downloads the file.
4. Add a CSV data file as `static/data/results.csv` and link to it from the `## Projects` section.
5. Verify the CSV link downloads correctly.

---

### Using SVG images

SVG images are vector graphics that scale without losing quality. They work well for diagrams, charts, and logos. Hugo serves SVG files the same way it serves other images.

**Exercises**

1. Add an SVG diagram to `static/images/diagram.svg`.
2. Reference it in the `## Projects` section with:
   ```markdown
   ![System Diagram](/images/diagram.svg)
   ```
3. Save and verify the SVG displays correctly.
4. Resize the browser window and notice the SVG scales smoothly.
5. Add a second SVG image and reference it in a different section.

---

## Section 3: Built-in Hugo Shortcodes

Hugo provides built-in shortcodes for common content patterns. Shortcodes generate HTML from simple parameters without requiring HTML to be written. They work directly in Markdown files.

This section introduces three useful shortcodes for research portfolios.

### Using the figure shortcode for images with captions

The figure shortcode creates images with captions, alt text, and sizing attributes. It generates semantic HTML that displays images professionally.

The shortcode uses named parameters like `src`, `alt`, `caption`, and `width`. These are placed inside `{{< >}}` markers.

**Note:*- Some themes may not support the width parameter. If the image size does not change when width is specified, this is theme-dependent behavior.

**Exercises**

1. Replace the profile image Markdown with:
   ```markdown
   {{< figure src="/images/profile.jpg" alt="Profile photo" caption="Dr. [Your Name]" width="300px" >}}
   ```
2. Save and reload. Verify the image now displays with a caption below it.
3. Change the caption text to something different. Reload and verify the new caption appears.
4. Remove the caption parameter entirely. Reload and verify the image displays without a caption.
5. Add a second figure with caption in the `## Projects` section using a different image.

---

### Using the youtube shortcode for embedded videos

The youtube shortcode embeds YouTube videos using their video ID. The video ID is the string after `v=` in a YouTube URL. Hugo generates the iframe HTML needed for embedding.

**Exercises**

1. Find a research presentation on YouTube.
2. Copy the video ID from the URL (the part after `v=`).
3. In the `## Projects` section, add:
   ```markdown
   {{< youtube VIDEO_ID >}}
   ```
4. Replace `VIDEO_ID` with the actual ID copied.
5. Save and verify the video embeds and plays.
6. Add a second YouTube video about a different project. Verify both videos display.

---

### Using the gist shortcode for code snippets

The gist shortcode embeds GitHub Gists using the username and gist ID. Gists display code with syntax highlighting. Hugo generates the script tags required for embedding.

A GitHub Gist is a simple way to share code snippets. Unlike a full repository, a Gist is just one or more files containing code or text. Each Gist has a unique ID that appears in its URL.

To create a Gist, go to gist.github.com while logged into GitHub. Paste code, give it a filename (the extension determines syntax highlighting), and click "Create public gist". GitHub generates a URL like `gist.github.com/username/abc123def456`. The part after the username (abc123def456) is the gist ID.

**Exercises**

1. Create a GitHub Gist with sample code from research at gist.github.com.
2. Copy the username and the gist ID from the URL.
3. In the `## Projects` section, add:
   ```markdown
   {{< gist USERNAME GIST_ID >}}
   ```
4. Replace `USERNAME` and `GIST_ID` with actual values.
5. Save and verify the code snippet displays with syntax highlighting.
6. Edit the Gist on GitHub to add a comment. Reload the portfolio and verify the updated content appears.

---

## Section 4: Data Files and Simple Access

Hugo reads structured data from files in the data directory. Data files use YAML format to store information. Shortcodes can access individual values, nested objects, and lists from these files.

Data files separate content from presentation. When a data file changes, the shortcode displays the updated content automatically. Information is maintained in one place.

### Creating all data files

Data files store structured information in YAML format. YAML uses colons to separate keys from values, indentation to define nested structure, and hyphens to denote list items. Each key-value pair sits on its own line.

Hugo reads all files from the data directory and makes them available to shortcodes through the `.Site.Data` variable. The filename determines the data key used to access the content.

**Exercises**

1. Create a `data/` directory in the site root.
2. Create `data/contact.yaml` with simple values and nested objects:
   ```yaml
   name: "Your Name"
   email: "you@example.com"
   social:
     github: "username"
   ```
3. Create `data/skills.yaml` with a list:
   ```yaml
   languages:
     - Python
     - R
     - JavaScript
   ```
4. Create `data/projects.yaml` with a list of objects:
   ```yaml
   - title: "Data Pipeline"
     year: 2024
     github: "https://github.com/username/pipeline"
   
   - title: "Dashboard"
     year: 2023
     demo: "https://demo.example.com"
   ```
5. Create `data/publications.yaml` with a list of objects with optional fields:
   ```yaml
   - title: "Machine Learning Paper"
     year: 2024
     link: "https://doi.org/10.1038/example"
   
   - title: "Data Science Paper"
     year: 2023
     link: "https://doi.org/10.1016/example"
     pdf: "/documents/paper.pdf"
   ```
6. Save all files and verify they open correctly.

---

### Creating a shortcode that accesses single values

Shortcodes are HTML templates stored in `layouts/shortcodes/`. They use double curly braces with dot notation to access data values.

The syntax `{{ .Site.Data.contact.name }}` tells Hugo to look in the data directory for a file named `contact.yaml` and retrieve the value of the `name` field.

**Exercises**

1. Create a `layouts/shortcodes/` directory in the site root.
2. Create `layouts/shortcodes/contact-info.html` with:
   ```html
   <p>{{ .Site.Data.contact.name }}<br>
   {{ .Site.Data.contact.email }}</p>
   ```
3. In the `## Contact` section in `content/_index.md`, add:
   ```markdown
   {{< contact-info >}}
   ```
4. Save and reload. Verify both values display.
5. Change the email in `contact.yaml`. Reload and verify the change appears automatically.

---

### Accessing nested objects

Hugo accesses nested values by chaining dot notation. The syntax `{{ .Site.Data.contact.social.github }}` navigates from the file to the parent key to the child key.

**Exercises**

1. Update `layouts/shortcodes/contact-info.html` to access the nested social field:
   ```html
   <p>{{ .Site.Data.contact.name }}<br>
   {{ .Site.Data.contact.email }}<br>
   GitHub: {{ .Site.Data.contact.social.github }}</p>
   ```
2. Save and reload. Verify the GitHub username displays.
3. Change the GitHub username in `contact.yaml`. Reload and verify the change appears automatically.

---

### Iterating over simple lists

The `range` function loops over list items, executing template code for each item. For each item in the list, Hugo executes the template code between `{{ range }}` and `{{ end }}`. The dot represents the current item.

**Exercises**

1. Create `layouts/shortcodes/skills.html` with:
   ```html
   <ul>
   {{ range .Site.Data.skills.languages }}
   <li>{{ . }}</li>
   {{ end }}
   </ul>
   ```
2. In the `## Skills` section, add `{{< skills >}}`.
3. Save and reload. Verify all programming languages display as a bulleted list.
4. Add another programming language to `skills.yaml`. Reload and verify it appears in the list.

---

## Section 5: Conditionals

Hugo template syntax supports conditional statements to check whether fields exist before displaying them. The `if` statement prevents errors when optional fields are missing from some items.

Conditionals make data structures flexible. Items can have different fields without breaking the template.

### Conditionally displaying optional fields

The `if` statement checks whether a field exists before displaying it. The syntax `{{ if .fieldname }}` checks if the current item has that field. If it exists, Hugo executes the code until `{{ end }}`.

**Exercises**

1. Add an optional `website` field to `data/contact.yaml`:
   ```yaml
   name: "Your Name"
   email: "you@example.com"
   website: "https://example.com"
   social:
     github: "username"
   ```
2. Update `layouts/shortcodes/contact-info.html` to conditionally display website:
   ```html
   <p>{{ .Site.Data.contact.name }}<br>
   {{ .Site.Data.contact.email }}<br>
   {{ if .Site.Data.contact.website }}{{ .Site.Data.contact.website }}<br>{{ end }}
   GitHub: {{ .Site.Data.contact.social.github }}</p>
   ```
3. Save and reload. Verify the website displays.
4. Remove the `website` field from `contact.yaml`. Reload and verify the page still works without showing the website line.

---

### Using conditionals with structured lists

The publications data file created in Section 4 has an optional `pdf` field. Conditionals check each item individually to determine which fields to display.

**Exercises**

1. Create `layouts/shortcodes/publications.html` with:
   ```html
   {{ range .Site.Data.publications }}
   <p><strong>{{ .title }}</strong> ({{ .year }})<br>
   <a href="{{ .link }}">Link</a>
   {{ if .pdf }} | <a href="{{ .pdf }}">PDF</a>{{ end }}</p>
   {{ end }}
   ```
2. In the `## Publications` section, add `{{< publications >}}`.
3. Save and reload. Verify both publications display, with the second showing a PDF link.

---

### Creating projects with multiple optional fields

The projects data file created in Section 4 has optional `github` and `demo` fields. Projects can have either field, both, or neither.

**Exercises**

1. Create `layouts/shortcodes/projects.html` with:
   ```html
   {{ range .Site.Data.projects }}
   <p><strong>{{ .title }}</strong> ({{ .year }})<br>
   {{ if .github }}<a href="{{ .github }}">GitHub</a>{{ end }}
   {{ if .demo }}{{ if .github }} | {{ end }}<a href="{{ .demo }}">Demo</a>{{ end }}</p>
   {{ end }}
   ```
2. In the `## Projects` section, add `{{< projects >}}`.
3. Save and reload. Verify the first project shows GitHub link and the second shows Demo link.

---

## Optional: Making Data Files Your Single Source of Truth

Now that data-driven shortcodes are managing structured content, the `_index.md` file can be cleaned up by removing manual text. This makes YAML files the single source of truth.

The `_index.md` sections would contain only shortcodes:

```markdown
## Skills

{{< skills >}}

## Publications

{{< publications >}}

## Projects

{{< projects >}}
```

With this approach, all content lives in YAML files. When adding a new publication, updating a project, or changing contact information, the YAML file is edited. The changes appear automatically on the portfolio without touching `_index.md`.

---