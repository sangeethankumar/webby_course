# Building Hugo Sites Without Themes: HTML, Layouts, and Data

Hugo builds websites by reading content files and layout templates. Layouts are HTML files that control how content appears in the browser. Without a theme, layouts must be created manually. Hugo's template language allows layouts to display dynamic content from configuration files and data files.

Here we will see:

- how to create layout files from scratch
- how template variables display dynamic content
- how data files work with loops

---

## Section 1: Creating Custom Layouts

Hugo requires layout files to display content. Themes provide these layouts automatically, but without a theme, the layout files must be created manually. The homepage layout is stored at `layouts/index.html`. This file contains HTML code that the browser displays, along with Hugo template syntax that inserts content.

This section covers creating the homepage layout file, understanding HTML structure, adding layout elements around content, and using HTML tags. By the end of this section, there will be a working homepage displaying content through a custom layout.

| File/Concept | Description |
|--------------|-------------|
| `layouts/index.html` | Layout file for the homepage |
| `{{ .Content }}` | Placeholder where markdown content appears |
| `<!DOCTYPE html>` | Declaration that this is an HTML document |
| `<html>`, `<head>`, `<body>` | Required HTML structure tags |
| `<h1>`, `<h2>`, `<h3>` | Heading tags (h1 largest, h3 smallest) |
| `<p>` | Paragraph tag |
| `<ul>`, `<ol>`, `<li>` | List tags (unordered, ordered, list item) |
| `<a href="url">` | Link tag |
| `<div>` | Container tag for grouping |

---

### Understanding the layout requirement

Hugo cannot display pages without layout templates. When a theme is used, it provides these templates. Without a theme, Hugo looks for layout files in the `layouts/` directory but finds nothing, resulting in a "Page Not Found" error even when content files exist.

---

**Example** Create a new Hugo site and add homepage content:

```bash
hugo new site html-portfolio
cd html-portfolio
hugo new content _index.md
```

Edit `content/_index.md`:

```markdown
---
title: "Home"
---

## About Me

I am a researcher specializing in data science.
```

Start the server with `hugo server -D` and navigate to `http://localhost:1313/`. The page shows an error because no layout file exists.

---

**Exercise** With the server running, verify that the homepage shows an error even though the content file exists.

---

**Exercise** Check the `layouts/` directory and verify it is empty.

---

### Creating the homepage layout

The homepage layout must be created at `layouts/index.html`. The simplest possible layout contains only the `{{ .Content }}` placeholder, which Hugo replaces with the markdown content from `content/_index.md`.

---

**Example** Create `layouts/index.html` with this content:

```html
{{ .Content }}
```

Save, refresh the browser, and verify the markdown content now appears.

---

**Exercise** Add a second paragraph to `content/_index.md`, save, and verify it appears in the browser.

---

**Exercise** Delete `{{ .Content }}` from the layout file, save, refresh the browser, and observe the page is blank. Add `{{ .Content }}` back.

---

**Exercise** Add text before the placeholder: `Welcome {{ .Content }}`, save, and observe both the text and markdown content appear.

---

**Example** Update `layouts/index.html` with proper HTML structure:

```html
<!DOCTYPE html>
<html>
<head>
    <title>My Portfolio</title>
</head>
<body>
    {{ .Content }}
</body>
</html>
```

Save and verify the content still displays, and the browser tab now shows "My Portfolio".

---

**Exercise** Change the title to your name, save, and verify the browser tab updates.

---

**Exercise** Open browser DevTools (F12), examine the page structure, and verify the `<html>`, `<head>`, and `<body>` tags are present.

---

### Adding layout elements around content

Content inside the `<body>` tags appears on the page. HTML can be added before and after the `{{ .Content }}` placeholder to create headers, footers, and other layout elements that appear on every page.

HTML uses tags with opening `<tag>` and closing `</tag>` parts. Headings use `<h1>` through `<h6>` tags, with h1 being largest. Paragraphs use `<p>` tags.

---

**Example** Add a header and footer:

```html
<body>
    <h1>Research Portfolio</h1>
    {{ .Content }}
    <p>Last updated: January 2025</p>
</body>
```

Save and observe the heading appears above content and the footer below.

---

**Exercise** Change the heading text to your name, save, and verify it updates.

---

**Exercise** Add a paragraph after the heading: `<p>Welcome to my website.</p>`, save, and verify it appears between the heading and content.

---

**Exercise** Move `{{ .Content }}` to appear before the `<h1>` heading, save, observe the order changes, then move it back.

---

**Example** Add multiple heading levels and paragraphs:

```html
<body>
    <h1>Research Portfolio</h1>
    <h2>Welcome</h2>
    <p>This website showcases my research and projects.</p>
    
    {{ .Content }}
    
    <p>Last updated: January 2025</p>
</body>
```

Save and observe the heading hierarchy and paragraph spacing.

---

**Exercise** Change `<h2>` to `<h3>`, save, and observe the heading becomes smaller.

---

**Exercise** Add a second paragraph after "Last updated", save, and verify both paragraphs have spacing between them.

---

**Exercise** Remove only the closing `</p>` tag from one paragraph, save, observe what happens, then add it back.

---

### Using HTML tags for structure

HTML provides tags for organizing content. Lists display multiple related items. Links create clickable connections. Container tags group related sections.

Unordered lists use `<ul>` and display bullets. Ordered lists use `<ol>` and display numbers. Each item uses `<li>`. The `<a>` tag creates links with the `href` attribute. The `<div>` tag groups related content.

---

**Example** Add a skills section with a list:

```html
<h2>Skills</h2>
<h3>Programming Languages</h3>
<ul>
    <li>Python</li>
    <li>R</li>
    <li>JavaScript</li>
</ul>
```

Save and observe the bullet points.

---

**Exercise** Add two more programming languages to the list, save, and verify they appear with bullets.

---

**Exercise** Change `<ul>` to `<ol>` (both opening and closing tags), save, and observe bullets change to numbers.

---

**Exercise** Change `<ol>` back to `<ul>`, save, and verify bullets return.

---

**Example** Add a contact section with links:

```html
<h2>Contact</h2>
<p>Email: <a href="mailto:name@example.com">name@example.com</a></p>
<p><a href="https://linkedin.com/in/profile">LinkedIn Profile</a></p>
```

Save, click the links, and verify they work.

---

**Exercise** Change the email address in both locations (inside `href=""` and between the tags), save, and verify the link works.

---

**Exercise** Add a paragraph with a GitHub link, save, and verify it opens GitHub.

---

**Exercise** Remove the `href="..."` attribute from one link (keep the `<a>` tags), save, observe the text is not clickable, then add the href back.

---

**Example** Group the Skills section with a div:

```html
<div>
    <h2>Skills</h2>
    <h3>Programming Languages</h3>
    <ul>
        <li>Python</li>
        <li>R</li>
        <li>JavaScript</li>
    </ul>
</div>
```

Save and observe the page looks the same (divs affect structure, not appearance).

---

**Exercise** Wrap the Contact section in a `<div>`, save, and verify the page looks unchanged.

---

**Exercise** In browser DevTools (F12), find one div element and verify it contains all the nested content.

---

## Section 2: Using Template Variables

Template variables are placeholders written inside double curly braces `{{ }}`. Hugo replaces these with actual data when building the site. Variables starting with `.Site` access configuration from `hugo.toml`. Variables starting with `.Params` access data from YAML files. This allows content to be updated without changing HTML.

This section covers using site configuration variables, creating homepage-specific data, and conditional display. By the end of this section, the layout will display dynamic information from data files.

| Template Syntax | Description | Data Source |
|-----------------|-------------|-------------|
| `{{ .Site.Title }}` | Site title | `hugo.toml` → `title =` |
| `{{ .Site.Params.name }}` | Custom site parameter | `hugo.toml` → `[params]` section |
| `{{ .Params.field }}` | Homepage data | `data/homepage.yaml` |
| `{{ if .variable }}` | Conditional display | Shows content only if variable exists |
| `{{ end }}` | End conditional block | Closes if statement |

---

### Accessing site configuration

Site-wide information can be stored in `hugo.toml` and accessed in layouts using `.Site` variables. This centralizes configuration so updates in one place affect all pages. The `[params]` section stores custom parameters.

---

**Example** Add parameters to `hugo.toml`:

```toml
title = "Research Portfolio"

[params]
author = "Your Name"
email = "name@example.com"
```

Update the Contact section in `layouts/index.html`:

```html
<h2>Contact</h2>
<p>Email {{ .Site.Params.author }}: <a href="mailto:{{ .Site.Params.email }}">{{ .Site.Params.email }}</a></p>
```

Restart the server (Ctrl+C, then `hugo server -D`) and verify the name and email appear.

---

**Exercise** Change the author name in `hugo.toml`, restart the server, and verify the page updates without changing HTML.

---

**Exercise** Change the email in `hugo.toml`, restart, and verify the Contact section reflects the change.

---

**Exercise** Add `linkedin = "username"` to the `[params]` section, add a paragraph displaying it: `<p>LinkedIn: {{ .Site.Params.linkedin }}</p>`, restart, and verify it appears.

---

**Exercise** Add a `github` parameter to `hugo.toml`, create a link using `<a href="https://github.com/{{ .Site.Params.github }}">GitHub</a>`, restart, and verify the link works.

---

### Using homepage-specific data

Homepage-specific data can be stored in `data/homepage.yaml`. Hugo reads this file and makes it available through `.Params` variables. This separates homepage content from site-wide configuration.

---

**Example** Create `data/homepage.yaml`:

```yaml
intro: "I am a researcher specializing in data science and machine learning."
tagline: "Building tools for scientific discovery"
```

Add these to the layout after the main heading:

```html
<body>
    <h1>Research Portfolio</h1>
    <p>{{ .Params.intro }}</p>
    <p>{{ .Params.tagline }}</p>
    
    {{ .Content }}
    ...
</body>
```

Restart and verify both lines appear.

---

**Exercise** Change the intro text in `homepage.yaml`, restart, and verify the page updates.

---

**Exercise** Add `experience: "5 years in research"` to `homepage.yaml`, display it with `<p>{{ .Params.experience }}</p>`, restart, and verify it appears.

---

**Exercise** Add two more fields to `homepage.yaml`, display them in the layout, restart, and verify all fields appear.

---

### Conditional display

The `{{ if }}` statement checks if a variable has a value. Content between `{{ if }}` and `{{ end }}` only appears if the variable exists. This makes layouts flexible for optional information.

---

**Example** Make the LinkedIn link optional:

```html
{{ if .Site.Params.linkedin }}
    <p><a href="https://linkedin.com/in/{{ .Site.Params.linkedin }}">LinkedIn</a></p>
{{ end }}
```

Restart and verify the link appears.

---

**Exercise** Remove the `linkedin =` line from `hugo.toml`, restart, and verify the LinkedIn paragraph disappears.

---

**Exercise** Add the linkedin parameter back, restart, and verify the paragraph returns.

---

**Exercise** Wrap the GitHub link in an `{{ if }}` block, restart, and verify it still appears when the parameter exists.

---

**Exercise** Remove the `{{ end }}` from an if block, save, observe the error message, then add `{{ end }}` back and restart.

---

## Section 3: Working with Data Files

Data files store lists of items with multiple fields. The `{{ range }}` loop iterates through each item in a list. Inside the loop, `{{ .fieldname }}` accesses the current item's fields. This separates data from presentation, making both easier to maintain.

This section covers creating data files with lists, looping through lists with range, and accessing fields inside loops. By the end of this section, entire sections will be built dynamically from data files.

| Concept | Description | Example |
|---------|-------------|---------|
| `data/filename.yaml` | Data file in YAML format | Stores structured data |
| `{{ range .Site.Data.filename }}` | Loop through list | Iterates each item |
| `{{ .fieldname }}` | Access field | Gets value of field in current item |
| `{{ end }}` | End loop | Closes range block |

---

### Creating data files with lists

Data files can store lists where each item has multiple fields. YAML format uses hyphens to denote list items and indentation to show structure. Each item can have different fields with different values.

---

**Example** Create `data/skills.yaml`:

```yaml
- name: Python
  level: Advanced
  
- name: R
  level: Intermediate
  
- name: JavaScript
  level: Beginner
```

This file contains a list of three skills. Each skill has two fields: name and level.

---

**Exercise** Add two more skills to `skills.yaml` with name and level fields, save the file, and verify the file has five skills total.

---

**Exercise** Change Python's level from "Advanced" to "Expert", save, and verify the change in the file.

---

### Looping through data with range

The `{{ range }}` loop iterates through each item in a data file list. Hugo accesses the data file using `.Site.Data.filename` where filename matches the YAML file name. The loop must end with `{{ end }}`.

---

**Example** Display the skills list in `layouts/index.html`:

```html
<h2>Skills</h2>
<ul>
{{ range .Site.Data.skills }}
    <li>{{ .name }} - {{ .level }}</li>
{{ end }}
</ul>
```

Restart and verify all skills appear with their levels.

---

**Exercise** Remove one skill from `skills.yaml`, restart, and verify it disappears from the page.

---

**Exercise** Add the skill back to `skills.yaml`, restart, and verify it reappears on the page.

---

**Exercise** Remove the `{{ end }}` from the range loop, restart, observe the error message, then add `{{ end }}` back.

---

### Accessing fields inside loops

Inside a range loop, `{{ .fieldname }}` accesses the current item's fields. Different fields can be displayed in different parts of the HTML. Additional fields can be added to the data file and displayed in the template.

---

**Example** Add a years field to skills and display it:

Update `data/skills.yaml`:

```yaml
- name: Python
  level: Expert
  years: 5
  
- name: R
  level: Intermediate
  years: 3
  
- name: JavaScript
  level: Beginner
  years: 1
```

Update the template:

```html
<ul>
{{ range .Site.Data.skills }}
    <li>{{ .name }} - {{ .level }} ({{ .years }} years)</li>
{{ end }}
</ul>
```

Restart and verify years appear for all skills.

---

**Exercise** Add a `category` field to each skill (such as "Language" or "Framework"), display it in the template before the name, restart, and verify categories appear.

---

**Exercise** Change one skill's years value, restart, and verify only that skill's years update on the page.

---

**Example** Create a projects data file with multiple fields:

Create `data/projects.yaml`:

```yaml
- title: Data Pipeline
  description: Automated processing system for research data
  year: 2024

- title: Visualization Tool
  description: Interactive dashboard for experimental results
  year: 2023
```

Add a Projects section to the layout:

```html
<h2>Projects</h2>
{{ range .Site.Data.projects }}
    <div>
        <h3>{{ .title }}</h3>
        <p>{{ .description }}</p>
        <p>Year: {{ .year }}</p>
    </div>
{{ end }}
```

Restart and verify both projects display with all fields.

---

**Exercise** Add a third project with title, description, and year fields, restart, and verify it appears.

---

**Exercise** Add a `status` field (such as "Completed" or "In Progress") to each project, display it in the template, restart, and verify all projects show their status.

---

**Exercise** Change one project's description, restart, and verify only that project updates on the page.

---

