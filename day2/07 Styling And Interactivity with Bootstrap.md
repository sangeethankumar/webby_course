# Styling Custom Layouts with Bootstrap

Bootstrap is a CSS framework that provides pre-written styles for common design patterns. Bootstrap classes applied to HTML elements control their appearance without writing custom CSS. Bootstrap requires loading CSS and JavaScript files through CDN links. Once loaded, Bootstrap classes work in all Hugo layouts.

Here we will see:

- how to load Bootstrap in Hugo templates
- how to use typography and spacing utilities
- how to create navigation bars
- how to structure layouts with containers and grid
- how to use cards, buttons, badges, and alerts

---

## Initial Setup

This section provides the files needed to use Bootstrap with your custom layouts. These files convert the standalone layouts from Document 05 to use a base template pattern. Content files with the necessary front matter fields are also provided. Create these files exactly as shown.

### Verifying site configuration

Open your `hugo.toml` and verify it contains the following. If any sections are missing, add them:

```toml
baseURL = 'http://localhost:1313/'
title = 'My Portfolio'
languageCode = 'en'

[params]
name = "Your Name"
tagline = "Research and Projects"

[[menu.main]]
name = "About"
url = "/about/"
weight = 1

[[menu.main]]
name = "Projects"
url = "/projects/"
weight = 2

[[menu.main]]
name = "Contact"
url = "/contact/"
weight = 3

[module]
[[module.imports]]
path = "github.com/halogenica/beautifulhugo"
```

### Creating content files

Replace or create the following content files:

**File: `content/_index.md`**
```markdown
---
title: "Home"
subtitle: "Machine Learning Research"
draft: false
---

## About

Research focused on machine learning and data science.

## Current Work

Working on neural network optimization and computer vision projects.

## Contact

Email: contact@example.com
```

**File: `content/about/index.md`**
```markdown
---
title: "About"
date: 2024-01-15
description: "Background and skills"
draft: false
---

During my Ph.D., I built pipelines to download, process, and analyze TESS data. I worked mainly in Python. I enjoyed this work, not just for my own research. I also helped other researchers with their code.

In my current role, I work with researchers on their programming needs. This also helps me prepare for a future in industry.

## Skills

Programming Languages: Python, R, C++, Matlab

Frameworks: Numpy, pandas, scipy

Tools: Git, Jupyter, Docker, LaTeX
```

**File: `content/projects/_index.md`**
```markdown
---
title: "Projects"
draft: false
---

I have worked on several research projects involving data analysis and software development. Below are some of my key projects.
```

**File: `content/projects/project-one.md`**
```markdown
---
title: "TESS Data Pipeline"
year: 2024
status: "Active"
tech: "Python"
github: "https://github.com/username/tess-pipeline"
draft: false
---

I built pipelines to download, process, and analyze TESS data. The pipeline includes automated quality control, error correction, and period analysis.

The system processes large datasets efficiently and provides researchers with clean, analysis-ready data.
```

**File: `content/projects/project-two.md`**
```markdown
---
title: "Light Curve Analysis Tool"
year: 2023
status: "Complete"
tech: "Python"
github: "https://github.com/username/light-curve"
draft: false
---

Tools to merge and analyze multi-sector photometric data from space missions. The tools handle large datasets and identify periodic signals.

Used by multiple research groups for analyzing stellar variability.
```

**File: `content/projects/project-three.md`**
```markdown
---
title: "Exoplanet Detection System"
year: 2024
status: "In Progress"
tech: "Python"
github: "https://github.com/username/exoplanet"
draft: false
---

Machine learning approach to detecting exoplanet transit signals in photometric time series data.

Currently testing different neural network architectures for improved detection accuracy.
```

**File: `content/contact/index.md`**
```markdown
---
title: "Contact"
description: "Get in touch"
draft: false
---

## Get in Touch

Email: contact@example.com

GitHub: github.com/username

LinkedIn: linkedin.com/in/username
```

### Creating the base template

The base template loads Bootstrap resources and defines the overall page structure. All other layouts inherit from this template.

1. Create directory `layouts/_default/` if it does not exist.
2. Create file `layouts/_default/baseof.html` with the following content:
   ```html
   <!DOCTYPE html>
   <html lang="en">
   <head>
     <meta charset="UTF-8">
     <meta name="viewport" content="width=device-width, initial-scale=1.0">
     <title>{{ .Title }} - {{ .Site.Title }}</title>
     <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet">
   </head>
   <body>
     {{ block "main" . }}{{ end }}
     <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/js/bootstrap.bundle.min.js"></script>
   </body>
   </html>
   ```

### Converting homepage layout

Replace your existing `layouts/index.html` with:

```html
{{ define "main" }}
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
{{ end }}
```

### Converting default single layout

Replace your existing `layouts/_default/single.html` with:

```html
{{ define "main" }}
<h1>{{ .Title }}</h1>
<p>{{ .Params.description }}</p>
<p>Last updated: {{ .Date.Format "January 2, 2006" }}</p>
{{ .Content }}
{{ end }}
```

### Converting default list layout

Replace your existing `layouts/_default/list.html` with:

```html
{{ define "main" }}
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
{{ end }}
```

### Converting about page layout

Replace your existing `layouts/about/single.html` with:

```html
{{ define "main" }}
<h1>About {{ .Site.Params.name }}</h1>
{{ .Content }}
<p><a href="/">Back to Home</a></p>
{{ end }}
```

### Converting projects list layout

Replace your existing `layouts/projects/list.html` with:

```html
{{ define "main" }}
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
{{ end }}
```

### Converting individual project layout

Replace your existing `layouts/projects/single.html` with:

```html
{{ define "main" }}
<h1>{{ .Title }}</h1>
<p>Year: {{ .Params.year }} | Status: {{ .Params.status }}</p>
{{ if .Params.github }}
<p><a href="{{ .Params.github }}">View on GitHub</a></p>
{{ end }}
{{ .Content }}
<p><a href="/projects/">Back to Projects</a></p>
{{ end }}
```

### Verifying Bootstrap loads

**Exercises**

1. Start the server with `hugo server -D` and navigate to `http://localhost:1313/`.
2. Verify the homepage displays with the title, subtitle, and content sections.
3. Right-click anywhere on the page and select "View Page Source".
4. Verify the `<head>` section contains the Bootstrap CSS link starting with `https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css`.
5. Verify the end of the `<body>` section contains the Bootstrap JavaScript link starting with `https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/js/bootstrap.bundle.min.js`.
6. Navigate to `/about/` and verify the about page displays correctly.
7. Navigate to `/projects/` and verify all three projects appear in the list.
8. Click on a project title and verify the individual project page displays with year, status, and GitHub link.

---

## Section 1: Typography and Spacing Utilities

Bootstrap typography classes control text appearance. Spacing classes control margins and padding. These utilities work on any HTML element without requiring additional structure.

### Text color utilities

Bootstrap provides color classes that change text color. Classes like `text-primary`, `text-success`, and `text-danger` apply colors. The `text-muted` class creates gray text for secondary information.

**Exercises**

1. Open `layouts/index.html`. Find the `<p>` tag containing `{{ .Site.Params.tagline }}`. Add `class="text-muted"` to this tag.
2. Save and reload the homepage. Verify the tagline appears in gray.
3. Change the class from `text-muted` to `text-primary`. Reload and verify the tagline appears in blue.
4. Change the class to `text-success`. Reload and verify the tagline appears in green.

---

### Text size and weight utilities

Bootstrap display classes create large headings. Font weight classes like `fw-bold` and `fw-light` change text thickness. These classes can be combined with color classes.

**Exercises**

1. In `layouts/index.html`, find the `<h1>` tag in the header section. Add `class="display-4"` to this tag.
2. Reload and verify the title appears much larger.
3. Change the class from `display-4` to `display-1`. Reload and verify the title becomes even larger.
4. Open `layouts/_default/single.html`. Find the `<h1>` tag and add `class="fw-bold text-primary"`.
5. Navigate to `/about/` and verify the title is bold and blue.

---

### Text alignment utilities

Bootstrap alignment classes control horizontal text positioning. The `text-center`, `text-start`, and `text-end` classes align content without requiring wrapper elements.

**Exercises**

1. In `layouts/index.html`, find the `<header>` tag. Add `class="text-center"` to this tag.
2. Reload and verify both the title and tagline are centered.
3. Change the class from `text-center` to `text-end`. Reload and verify the header content aligns to the right.
4. Change back to `text-center` and save.

---

### Spacing utilities for margins

Bootstrap spacing classes add margins around elements. Classes like `mt-3` add top margin, `mb-4` adds bottom margin, and `my-5` adds vertical margins. Numbers range from 0 to 5, representing increasing spacing.

**Exercises**

1. In `layouts/index.html`, find the `<header>` tag. Add `my-5` to the existing class attribute so it reads `class="text-center my-5"`.
2. Reload and verify space appears above and below the header.
3. Change `my-5` to `mt-5 mb-3`. Reload and verify the top margin is larger than the bottom margin.
4. Find the `<h2>` tag in the main section. Add `class="mb-4"` to this tag.
5. Reload and verify space appears between the subtitle and content.

---

### Spacing utilities for padding

Bootstrap padding classes add space inside elements. Classes like `p-3` add padding on all sides, while `px-4` adds horizontal padding and `py-2` adds vertical padding.

**Exercises**

1. In `layouts/index.html`, find the `<footer>` tag. Add `class="p-3"` to this tag.
2. Reload and verify the footer text has space around it.
3. Change the class from `p-3` to `py-2`. Reload and verify padding appears only on top and bottom.
4. Open `layouts/_default/single.html`. Add `class="mb-4"` to the first `<p>` tag (the one with description).
5. Add `class="text-muted fst-italic mb-4"` to the second `<p>` tag (the one with the date).
6. Navigate to `/about/` and verify spacing appears between title, description, date, and content.

---

## Section 2: Navigation Components

Bootstrap navbar provides a navigation bar with branding and menu links. Hugo menu configuration from Document 03 provides the menu items. This section starts with a simple HTML navbar and progressively adds Bootstrap classes to enhance appearance and behavior.

### Creating a basic HTML navbar

A navbar starts as a simple HTML structure with a `<nav>` element containing links. This navbar uses Hugo's menu system to generate links automatically.

**Exercises**

1. Open `layouts/_default/baseof.html`. After the opening `<body>` tag, add a simple navbar:
   ```html
   <body>
     <nav>
       <a href="/">{{ .Site.Title }}</a>
       <div>
         {{ range .Site.Menus.main }}
         <a href="{{ .URL }}">{{ .Name }}</a>
         {{ end }}
       </div>
     </nav>
     {{ block "main" . }}{{ end }}
     <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/js/bootstrap.bundle.min.js"></script>
   </body>
   ```
2. Reload any page and verify a basic navigation bar appears at the top with the site title and menu links.
3. Click each menu link and verify navigation works.
4. Verify the site title link navigates to the homepage.

---

### Adding Bootstrap navbar classes

Bootstrap navbar classes transform the plain HTML into a styled navigation bar. The `navbar` class provides base navbar styles. The `navbar-brand` class styles the site title. The `nav-link` class styles individual menu items.

**Exercises**

1. In `layouts/_default/baseof.html`, find the `<nav>` tag. Add `class="navbar"`.
2. Find the site title link. Add `class="navbar-brand"`.
3. Find the inner `<div>` that wraps the menu range loop. Add `class="navbar-nav"`.
4. Find each menu link inside the range loop. Add `class="nav-link"`.
5. Reload and verify the navbar now has Bootstrap styling with proper spacing and alignment.

---

### Adding navbar layout classes

Bootstrap provides layout classes that control navbar structure. The `navbar-expand-lg` class makes the navbar horizontal on large screens. Adding a `container-fluid` wrapper inside the navbar constrains content width.

**Exercises**

1. Find the `<nav>` tag. Add `navbar-expand-lg` to the class attribute so it reads `class="navbar navbar-expand-lg"`.
2. After the opening `<nav>` tag, wrap all content in a div:
   ```html
   <nav class="navbar navbar-expand-lg">
     <div class="container-fluid">
       <a class="navbar-brand" href="/">{{ .Site.Title }}</a>
       <div class="navbar-nav">
         {{ range .Site.Menus.main }}
         <a class="nav-link" href="{{ .URL }}">{{ .Name }}</a>
         {{ end }}
       </div>
     </div>
   </nav>
   ```
3. Reload and verify the navbar content is properly contained.

---

### Aligning menu items to the right

Bootstrap spacing utilities control element positioning within the navbar. The `ms-auto` class pushes elements to the right by applying automatic left margin.

**Exercises**

1. Find the `<div class="navbar-nav">`. Add `ms-auto` to the class attribute so it reads `class="navbar-nav ms-auto"`.
2. Reload and verify the menu items now appear on the right side of the navbar.
3. Remove `ms-auto` from the class. Reload and verify the menu items return to the left.
4. Add `ms-auto` back to the class and save.

---

### Styling the navbar with colors

Bootstrap provides color schemes for navbars. The `navbar-light` and `navbar-dark` classes determine text color. Background classes like `bg-light`, `bg-dark`, and `bg-primary` set the navbar background.

**Exercises**

1. Find the `<nav>` tag. Add `navbar-light bg-light` to the class attribute so it reads `class="navbar navbar-expand-lg navbar-light bg-light"`.
2. Reload and verify the navbar has a light gray background with dark text.
3. Change `navbar-light bg-light` to `navbar-dark bg-dark`. Reload and verify the navbar has a dark background with white text.
4. Change the classes to `navbar-dark bg-primary`. Reload and verify the navbar has a blue background.
5. Change back to `navbar-light bg-light` and save.

---

### Adding a responsive toggle

Bootstrap navbar collapse hides menu items behind a toggle button on small screens. The `navbar-toggler` creates the button. The `collapse` class with a target ID controls which elements hide.

**Exercises**

1. In `layouts/_default/baseof.html`, find the navbar. After the navbar-brand link, add a toggle button:
   ```html
   <a class="navbar-brand" href="/">{{ .Site.Title }}</a>
   <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navMenu">
     <span class="navbar-toggler-icon"></span>
   </button>
   ```
2. Find the `<div class="navbar-nav ms-auto">`. Wrap it in a collapsible div:
   ```html
   <div class="collapse navbar-collapse" id="navMenu">
     <div class="navbar-nav ms-auto">
       {{ range .Site.Menus.main }}
       <a class="nav-link" href="{{ .URL }}">{{ .Name }}</a>
       {{ end }}
     </div>
   </div>
   ```
3. Reload the page at full width. Verify the menu items still appear on the right.
4. Resize the browser window to mobile width (or use browser developer tools to simulate mobile).
5. Verify the menu items disappear and a toggle button (three horizontal lines) appears.
6. Click the toggle button and verify the menu items appear below the navbar.
7. Click the toggle button again and verify the menu collapses.

---

### Adding a border to the navbar

Bootstrap border utilities add visual separation. The `border-bottom` class creates a bottom border. Border color can be customized with `border-primary`, `border-dark`, or other color classes.

**Exercises**

1. Find the `<nav>` tag. Add `border-bottom` to the class attribute.
2. Reload and verify a subtle border appears at the bottom of the navbar.
3. Add `border-primary border-3` to the class attribute. Reload and verify a thick blue border appears.
4. Remove `border-primary border-3` and keep only `border-bottom` for a subtle border.

---

## Section 3: Layout with Containers and Grid

Bootstrap containers constrain content width and center it on the page. The grid system divides space into columns for multi-column layouts. Containers and grid work together to create structured page layouts.

### Adding a container to constrain width

Bootstrap container classes wrap content and apply maximum width. The `container` class creates a responsive container that adjusts to screen size. The `container-fluid` class spans the full width.

**Exercises**

1. Open `layouts/_default/baseof.html`. Find the line `{{ block "main" . }}{{ end }}`. Wrap it in a `<main>` tag with container classes:
   ```html
   <main class="container my-5">
     {{ block "main" . }}{{ end }}
   </main>
   ```
2. Reload any page and verify the content has margins on both sides and is centered.
3. Resize the browser window and verify the content width adjusts but stays centered.
4. Find the `<main>` tag. Change `container` to `container-fluid`. Reload and verify the content extends to full width.
5. Change back to `container` and save.

---

### Creating a two-column layout

FILL

---

## Section 4: Components for Portfolio Content

Bootstrap components provide styled patterns for common interface elements. 

### Styling buttons

Bootstrap button classes create styled buttons. The `btn` class provides base button styles. Color variants like `btn-primary`, `btn-success`, and `btn-danger` apply semantic colors. Outline variants like `btn-outline-primary` create bordered buttons.

**Exercises**

1. Open `layouts/projects/single.html`. Find the GitHub link inside the `{{ if .Params.github }}` block. Add `class="btn btn-primary"` to the `<a>` tag.
2. Find the "Back to Projects" link at the bottom. Add `class="btn btn-outline-secondary"` to that `<a>` tag.
3. Navigate to a project page and verify both links appear as styled buttons.
4. Find the GitHub button and change `btn-primary` to `btn-success`. Reload and verify the GitHub button is green.
5. Find the back button and change `btn-outline-secondary` to `btn-secondary`. Reload and verify the back button has a solid gray background.
6. Change back to `btn-primary` and `btn-outline-secondary` and save.

---

### Button sizing

Bootstrap provides size variants for buttons. The `btn-lg` class creates large buttons, while `btn-sm` creates small buttons. Size classes can be combined with color classes.

**Exercises**

1. In `layouts/projects/single.html`, find the GitHub button. Add `btn-lg` to the class attribute.
2. Reload and verify the button appears larger.
3. Find the back button at the bottom. Add `btn-sm` to the class attribute.
4. Reload and verify the back button appears smaller than the GitHub button.

---

### Adding badges for tags

Badges highlight small pieces of information like tags, categories, or status indicators. The `badge` class creates a small labeled element. Background color classes determine the badge appearance.

**Exercises**

1. In `layouts/projects/single.html`, find the `<p>` tag that displays year and status. Replace the entire `<p>` tag with:
   ```html
   <p class="mb-4">
     <span class="badge bg-secondary">{{ .Params.year }}</span>
     <span class="badge bg-success">{{ .Params.status }}</span>
   </p>
   ```
2. Navigate to a project page and verify the year and status appear as small colored badges.
3. Find the status badge and change `bg-success` to `bg-warning`. Reload and verify the status badge is yellow.
4. Add a third badge after the status badge for technology:
   ```html
   <span class="badge bg-info">{{ .Params.tech }}</span>
   ```
5. Reload and verify the technology badge appears.

---