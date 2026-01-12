# Enhancing Your Portfolio with Media and Data - SOLUTIONS

Hugo portfolios can display rich content through markdown formatting, static resources, and shortcodes. Markdown provides structure with headings, lists, and links. Static resources include images, documents, and downloadable files. Shortcodes enable advanced features like galleries, video embeds, and collapsible sections.

Here we will see:

- how to organize content with markdown
- how to add and manage static resources
- how to use Hugo shortcodes for rich media

---

## Section 1: Organizing Sections in Markdown

A portfolio needs clear structure to present information effectively. Markdown provides headings to organize content into sections, lists to present items, and links to connect to external resources. These basic formatting tools make the portfolio easier to navigate and understand.

This section covers adding structural elements to organize portfolio content, including headings for sections, lists for presenting information, links for external resources, and anchor links for in-page navigation.

![alt text](s2_s1.gif)

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

**Solution:**
```markdown
## About Me

I am a researcher working on interesting problems in data science and machine learning.

## Skills

My technical expertise includes Python programming, statistical analysis, machine learning, and data visualization. I specialize in developing scalable data pipelines and predictive models.

## Projects

I am currently investigating novel approaches to deep learning for genomic sequence analysis. This work focuses on developing transformer-based models for predicting gene expression patterns.

## Publications

List of my published research papers and conference presentations.
```

---

**Exercise** Add a subsection `### Current Research` under the Projects section with a paragraph about your current work. Save and verify the subsection heading appears smaller than the main section heading.

**Solution:**
```markdown
## Projects

### Current Research

I am currently investigating novel approaches to deep learning for genomic sequence analysis. This work focuses on developing transformer-based models for predicting gene expression patterns.
```

---

**Exercise** Add a `## Contact` section at the end with your contact information. Save and verify the complete page structure with all headings displays correctly.

**Solution:**
```markdown
## Contact

Email: jane.smith@university.edu
Office: Building 42, Room 301
```

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

**Solution:**
```markdown
## Skills

Technical skills include:

1. Python
1. R
1. JavaScript
1. SQL
```

Note: You can use `1.` for all items and Hugo will automatically number them sequentially.

---

**Exercise** Add a new unordered list under the Publications section with three placeholder publication titles. Save and verify the list appears properly formatted.

**Solution:**
```markdown
## Publications

- Machine Learning Methods for Protein Structure Prediction
- Deep Learning for Genomic Sequence Analysis
- Statistical Approaches to Multi-Omics Data Integration
```

---

**Exercise** Under the Projects section, create an ordered list of your three most important projects. Save and verify they display numbered in order.

**Solution:**
```markdown
## Projects

My most significant projects:

1. Genomic Data Analysis Pipeline
2. Protein Structure Prediction Tool
3. Multi-Omics Integration Framework

```

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

**Solution:**
```markdown
Connect with me on [LinkedIn](https://www.linkedin.com/in/yourprofile)
```

---

**Exercise** Add a link to your university or institution homepage in the About Me section. Save and verify the link works correctly.

**Solution:**
```markdown
## About Me

I am a researcher at [Stanford University](https://www.stanford.edu) working on computational biology.
```

---

**Exercise** In the Publications section, add a link labeled "View on Google Scholar" that points to your Google Scholar profile. Save and verify the link opens correctly.

**Solution:**
```markdown
## Publications

[View on Google Scholar](https://scholar.google.com/citations?user=YOURID)
```

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

[About Me](#about-me) | [Projects](#projects)

## About Me

Content here...
```

---


**Exercise** Add Skills, Publications and Contact sections to the Quick Navigation

```markdown
---
title: "Home"
date: 2025-01-10T12:00:00+01:00
draft: false
---

[About Me](#about-me) | [Skills](#skills) | [Projects](#projects) | [Publications](#publications) | [Contact](#contact)

## About Me

Content here...
```

---

**Exercise** Add a "Back to top" link at the end of last section which links to the first section.

**Solution:**
```markdown
## Contact 
...

[Back to top](#about-me)
```
---
**Exercise** Add a "Scroll to bottom" link at the end of last section which links to the first section.

**Solution:**
[Scroll to bottom](#contact)
```markdown
## About Me 
...

```
---

## Section 2: Adding Resources

Hugo serves static files like images and documents from the static directory. These resources are copied directly to the website without modification. Organizing resources into subdirectories makes them easier to find and maintain. Different file types serve different purposes in a research portfolio.

This section covers adding images with descriptive alt text, organizing the static directory structure, linking to different file types, using SVG images, and adding badges.

![Links](s2_s2.gif)

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

**Example** Create the images directory and add a profile photo with descriptive alt text. Then add the image to `content/_index.md`:

```markdown
## About Me

![Researcher examining data visualizations in the laboratory](/images/profile.jpg)

I am a researcher working on data science and machine learning.
```

Save and verify the image displays in the browser.

---

**Exercise** Add a profile photo to `static/images/profile.jpg` with your own descriptive alt text (not just "Profile Photo"). Save and verify the image displays. Right-click the image and select "Inspect" to verify your alt text appears in the HTML `alt` attribute.

**Solution:**
```markdown
## About Me

![Dr. Jane Smith analyzing genomic data at her workstation](/images/profile.jpg)

I am a computational biologist specializing in genomic data analysis.
```

To verify: Right-click the image > Inspect > check the `alt` attribute in the HTML.

---

**Exercise** Add a second image `research.jpg` to the Projects section showing your research or lab. Use descriptive alt text that explains what the image shows. Save, verify it displays, and test by changing the filename to `/images/missing.jpg` to see the alt text appear. Then change it back to the correct filename.

**Solution:**
```markdown
## Projects

![Laboratory equipment setup showing PCR machine and sequencing apparatus](/images/research.jpg)
```

Test with broken link:
```markdown
![Laboratory equipment setup showing PCR machine and sequencing apparatus](/images/missing.jpg)
```

The alt text will display as text. Then change back to `/images/research.jpg`.

---

**Exercise** Add an SVG diagram to `static/images/diagram.svg`. Reference it in the Projects section with descriptive alt text. Save and verify it displays. Resize your browser window from wide to narrow and notice how the SVG scales smoothly without pixelation.

**Solution:**

```markdown
## Projects

![Data processing pipeline diagram](/images/diagram.svg)
```

Open browser developer tools (F12), toggle device toolbar, and test different screen sizes. The SVG should remain sharp at all sizes.

---

### Organizing static files and documents

Subdirectories within static organize different resource types. Images go in one directory, documents in another. Hugo preserves this directory structure when serving files. A file at `static/documents/cv.pdf` becomes available at `/documents/cv.pdf` on the website.

Hugo serves any file type from static without processing. Research portfolios often need PDFs for papers, BibTeX files for citations, CSV files for data, and code files. Each file type serves a specific purpose and should be organized appropriately.

---

**Example** Create a documents directory and add a CV. Then link to it in the Contact section:

```markdown
## Contact

[Download my CV](/documents/cv.pdf)
```

Save and verify clicking the link opens the PDF.

---

**Exercise** Create `static/documents/research-statement.pdf` and add a link in the About Me section with text "Read my research statement". Create `static/data/results.csv` with sample data and link to it from Projects. Save and verify both downloads work.

**Solution:**
```markdown
## About Me

I am a computational biologist specializing in genomic data analysis. [Read my research statement](/documents/research-statement.pdf) for more details about my work.

## Projects

Download the [research dataset](/data/results.csv) used in this analysis.
```

---

**Exercise** Create a BibTeX file at `static/documents/publications.bib` with sample citation data. Link to it in the Publications section with text "Download BibTeX citations". Save and verify the file downloads when clicked.

**Solution:**
Create a file `static/documents/publications.bib` with content:

```bibtex
@article{smith2024ml,
  title={Machine Learning for Genomics},
  author={Smith, Jane and Doe, John},
  journal={Nature},
  year={2024},
  volume={123},
  pages={456--789}
}
```

```markdown
## Publications

[Download BibTeX citations](/documents/publications.bib)
```

---

**Exercise** Create a `static/code/` directory and add a Jupyter notebook `analysis.ipynb` or Python script. Link to it from the Projects section.

**Solution:**

```markdown
## Projects

View the [Jupyter notebook](/code/analysis.ipynb) containing the full analysis pipeline.
```
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

**Solution:**
```markdown
## Projects

### Genomic Analysis Pipeline

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

A comprehensive pipeline for analyzing genomic sequencing data.
```

---

**Exercise** Add a "Published" badge to your most recent publication using: `[![Status](https://img.shields.io/badge/Status-Published-green.svg)](#)`. Save and verify it displays.

**Solution:**
```markdown
## Publications

**Machine Learning for Genomics** (2024)

[![Status](https://img.shields.io/badge/Status-Published-green.svg)](#)
[![DOI](https://img.shields.io/badge/DOI-10.1038%2Fs41586--024--12345-blue)](https://doi.org/10.1038/s41586-024-12345-6)
```

---

**Exercise** Create a custom badge for your research area using shields.io's static badge format: `![Research](https://img.shields.io/badge/Research-Data_Science-blue)`. Add it to your About Me section. Save and verify it appears.

**Solution:**
```markdown
## About Me

![Research](https://img.shields.io/badge/Research-Computational_Biology-blue)
![Focus](https://img.shields.io/badge/Focus-Machine_Learning-green)

I am a computational biologist specializing in applying machine learning to genomic data analysis.
```

---

## Section 3: Hugo Shortcodes

Hugo provides shortcodes for common content patterns. Shortcodes generate HTML from simple parameters without requiring manual HTML. The Beautiful Hugo theme includes additional shortcodes for galleries, columns, and collapsible sections. Shortcodes work directly in markdown files.

This section introduces shortcodes for displaying images with captions, embedding videos and code, creating image galleries, arranging content in columns, and making collapsible sections.

![shortcodes](s2_s3.gif)

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

**Solution:**
```markdown
{{< figure src="/images/profile.jpg" alt="Dr. Jane Smith in the laboratory" caption="Dr. Jane Smith - Computational Biologist" width="300px" >}}
```

---

**Exercise** Change the caption text to something different. Save and verify the new caption appears.

**Solution:**
```markdown
{{< figure src="/images/profile.jpg" alt="Dr. Jane Smith in the laboratory" caption="Principal Investigator, Genomics Lab" width="300px" >}}
```

---

**Exercise** Remove the `width` parameter entirely and save. Verify the image displays at its natural size. Add the width parameter back with a different value like `400px`.

**Solution:**
```markdown
<!-- Without width -->
{{< figure src="/images/profile.jpg" alt="Dr. Jane Smith in the laboratory" caption="Principal Investigator, Genomics Lab" >}}

<!-- Then with different width -->
{{< figure src="/images/profile.jpg" alt="Dr. Jane Smith in the laboratory" caption="Principal Investigator, Genomics Lab" width="400px" >}}
```

---

**Exercise** Add a second figure shortcode in the Projects section using a different image. Include both alt text and a caption describing the research shown. Save and verify both figures display correctly.

**Solution:**
```markdown
## Projects

{{< figure src="/images/research.jpg" alt="Laboratory equipment for genomic sequencing" caption="Next-generation sequencing setup used for DNA analysis" width="350px" >}}
```

---

### Using the youtube shortcode

The youtube shortcode embeds YouTube videos using their video ID. The video ID is the string after `v=` in a YouTube URL. For example, in `https://www.youtube.com/watch?v=dQw4w9WgXcQ`, the ID is `dQw4w9WgXcQ`.

Hugo generates the iframe HTML needed for embedding automatically. The syntax is: `{{< youtube VIDEO_ID >}}`

---

**Exercise** Find a relevant research presentation or talk on YouTube. Copy the video ID from the URL (the part after `v=`). Add the youtube shortcode to your Projects section with the video ID. Save and verify the video embeds and plays within the page.

**Solution:**
```markdown
## Projects

### Conference Presentation

{{< youtube J9IUyzaJo0k >}}

My presentation from the 2024 Computational Biology Conference on machine learning approaches to protein structure prediction.
```

---

**Exercise** Add a second YouTube video to a different section (perhaps a tutorial or conference talk). Save and verify both videos display properly and can be played without opening YouTube in a new tab.

**Solution:**
```markdown
## About Me

### Research Overview

{{< youtube Lto-ajuqW3w >}}

Watch this overview of my research group's work in computational genomics.
```

Click the play button on embedded videos - they should play inline.

---

### (Optional) Using the gist shortcode

The gist shortcode embeds GitHub Gists using the username and gist ID. GitHub Gists are simple code snippet repositories. Each Gist has a unique ID that appears in its URL.

To create a Gist: go to gist.github.com, paste code, add a filename (extension determines syntax highlighting), and click "Create public gist". The URL will be `gist.github.com/username/abc123def456` where `abc123def456` is the gist ID.

The syntax is: `{{< gist USERNAME GIST_ID >}}`

---

**Exercise** Create a GitHub Gist with sample code from your research at gist.github.com. Copy your username and the gist ID from the URL. Add the gist shortcode to your Projects section using both values. Save and verify the code displays with syntax highlighting.

**Solution:**
```markdown
## Projects

### Data Analysis Pipeline

{{< gist janesmith 8f3e9d2c1b4a5678901234567890abcd >}}

This Python script demonstrates our data preprocessing pipeline for genomic sequences.
```

---

**Exercise** Edit your Gist on GitHub (add a comment or modify the code). Reload your portfolio page and verify the updated content appears automatically. Then create a second Gist with different code and embed it in another section. Save and verify both Gists display correctly.

**Solution:**
1. Go to your Gist URL on GitHub
2. Click "Edit"
3. Add a comment like `# Updated on 2025-01-10`
4. Save
5. Reload your portfolio - the changes should appear

Second Gist:
```markdown
## Projects

### Machine Learning Model

{{< gist janesmith 1a2b3c4d5e6f7890abcdef1234567890 >}}

Our transformer-based model for genomic sequence analysis.
```

---

### Using the gallery shortcode

The gallery shortcode displays multiple images in a grid with lightbox functionality. The Beautiful Hugo theme includes PhotoSwipe for viewing images full-screen. The gallery shortcode uses the figure shortcode internally, so it supports captions and alt text.

Gallery images can showcase research photos, lab equipment, conference posters, or project visualizations.

---

**Example** Create a gallery of research images:

```markdown
## Projects

{{< gallery >}}
{{< figure src="/images/stock1.jpg" caption="Initial setup" >}}
{{< /gallery >}}

```

---

**Exercise** Add another image to the gallary.

```markdown
## Projects

{{< gallery >}}
{{< figure src="/images/stock1.jpg" caption="Initial setup" >}}
{{< figure src="/images/stock2.jpg" caption="Processing" >}}
{{< figure src="/images/stock3.jpg" caption="Final Celebration" >}}
{{< /gallery >}}

```

---

### Using the columns shortcode

The columns shortcode creates side-by-side layouts for comparing information. Content in columns appears next to each other on wide screens and stacks vertically on narrow screens. This is useful for before/after comparisons, contrasting methods, or showing related information.

The columns shortcode uses opening `{{< columns >}}` and closing `{{< endcolumn >}}` tags with `{{< column >}}` to separate the columns.

---

**Example** Create a two-column comparison in your Projects section showing two different research methods or approaches. Include a heading and description in each column. Save and verify they appear side by side on wide screens. Resize your browser window to narrow and verify the columns stack vertically.

**Solution:**
```markdown
## Projects

### Comparing Approaches

{{< columns >}}

### Statistical Methods
- Interpretable results
- Requires domain knowledge
- Works with small datasets
- Established theory base

{{< column >}}

### Deep Learning
- High accuracy on complex patterns
- Automated feature learning
- Requires large datasets
- Black box models

{{< endcolumns >}}
```
---

**Exercise** Add images to each column using the figure shortcode. Save and verify the images display properly within the column layout. Create another columns section comparing "Current Work" and "Future Directions" and test that both work correctly.

**Solution:**
```markdown
{{< columns >}}

### Traditional Pipeline
{{< figure src="/images/traditional-pipeline.svg" caption="Statistical analysis workflow" >}}

Uses established statistical methods for data analysis.

{{< column >}}

### ML Pipeline
{{< figure src="/images/ml-pipeline.svg" caption="Machine learning workflow" >}}

Automated feature extraction and pattern recognition.

{{< endcolumns >}}
```

Second columns section:
```markdown
## Projects

### Research Roadmap

{{< columns >}}

### Current Work
- Developing transformer models
- Analyzing 10,000+ sequences
- Collaborating with experimentalists

{{< column >}}

### Future Directions
- Expand to multi-modal data
- Develop interpretability methods
- Clinical applications

{{< endcolumn >}}
```

---