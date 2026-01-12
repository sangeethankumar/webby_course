# Template Inheritance and Reusable Components - SOLUTIONS

Hugo allows templates to inherit from a base template, preventing repetition of common HTML structure across pages. When building multiple pages, the same header, footer, and HTML structure often appears in every layout file. Template inheritance solves this by defining common elements once in a base template. Partials are smaller reusable template pieces that can be included anywhere to avoid repeating code.

Here we will see:

- how base templates eliminate duplicate HTML code
- how blocks allow pages to customize specific sections
- how partials create reusable components

---

## Section 1: Creating a Base Template

Hugo needs layout files to display content. Without a base template, every layout file must include the complete HTML structure. This leads to duplicate code across multiple files. When the same HTML appears in many places, updating becomes difficult and error-prone.

This section covers creating multiple layout files to see the duplication problem, creating a base template file to solve it, and removing duplicate code from individual layouts. By the end of this section, common HTML will exist in one place and all pages will inherit from it.

| File/Concept | Description |
|--------------|-------------|
| `layouts/_default/baseof.html` | Base template that other layouts inherit from |
| `{{ block "name" . }}{{ end }}` | Defines a block that child templates can override |
| `{{ define "name" }}{{ end }}` | Overrides a block from the base template |
| `layouts/index.html` | Layout for the homepage |
| `layouts/about/single.html` | Layout for the about page |

---

### Seeing the duplication problem

When building a site with multiple pages, each page needs its own layout file. Without template inheritance, every layout file must include the complete HTML structure including doctype, head, and body tags. This creates duplication where the same HTML appears in multiple files.

To understand why base templates are useful, the duplication problem must be seen first. This subsection creates two separate layout files with identical HTML structure.

---

**Example** Create a new Hugo site, add content files for homepage and about page, then create layout files with complete HTML structure for each:

```bash
hugo new site inheritance-demo
cd inheritance-demo
hugo new content _index.md
hugo new content about.md
```

Create `layouts/index.html`:

```html
<!DOCTYPE html>
<html>
<head>
    <title>My Portfolio</title>
    <style>
        body { font-family: Arial, sans-serif; margin: 40px; }
        footer { margin-top: 50px; color: gray; }
    </style>
</head>
<body>
    <h1>Welcome to My Portfolio</h1>
    {{ .Content }}
    <footer>
        <p>© 2025 My Portfolio. All rights reserved.</p>
    </footer>
</body>
</html>
```

Create `layouts/about/single.html`:

```html
<!DOCTYPE html>
<html>
<head>
    <title>My Portfolio</title>
    <style>
        body { font-family: Arial, sans-serif; margin: 40px; }
        footer { margin-top: 50px; color: gray; }
    </style>
</head>
<body>
    <h1>About Me</h1>
    {{ .Content }}
    <footer>
        <p>© 2025 My Portfolio. All rights reserved.</p>
    </footer>
</body>
</html>
```

Start the server with `hugo server -D`, navigate to `http://localhost:1313/` for homepage and `http://localhost:1313/about/` for about page.

---

**Exercise** Compare the two layout files and count how many lines of HTML are identical between them.

**Solution:**
Lines 1-8 (DOCTYPE through style closing tag) and lines 11-14 (footer section through closing html tag) are identical - that's 11 out of 15 lines that are duplicated.

---

**Exercise** Change the copyright year in the footer from "2025" to "2026" in `layouts/index.html` only, save, refresh the homepage, then visit the about page and observe the footer still shows "2025".

**Solution:**
```html
<footer>
    <p>© 2026 My Portfolio. All rights reserved.</p>
</footer>
```
Homepage shows "2026" but about page still shows "2025".

---

**Exercise** Update the footer in `layouts/about/single.html` to match the homepage by changing "2025" to "2026", save, refresh the about page, and verify both pages now show "2026".

**Solution:**
```html
<footer>
    <p>© 2026 My Portfolio. All rights reserved.</p>
</footer>
```
Both pages now show "2026".

---

### Creating the base template

A base template contains the HTML structure that all pages share. This file is created at `layouts/_default/baseof.html`. Hugo automatically looks for this file and uses it as the foundation for all other layouts.

The base template includes blocks. A block is a placeholder where child templates can insert their own content. The most important block is the "main" block which holds the page-specific content.

---

**Example** Create `layouts/_default/baseof.html` with the shared HTML structure:

```html
<!DOCTYPE html>
<html>
<head>
    <title>My Portfolio</title>
    <style>
        body { font-family: Arial, sans-serif; margin: 40px; }
        footer { margin-top: 50px; color: gray; }
    </style>
</head>
<body>
    {{ block "main" . }}{{ end }}
    <footer>
        <p>© 2026 My Portfolio. All rights reserved.</p>
    </footer>
</body>
</html>
```

Restart the server with `Ctrl+C` then `hugo server -D`.

---

**Exercise** With the server running, verify that the homepage at `http://localhost:1313/` still displays correctly with the same styling and footer.

**Solution:**
Homepage displays correctly with Arial font, 40px margin, and footer showing "© 2026 My Portfolio. All rights reserved."

---

**Exercise** Visit the about page at `http://localhost:1313/about/` and verify it also displays correctly with the same styling and footer.

**Solution:**
About page displays correctly with the same styling and footer as homepage.

---

**Exercise** Add a comment inside the `<head>` tag in `baseof.html`: `<!-- This is the base template -->`, restart the server, open browser DevTools (F12), examine the page source, and verify the comment appears on both homepage and about page.

**Solution:**
```html
<head>
    <title>My Portfolio</title>
    <!-- This is the base template -->
    <style>
        body { font-family: Arial, sans-serif; margin: 40px; }
        footer { margin-top: 50px; color: gray; }
    </style>
</head>
```
The comment appears in the source code of both pages.

---

### Simplifying layout files

Now that the base template exists, individual layout files no longer need the complete HTML structure. They only need to define what goes inside the "main" block. This eliminates all the duplicate code.

The `{{ define "main" }}` statement tells Hugo to put everything between it and `{{ end }}` into the "main" block of the base template.

---

**Example** Replace the entire contents of `layouts/index.html` with:

```html
{{ define "main" }}
    <h1>Welcome to My Portfolio</h1>
    {{ .Content }}
{{ end }}
```

Save, refresh the browser, and verify the homepage still displays with the header, footer, and styling from the base template.

---

**Exercise** Replace the entire contents of `layouts/about/single.html` with only the define block for the main content, save, refresh the about page, and verify it displays correctly.

**Solution:**
```html
{{ define "main" }}
    <h1>About Me</h1>
    {{ .Content }}
{{ end }}
```
About page displays correctly with heading and content.

---

**Exercise** Count how many lines each layout file has now compared to before using the base template.

**Solution:**
Before: 15 lines in each file (30 total)
After: 4 lines in each file (8 total)
The files are now much shorter with no duplicate HTML.

---

**Example** Change the page title in `baseof.html` from "My Portfolio" to "Professional Portfolio":

```html
<head>
    <title>Professional Portfolio</title>
    ...
</head>
```

Restart the server, check the browser tab title on both the homepage and about page, and verify both show "Professional Portfolio".

---

**Exercise** Add a background color to the body in the base template's style section: `body { font-family: Arial, sans-serif; margin: 40px; background-color: #f5f5f5; }`, restart, and verify both pages now have a light gray background.

**Solution:**
```html
<style>
    body { font-family: Arial, sans-serif; margin: 40px; background-color: #f5f5f5; }
    footer { margin-top: 50px; color: gray; }
</style>
```
Both pages now have a light gray background.

---

**Exercise** Change the footer text in `baseof.html` to include your name instead of "My Portfolio", restart, and verify both pages show the updated footer without changing the individual layout files.

**Solution:**
```html
<footer>
    <p>© 2026 Jane Doe. All rights reserved.</p>
</footer>
```
Both pages show the updated footer with the new name.

---

## Section 2: Working with Template Blocks

Blocks allow different pages to customize specific sections while inheriting common structure. The base template can define multiple blocks, and each layout file can choose which blocks to override. If a layout file doesn't override a block, the default content from the base template appears.

This section covers understanding how the main block works, creating additional blocks in the base template, and overriding blocks selectively in different layouts. By the end of this section, the homepage and about page will have different headers while sharing other elements.

| Concept | Description |
|---------|-------------|
| `{{ block "name" . }}content{{ end }}` | Defines a named block with default content |
| `{{ define "name" }}content{{ end }}` | Overrides a block from base template |
| Default content | Content inside block definition that appears if not overridden |
| Block context (`.`) | Passes page data to blocks |

---

### Understanding the main content block

The main content block is where page-specific content appears. In the base template, `{{ block "main" . }}{{ end }}` creates a placeholder. In layout files, `{{ define "main" }}` fills that placeholder with custom content.

The dot (`.`) after the block name passes the current page context into the block. This allows access to page variables like `.Content`, `.Title`, and `.Params`.

---

**Example** Add default content inside the main block in `baseof.html`:

```html
<body>
    {{ block "main" . }}
        <p>This is default content that appears if no layout overrides this block.</p>
    {{ end }}
    <footer>
        <p>© 2026 My Portfolio. All rights reserved.</p>
    </footer>
</body>
```

Temporarily rename `layouts/index.html` to `layouts/index.html.backup`, restart the server, visit the homepage, and observe the default content appears.

---

**Exercise** Rename the file back from `layouts/index.html.backup` to `layouts/index.html`, restart, refresh the homepage, and verify the custom homepage content replaces the default content.

**Solution:**
```bash
mv layouts/index.html.backup layouts/index.html
hugo server -D
```
Homepage now shows the custom content instead of the default.

---

**Exercise** Temporarily rename `layouts/about/single.html` to `layouts/about/single.html.backup`, restart, visit the about page, observe the default content appears, then rename it back and restart to restore the custom about content.

**Solution:**
```bash
mv layouts/about/single.html layouts/about/single.html.backup
hugo server -D
```
About page shows default content. Then:
```bash
mv layouts/about/single.html.backup layouts/about/single.html
hugo server -D
```
About page shows custom content again.

---

**Exercise** In the main block's default content in `baseof.html`, add `{{ .Content }}` so it displays markdown content, restart, and test by renaming one layout file again to see the default block now shows markdown content.

**Solution:**
```html
{{ block "main" . }}
    <p>This is default content that appears if no layout overrides this block.</p>
    {{ .Content }}
{{ end }}
```
When a layout file is missing, the page now shows both the default text and the markdown content.

---

### Adding a header block

Additional blocks let different pages have different sections. A header block allows the homepage and about page to display different headings while sharing the same base structure.

When a block is defined in the base template, any layout file can override it. If a layout doesn't override a block, the default content from the base template appears.

---

**Example** Add a header block to `baseof.html` above the main block:

```html
<body>
    {{ block "header" . }}
        <h1>My Portfolio</h1>
    {{ end }}
    
    {{ block "main" . }}
        <p>This is default content.</p>
    {{ end }}
    
    <footer>
        <p>© 2026 My Portfolio. All rights reserved.</p>
    </footer>
</body>
```

Restart and verify both pages show "My Portfolio" as the heading.

---

**Exercise** Override the header block in `layouts/index.html` by adding a define statement before the main block:

```html
{{ define "header" }}
    <h1>Welcome to My Professional Portfolio</h1>
    <p>Showcasing my work and research</p>
{{ end }}

{{ define "main" }}
    {{ .Content }}
{{ end }}
```

Save, restart, refresh the homepage, and verify it shows the custom header.

**Solution:**
```html
{{ define "header" }}
    <h1>Welcome to My Professional Portfolio</h1>
    <p>Showcasing my work and research</p>
{{ end }}

{{ define "main" }}
    {{ .Content }}
{{ end }}
```
Homepage shows custom header with heading and paragraph.

---

**Exercise** Visit the about page and verify it still shows the default "My Portfolio" header because that layout doesn't override the header block.

**Solution:**
About page shows only "My Portfolio" heading - the default from the base template.

---

**Exercise** Override the header block in `layouts/about/single.html` with different content, restart, and verify the about page now has its own custom header while the homepage keeps its different header.

**Solution:**
```html
{{ define "header" }}
    <h1>About Me</h1>
    <p>Learn more about my background</p>
{{ end }}

{{ define "main" }}
    {{ .Content }}
{{ end }}
```
About page now has its own custom header different from the homepage.

---

**Exercise** Remove the header override from `layouts/index.html` (delete the `{{ define "header" }}...{{ end }}` block), restart, and verify the homepage now shows the default header again.

**Solution:**
```html
{{ define "main" }}
    {{ .Content }}
{{ end }}
```
Homepage now shows the default "My Portfolio" header from the base template.

---

### Adding a footer block

A footer block allows pages to have different footer content. Like other blocks, it can have default content that appears unless overridden. This demonstrates how multiple blocks work independently.

---

**Example** Move the footer content into a block in `baseof.html`:

```html
<body>
    {{ block "header" . }}
        <h1>My Portfolio</h1>
    {{ end }}
    
    {{ block "main" . }}
        <p>This is default content.</p>
    {{ end }}
    
    {{ block "footer" . }}
        <footer>
            <p>© 2026 My Portfolio. All rights reserved.</p>
        </footer>
    {{ end }}
</body>
```

Restart and verify both pages still show the footer.

---

**Exercise** Override the footer block in `layouts/about/single.html` to add contact information:

```html
{{ define "footer" }}
    <footer>
        <p>Contact: email@example.com</p>
        <p>© 2026 My Portfolio. All rights reserved.</p>
    </footer>
{{ end }}
```

Save, restart, visit the about page, and verify it shows the contact information in the footer.

**Solution:**
```html
{{ define "header" }}
    <h1>About Me</h1>
    <p>Learn more about my background</p>
{{ end }}

{{ define "main" }}
    {{ .Content }}
{{ end }}

{{ define "footer" }}
    <footer>
        <p>Contact: email@example.com</p>
        <p>© 2026 My Portfolio. All rights reserved.</p>
    </footer>
{{ end }}
```
About page footer now shows contact information plus copyright.

---

**Exercise** Visit the homepage and verify it still shows only the default footer without contact information.

**Solution:**
Homepage footer shows only "© 2026 My Portfolio. All rights reserved."

---

**Exercise** Add a different footer override to `layouts/index.html` that includes social media text (not actual links), restart, and verify the homepage and about page now have different footers.

**Solution:**
```html
{{ define "main" }}
    {{ .Content }}
{{ end }}

{{ define "footer" }}
    <footer>
        <p>Follow me on GitHub and LinkedIn</p>
        <p>© 2026 My Portfolio. All rights reserved.</p>
    </footer>
{{ end }}
```
Homepage footer shows social media text. About page footer shows contact email. Each page has different footer content.

---

**Exercise** Remove both footer overrides from the layout files, restart, and verify both pages return to showing the default footer from the base template.

**Solution:**
In `layouts/index.html`:
```html
{{ define "main" }}
    {{ .Content }}
{{ end }}
```

In `layouts/about/single.html`:
```html
{{ define "header" }}
    <h1>About Me</h1>
    <p>Learn more about my background</p>
{{ end }}

{{ define "main" }}
    {{ .Content }}
{{ end }}
```
Both pages now show the default footer.

---

## Section 3: Extracting Reusable Partials

Partials are small template pieces that can be included in any template file. Even with just two pages, elements like social links or contact information may appear in multiple places. Extracting these into partials avoids duplication and makes updates easier.

This section covers creating partial files, including them in templates, passing site parameters to partials, and passing custom data to partials. By the end of this section, repeated elements will be extracted into reusable components.

| Concept | Description |
|---------|-------------|
| `partials/filename.html` | Partial template file location |
| `{{ partial "filename.html" . }}` | Includes a partial, passes current context |
| `{{ .Site.Params.name }}` | Access site parameters in partials |
| `(dict "key" "value")` | Pass custom data to partials |
| `{{ .key }}` | Access passed data inside partial |

---

### Creating your first partial

A partial is created in the `partials/` directory. The partial file contains HTML and template code just like layout files. The `{{ partial }}` function includes the partial's content wherever it's called.

The dot (`.`) after the filename passes the current context to the partial, allowing it to access page and site data.

---

**Example** Create `partials/social-links.html`:

```html
<div>
    <p>Follow me:</p>
    <p>GitHub: github.com/username</p>
    <p>LinkedIn: linkedin.com/in/username</p>
</div>
```

Include it in the footer block of `baseof.html`:

```html
{{ block "footer" . }}
    <footer>
        {{ partial "social-links.html" . }}
        <p>© 2026 My Portfolio. All rights reserved.</p>
    </footer>
{{ end }}
```

Restart and verify both pages show the social links in the footer.

---

**Exercise** Change the GitHub username in `partials/social-links.html`, restart, and verify both pages update automatically without touching the base template or layout files.

**Solution:**
```html
<div>
    <p>Follow me:</p>
    <p>GitHub: github.com/newusername</p>
    <p>LinkedIn: linkedin.com/in/username</p>
</div>
```
Both pages show the updated GitHub username.

---

**Exercise** Create a new partial file `partials/copyright.html` containing just the copyright line, include it in the footer block instead of the inline `<p>` tag, restart, and verify it appears on both pages.

**Solution:**
Create `partials/copyright.html`:
```html
<p>© 2026 My Portfolio. All rights reserved.</p>
```

Update `baseof.html`:
```html
{{ block "footer" . }}
    <footer>
        {{ partial "social-links.html" . }}
        {{ partial "copyright.html" . }}
    </footer>
{{ end }}
```
Both pages show the copyright line from the partial.

---

**Exercise** Create `partials/page-header.html` with a simple heading style, include it in the header block of `baseof.html`, restart, and verify it appears on pages that don't override the header block.

**Solution:**
Create `partials/page-header.html`:
```html
<h1 style="color: #333; border-bottom: 2px solid #333;">My Portfolio</h1>
```

Update `baseof.html`:
```html
{{ block "header" . }}
    {{ partial "page-header.html" . }}
{{ end }}
```
Pages without header overrides show the styled header from the partial.

---

### Partials with site parameters

Partials can access site configuration from `hugo.toml` using `{{ .Site.Params }}`. This allows partials to display dynamic content without hardcoding values. When site parameters change, all partials using them update automatically.

---

**Example** Add author information to `hugo.toml`:

```toml
title = 'Professional Portfolio'

[params]
author = "Your Name"
github = "yourusername"
linkedin = "yourusername"
```

Update `partials/social-links.html` to use these parameters:

```html
<div>
    <p>Follow {{ .Site.Params.author }}:</p>
    <p>GitHub: github.com/{{ .Site.Params.github }}</p>
    <p>LinkedIn: linkedin.com/in/{{ .Site.Params.linkedin }}</p>
</div>
```

Restart and verify the author name and usernames appear in the footer.

---

**Exercise** Change the author name in `hugo.toml`, restart, and verify the footer updates on both pages without changing the partial file.

**Solution:**
```toml
[params]
author = "Jane Doe"
github = "yourusername"
linkedin = "yourusername"
```
Both pages now show "Follow Jane Doe:" in the footer.

---

**Exercise** Add `email = "your.email@example.com"` to the `[params]` section in `hugo.toml`, update the social-links partial to display it, restart, and verify the email appears on both pages.

**Solution:**
In `hugo.toml`:
```toml
[params]
author = "Jane Doe"
github = "yourusername"
linkedin = "yourusername"
email = "jane@example.com"
```

In `partials/social-links.html`:
```html
<div>
    <p>Follow {{ .Site.Params.author }}:</p>
    <p>Email: {{ .Site.Params.email }}</p>
    <p>GitHub: github.com/{{ .Site.Params.github }}</p>
    <p>LinkedIn: linkedin.com/in/{{ .Site.Params.linkedin }}</p>
</div>
```
Both pages show the email address.

---

**Exercise** Create a new partial `partials/author-bio.html` that displays author name and a bio from `hugo.toml` (add `bio` parameter first), include it in the main block of `layouts/index.html`, restart, and verify it appears only on the homepage.

**Solution:**
In `hugo.toml`:
```toml
[params]
author = "Jane Doe"
github = "yourusername"
linkedin = "yourusername"
email = "jane@example.com"
bio = "Researcher specializing in data science and machine learning."
```

Create `partials/author-bio.html`:
```html
<div>
    <h2>{{ .Site.Params.author }}</h2>
    <p>{{ .Site.Params.bio }}</p>
</div>
```

In `layouts/index.html`:
```html
{{ define "main" }}
    {{ partial "author-bio.html" . }}
    {{ .Content }}
{{ end }}
```
Bio appears on homepage only.

---

**Exercise** Include the same author-bio partial in `layouts/about/single.html`, restart, and verify the same content appears on both pages because it pulls from the same site parameters.

**Solution:**
In `layouts/about/single.html`:
```html
{{ define "header" }}
    <h1>About Me</h1>
    <p>Learn more about my background</p>
{{ end }}

{{ define "main" }}
    {{ partial "author-bio.html" . }}
    {{ .Content }}
{{ end }}
```
Same bio now appears on both pages.

---

### Partials with custom data

Partials can receive custom data instead of just the page context. The `dict` function creates a dictionary of key-value pairs that gets passed to the partial. Inside the partial, `{{ .key }}` accesses the values.

This allows the same partial to display different content depending on where it's used.

---

**Example** Create `partials/info-box.html`:

```html
<div style="border: 2px solid #333; padding: 15px; margin: 20px 0;">
    <h3>{{ .title }}</h3>
    <p>{{ .text }}</p>
</div>
```

Use it in `layouts/index.html` with custom data:

```html
{{ define "main" }}
    {{ partial "info-box.html" (dict "title" "Featured" "text" "Welcome to my portfolio site.") }}
    {{ .Content }}
{{ end }}
```

Restart and verify the info box appears on the homepage with the specified title and text.

---

**Exercise** Add another info-box partial call in the same layout file with different title and text values, restart, and verify both boxes appear with different content.

**Solution:**
```html
{{ define "main" }}
    {{ partial "info-box.html" (dict "title" "Featured" "text" "Welcome to my portfolio site.") }}
    {{ partial "info-box.html" (dict "title" "Latest News" "text" "Check out my recent publications.") }}
    {{ .Content }}
{{ end }}
```
Homepage shows two info boxes with different content.

---

**Exercise** Use the info-box partial in `layouts/about/single.html` with completely different data, restart, and verify each page shows different info boxes despite using the same partial.

**Solution:**
```html
{{ define "header" }}
    <h1>About Me</h1>
    <p>Learn more about my background</p>
{{ end }}

{{ define "main" }}
    {{ partial "info-box.html" (dict "title" "Background" "text" "I have 10 years of experience in research.") }}
    {{ .Content }}
{{ end }}
```
About page shows different info box content than homepage.

---

**Exercise** Change the border style in `partials/info-box.html` to `border: 3px dashed blue;`, restart, and verify all info boxes on both pages update with the new style.

**Solution:**
```html
<div style="border: 3px dashed blue; padding: 15px; margin: 20px 0;">
    <h3>{{ .title }}</h3>
    <p>{{ .text }}</p>
</div>
```
All info boxes on all pages now have blue dashed borders.

---

**Example** Create a more complex partial that accepts multiple fields. Create `partials/skill-card.html`:

```html
<div style="border: 1px solid #ccc; padding: 10px; margin: 10px 0;">
    <h4>{{ .name }}</h4>
    <p>Level: {{ .level }}</p>
    <p>Experience: {{ .years }} years</p>
</div>
```

Use it in `layouts/index.html`:

```html
{{ define "main" }}
    <h2>Skills</h2>
    {{ partial "skill-card.html" (dict "name" "Python" "level" "Advanced" "years" 5) }}
    {{ partial "skill-card.html" (dict "name" "R" "level" "Intermediate" "years" 3) }}
    {{ .Content }}
{{ end }}
```

Restart and verify both skill cards appear with different data.

---

**Exercise** Add a third skill card with different values to the homepage layout, restart, and verify all three display correctly.

**Solution:**
```html
{{ define "main" }}
    <h2>Skills</h2>
    {{ partial "skill-card.html" (dict "name" "Python" "level" "Advanced" "years" 5) }}
    {{ partial "skill-card.html" (dict "name" "R" "level" "Intermediate" "years" 3) }}
    {{ partial "skill-card.html" (dict "name" "JavaScript" "level" "Beginner" "years" 1) }}
    {{ .Content }}
{{ end }}
```
Three skill cards appear with different data.

---

**Exercise** Modify the skill-card partial to add a description field, update the partial calls to include `"description" "Some text"`, restart, and verify the descriptions appear in all skill cards.

**Solution:**
In `partials/skill-card.html`:
```html
<div style="border: 1px solid #ccc; padding: 10px; margin: 10px 0;">
    <h4>{{ .name }}</h4>
    <p>Level: {{ .level }}</p>
    <p>Experience: {{ .years }} years</p>
    <p>{{ .description }}</p>
</div>
```

In `layouts/index.html`:
```html
{{ define "main" }}
    <h2>Skills</h2>
    {{ partial "skill-card.html" (dict "name" "Python" "level" "Advanced" "years" 5 "description" "Used for data analysis and machine learning") }}
    {{ partial "skill-card.html" (dict "name" "R" "level" "Intermediate" "years" 3 "description" "Statistical computing and graphics") }}
    {{ partial "skill-card.html" (dict "name" "JavaScript" "level" "Beginner" "years" 1 "description" "Web development and visualizations") }}
    {{ .Content }}
{{ end }}
```
All skill cards show descriptions.

---

**Exercise** Change the styling in `partials/skill-card.html` (background color, padding, border), restart, and verify all skill cards on all pages update with the new styling without changing any layout files.

**Solution:**
```html
<div style="border: 2px solid #007bff; padding: 20px; margin: 15px 0; background-color: #f0f8ff;">
    <h4>{{ .name }}</h4>
    <p>Level: {{ .level }}</p>
    <p>Experience: {{ .years }} years</p>
    <p>{{ .description }}</p>
</div>
```
All skill cards now have blue border, more padding, and light blue background.

---