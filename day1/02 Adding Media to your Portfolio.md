# Adding Media to your Portfolio

Hugo portfolios can display rich content through markdown formatting, static resources, and shortcodes. Markdown provides structure with headings, lists, and links. Static resources include images, documents, and downloadable files. Shortcodes enable advanced features like galleries, video embeds, and collapsible sections.

Here we will see:

- how to organize content with markdown
- how to add and manage static resources
- how to use Hugo shortcodes for rich media

---

## Section 1: Organizing Sections in Markdown

A portfolio needs clear structure to present information effectively. Markdown provides headings to organize content into sections, lists to present items, and links to connect to external resources. These basic formatting tools make the portfolio easier to navigate and understand.

This section covers adding structural elements to organize portfolio content, including headings for sections, lists for presenting information, links for external resources, and anchor links for in-page navigation.

| Markdown Syntax | Description |
|-----------------|-------------|
| `## Heading` | Level 2 heading (section title) |
| `### Heading` | Level 3 heading (subsection title) |
| `- Item` | Unordered (bullet) list item |
| `1. Item` | Ordered (numbered) list item |
| `[text](url)` | Link with display text |
| `[text](#anchor)` | Link to heading on same page |

---

### Adding headings to create sections

Headings divide content into logical sections. Level 2 headings (`##`) create main sections like About Me, Projects, and Contact. Level 3 headings (`###`) create subsections within those main sections.

Hugo automatically generates anchor links for headings, which enables in-page navigation. The anchor is created from the heading text with spaces replaced by hyphens and converted to lowercase.

---

**Example** Add a section heading to start organizing the portfolio. In `content/_index.md`, add the About Me section:

```markdown
## About Me

I am a researcher working on interesting problems in data science and machine learning.
```

Save and verify the heading appears on the page.

---

**Exercise** Add three more main section headings: `## Skills`, `## Projects`, and `## Publications`. Add a paragraph of content under each heading. Save and verify all sections appear with proper spacing and hierarchy.

---

**Exercise** Add a subsection `### Current Research` under the Projects section with a paragraph about your current work. Save and verify the subsection heading appears smaller than the main section heading.

---

**Exercise** Add a `## Contact` section at the end with your contact information. Save and verify the complete page structure with all headings displays correctly.

---

### Creating lists for presenting information

Lists present multiple items in an organized way. Unordered lists use hyphens (`-`) for bullet points. Ordered lists use numbers (`1.`) for sequential items. Lists help readers scan information quickly.

Each list item should be on its own line. Blank lines separate lists from other content.

---

**Example** Add an unordered list of programming languages to the Skills section:

```markdown
## Skills

Technical skills include:

- Python
- R
- JavaScript
- SQL
```

---

**Exercise** Convert the programming languages list to an ordered list by replacing the hyphens with `1.` for each item. Save and verify the items now display with numbers.

---

**Exercise** Add a new unordered list under the Publications section with three placeholder publication titles. Save and verify the list appears properly formatted.

---

**Exercise** Under the Projects section, create an ordered list of your three most important projects. Save and verify they display numbered in order.

---

### Adding links to external resources

Links connect portfolio content to external resources. Links use square brackets for display text and parentheses for the URL. The display text should be descriptive and indicate where the link leads.

Links can point to external websites, academic profiles, code repositories, or any other online resource. Email links use `mailto:` before the email address.

---

**Example** Add links to the Contact section:

```markdown
## Contact

Email me at [your.email@example.com](mailto:your.email@example.com)

Find me on [GitHub](https://github.com/yourusername)
```

---

**Exercise** Add a link to your LinkedIn profile in the Contact section. Save and verify clicking the link opens LinkedIn in a new browser tab.

---

**Exercise** Add a link to your university or institution homepage in the About Me section. Save and verify the link works correctly.

---

**Exercise** In the Publications section, add a link labeled "View on Google Scholar" that points to your Google Scholar profile. Save and verify the link opens correctly.

---

### Creating in-page navigation with anchor links

Anchor links allow navigation between sections on the same page. Hugo automatically creates anchors from heading text. The anchor name is the heading text in lowercase with spaces replaced by hyphens.

A table of contents at the top of the page can link to each section, making it easy to jump directly to relevant information.

---

**Example** Add a table of contents at the top of the page that links to each section:

```markdown
---
title: "Home"
date: 2025-01-10T12:00:00+01:00
draft: false
---

**Quick Navigation:** [About Me](#about-me) | [Projects](#projects) | [Publications](#publications) | [Contact](#contact)

## About Me

Content here...
```

---

**Exercise** Add a "Back to top" link at the end of each major section that returns to the navigation menu. The anchor for the top would be `#quick-navigation`. Save and test clicking a back to top link.

---

**Exercise** Add a Skills section to your quick navigation menu. Save and test clicking each navigation link to verify they all jump to the correct sections. If any don't work, check that the anchor name matches the heading text (lowercase, spaces as hyphens).

---

## Section 2: Adding Resources

Hugo serves static files like images and documents from the static directory. These resources are copied directly to the website without modification. Organizing resources into subdirectories makes them easier to find and maintain. Different file types serve different purposes in a research portfolio.

This section covers adding images with descriptive alt text, organizing the static directory structure, linking to different file types, using SVG images, and adding badges.

| Resource Type | Directory | Usage |
|---------------|-----------|-------|
| Images | `static/images/` | Photos, diagrams, figures |
| Documents | `static/documents/` | PDFs, papers, CV |
| Data | `static/data/` | CSV files, datasets |
| Code | `static/code/` | Source files, scripts |

---

### Adding and describing images

The static directory holds files that Hugo copies directly to the website. Images placed in `static/images/` are referenced in markdown as `/images/filename.jpg`. The leading slash tells Hugo to look from the site root.

Markdown image syntax uses square brackets for alt text and parentheses for the file path: `![alt text](/path/to/image.jpg)`. Alt text describes an image for people who cannot see it and displays when an image fails to load. Good alt text describes the image content concisely.

SVG images are vector graphics that scale without losing quality. They work well for diagrams, charts, and technical illustrations. SVG files are referenced exactly like other image formats.

---

**Example** Create the images directory and add a profile photo with descriptive alt text:

```bash
mkdir -p static/images
```

Then add the image to `content/_index.md`:

```markdown
## About Me

![Researcher examining data visualizations in the laboratory](/images/profile.jpg)

I am a researcher working on data science and machine learning.
```

Save and verify the image displays in the browser.

---

**Exercise** Add a profile photo to `static/images/profile.jpg` with your own descriptive alt text (not just "Profile Photo"). Save and verify the image displays. Right-click the image and select "Inspect" to verify your alt text appears in the HTML `alt` attribute.

---

**Exercise** Add a second image `research.jpg` to the Projects section showing your research or lab. Use descriptive alt text that explains what the image shows. Save, verify it displays, and test by changing the filename to `/images/missing.jpg` to see the alt text appear. Then change it back to the correct filename.

---

**Exercise** Add an SVG diagram to `static/images/diagram.svg`. Reference it in the Projects section with descriptive alt text. Save and verify it displays. Resize your browser window from wide to narrow and notice how the SVG scales smoothly without pixelation.

---

### Organizing static files and documents

Subdirectories within static organize different resource types. Images go in one directory, documents in another. Hugo preserves this directory structure when serving files. A file at `static/documents/cv.pdf` becomes available at `/documents/cv.pdf` on the website.

Hugo serves any file type from static without processing. Research portfolios often need PDFs for papers, BibTeX files for citations, CSV files for data, and code files. Each file type serves a specific purpose and should be organized appropriately.

---

**Example** Create a documents directory and add a CV:

```bash
mkdir -p static/documents
```

Then link to it in the Contact section:

```markdown
## Contact

[Download my CV](/documents/cv.pdf)
```

Save and verify clicking the link opens the PDF.

---

**Exercise** Create `static/documents/research-statement.pdf` and add a link in the About Me section with text "Read my research statement". Create `static/data/results.csv` with sample data and link to it from Projects. Save and verify both downloads work.

---

**Exercise** Create a BibTeX file at `static/documents/publications.bib` with sample citation data. Link to it in the Publications section with text "Download BibTeX citations". Save and verify the file downloads when clicked.

---

**Exercise** Create a `static/code/` directory and add a Jupyter notebook `analysis.ipynb` or Python script. Link to it from the Projects section. Save and verify all your downloadable files (CV, research statement, CSV, BibTeX, code) work by clicking each link.

---

### Adding badges and shields

Badges display project information like licenses, build status, DOI links, or version numbers. Badges combine an image and a link, using standard markdown syntax. Many badge services like shields.io generate badges automatically.

Badges are typically placed near project titles or at the top of sections. They provide quick visual information about project status or credentials.

---

**Example** Add a DOI badge to a publication:

```markdown
## Publications

**Machine Learning for Genomics** (2024)

[![DOI](https://img.shields.io/badge/DOI-10.1038%2Fs41586--024--12345-blue)](https://doi.org/10.1038/s41586-024-12345-6)
```

---

**Exercise** Add a license badge to one of your projects using shields.io format: `[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)`. Save and verify the badge displays and links correctly.

---

**Exercise** Add a "Published" badge to your most recent publication using: `[![Status](https://img.shields.io/badge/Status-Published-green.svg)](#)`. Save and verify it displays.

---

**Exercise** Create a custom badge for your research area using shields.io's static badge format: `![Research](https://img.shields.io/badge/Research-Data_Science-blue)`. Add it to your About Me section. Save and verify it appears.

---

## Section 3: Hugo Shortcodes

Hugo provides shortcodes for common content patterns. Shortcodes generate HTML from simple parameters without requiring manual HTML. The Beautiful Hugo theme includes additional shortcodes for galleries, columns, and collapsible sections. Shortcodes work directly in markdown files.

This section introduces shortcodes for displaying images with captions, embedding videos and code, creating image galleries, arranging content in columns, and making collapsible sections.

| Shortcode Syntax | Description |
|------------------|-------------|
| `{{< shortcode >}}` | Self-closing shortcode |
| `{{< shortcode >}}content{{< /shortcode >}}` | Shortcode with content |
| `{{% shortcode %}}` | Shortcode that processes markdown |
| `parameter="value"` | Named parameter in shortcode |

---

### Using the figure shortcode

The figure shortcode creates images with captions, alt text, and sizing attributes. It generates semantic HTML that displays images more professionally than plain markdown. The shortcode accepts parameters like `src`, `alt`, `caption`, and `width`.

Figure shortcodes are useful for research images that need explanatory captions.

---

**Example** Replace a markdown image with the figure shortcode:

```markdown
{{< figure src="/images/profile.jpg" alt="Researcher in laboratory" caption="Dr. Smith conducting analysis" width="300px" >}}
```

---

**Exercise** Replace your profile image markdown with a figure shortcode that includes a caption with your name. Save and verify the image displays with a caption below it.

---

**Exercise** Change the caption text to something different. Save and verify the new caption appears.

---

**Exercise** Remove the `width` parameter entirely and save. Verify the image displays at its natural size. Add the width parameter back with a different value like `400px`.

---

**Exercise** Add a second figure shortcode in the Projects section using a different image. Include both alt text and a caption describing the research shown. Save and verify both figures display correctly.

---

### Using the youtube shortcode

The youtube shortcode embeds YouTube videos using their video ID. The video ID is the string after `v=` in a YouTube URL. For example, in `https://www.youtube.com/watch?v=dQw4w9WgXcQ`, the ID is `dQw4w9WgXcQ`.

Hugo generates the iframe HTML needed for embedding automatically. The syntax is: `{{< youtube VIDEO_ID >}}`

---

**Exercise** Find a relevant research presentation or talk on YouTube. Copy the video ID from the URL (the part after `v=`). Add the youtube shortcode to your Projects section with the video ID. Save and verify the video embeds and plays within the page.

---

**Exercise** Add a second YouTube video to a different section (perhaps a tutorial or conference talk). Save and verify both videos display properly and can be played without opening YouTube in a new tab.

---

### Using the gist shortcode

The gist shortcode embeds GitHub Gists using the username and gist ID. GitHub Gists are simple code snippet repositories. Each Gist has a unique ID that appears in its URL.

To create a Gist: go to gist.github.com, paste code, add a filename (extension determines syntax highlighting), and click "Create public gist". The URL will be `gist.github.com/username/abc123def456` where `abc123def456` is the gist ID.

The syntax is: `{{< gist USERNAME GIST_ID >}}`

---

**Exercise** Create a GitHub Gist with sample code from your research at gist.github.com. Copy your username and the gist ID from the URL. Add the gist shortcode to your Projects section using both values. Save and verify the code displays with syntax highlighting.

---

**Exercise** Edit your Gist on GitHub (add a comment or modify the code). Reload your portfolio page and verify the updated content appears automatically. Then create a second Gist with different code and embed it in another section. Save and verify both Gists display correctly.

---

### Using the gallery shortcode

The gallery shortcode displays multiple images in a grid with lightbox functionality. The Beautiful Hugo theme includes PhotoSwipe for viewing images full-screen. The gallery shortcode uses the figure shortcode internally, so it supports captions and alt text.

Gallery images can showcase research photos, lab equipment, conference posters, or project visualizations.

---

**Example** Create a gallery of research images:

```markdown
## Projects

{{< gallery >}}
{{< figure src="/images/experiment1.jpg" caption="Initial setup" >}}
{{< figure src="/images/experiment2.jpg" caption="Data collection" >}}
{{< figure src="/images/results.jpg" caption="Final results" >}}
{{< /gallery >}}

{{< load-photoswipe >}}
```

Note: The `{{< load-photoswipe >}}` shortcode must be called once per page to enable the lightbox functionality.

---

**Exercise** Add three related images to `static/images/`. Create a gallery in your Projects section with all three images, each with a descriptive caption. Add the `load-photoswipe` shortcode at the bottom of your page. Save and verify the gallery displays as a grid.

---

**Exercise** Click on one of the gallery images and verify it opens in a lightbox overlay. Test the arrow navigation to move between images in the lightbox.

---

**Exercise** Add a second gallery to a different section with different images. Save and verify both galleries work independently with the lightbox.

---

### Using the columns shortcode

The columns shortcode creates side-by-side layouts for comparing information. Content in columns appears next to each other on wide screens and stacks vertically on narrow screens. This is useful for before/after comparisons, contrasting methods, or showing related information.

The columns shortcode uses opening `{{< columns >}}` and closing `{{< endcolumn >}}` tags with `{{< column >}}` to separate the columns.

---

**Exercise** Create a two-column comparison in your Projects section showing two different research methods or approaches. Include a heading and description in each column. Save and verify they appear side by side on wide screens. Resize your browser window to narrow and verify the columns stack vertically.

---

**Exercise** Add images to each column using the figure shortcode. Save and verify the images display properly within the column layout. Create another columns section comparing "Current Work" and "Future Directions" and test that both work correctly.

---

### Using the details shortcode

The details shortcode creates collapsible sections with a clickable title. The content is hidden by default and expands when clicked. This is perfect for publications where you want to show just titles initially, with full details available on demand.

The details shortcode uses `{{% %}}` delimiters (note the percent signs) because it needs to process markdown content inside. The syntax is: `{{% details "Title text" %}}content{{% /details %}}`

---

**Exercise** Add a collapsible publication to your Publications section using the details shortcode. Include the title (with year) in the details parameter and add author information, abstract, DOI link, and PDF download link inside. Save and verify the entry is collapsed by default. Click the title to test expanding and collapsing.

---

**Exercise** Add two more publication entries using the details shortcode. Save and verify all three can be expanded and collapsed independently. Create a collapsible FAQ section in your Contact section with 2-3 questions as separate details blocks. Test expanding/collapsing each one.

---