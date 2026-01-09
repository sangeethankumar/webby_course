# A Single-Page Portfolio (using Beautiful Hugo theme)

Hugo builds websites by reading files from a computer and turning them into web pages. Content is written in Markdown files, extra information is stored in front matter, and themes and configuration files control how the site looks.

Here we will see:

- how Hugo is used locally
- how a single-page homepage is created
- how themes control the appearance of the site

---

## Section 1: Initial Setup

Hugo needs a project structure and a theme before it can display content. Without a theme, Hugo has no templates to turn Markdown files into web pages. This section covers the essential setup steps that must happen before creating any content.

This section covers creating a new Hugo site, learning how the local server works, installing a theme using Hugo Modules, and configuring basic theme settings. By the end of this section, there will be a working site ready to receive content.

### Creating a Hugo site

Hugo is a tool that builds websites from files on a computer. Content is written in simple text files, and Hugo converts them into web pages. 

When creating a new Hugo site, it sets up a folder structure with all the necessary directories. This structure tells Hugo where to find content, themes, and configuration settings.

**Exercises**

1. Use `hugo new site my-portfolio` to create a new site.
2. Navigate into the `my-portfolio` directory.
3. Make sure that the `content` directory exists. This is where we add all our contents
4. Make sure that hugo.toml file exists

---

### Understanding the local server

Hugo includes a web server that runs on a computer. This server lets browsers display the website before publishing it online. The server watches files, and when a change is saved, it automatically rebuilds the site and refreshes the browser.

**Exercises**

1. Start the Hugo server with `hugo server -D`.
2. Open `http://localhost:1313/` in a browser.
3. Notice the message "Page Not Found" appears (this is normal because there is no theme yet).
4. Keep the terminal window open but return to it after the next section.
5. Stop the server with `Ctrl+C` (this can be left running. But sometimes, it might be necessary to restart the server).

---

### Adding a theme using Hugo Modules

A Hugo theme is a collection of templates, stylesheets, and assets that control how a site looks. Without a theme, Hugo cannot display content because it has no templates to render it.

Hugo Modules is the modern way to add themes to a site. Instead of downloading theme files into the project, the theme is declared as a dependency. Hugo then downloads and manages it.

**Exercises**

1. Run `hugo mod init github.com/yourusername/my-portfolio` (replace `yourusername` with any name).
2. Add the Beautiful Hugo theme:
   ```bash
   hugo mod get github.com/halogenica/beautifulhugo
   ```
3. Notice that Hugo created a `go.mod` file in the project root.

---

### Enabling and configuring the theme

After adding a theme, Hugo must be told to use it. With Hugo Modules, the theme is imported in the configuration file using the module import syntax. The configuration file is where Hugo looks for site-wide settings.

Themes come with their own set of configurable options. These options let customization of colors, layouts, features, and behavior without editing theme files directly.

**Exercises**

1. Create a file named `hugo.toml` in the site root (not inside any folder).
2. Add the following content:
   ```toml
   [module]
   [[module.imports]]
   path = "github.com/halogenica/beautifulhugo"
   ```
3. Start the server with `hugo server -D`.
4. Refresh the browser at `http://localhost:1313/`.
5. Notice the page now shows the theme styling (though it is still empty).

---

## Section 2: Creating the Homepage

Now that the site has a working theme, content can be created that will actually display. For a single-page portfolio, only one content file called `_index.md` is needed. This file becomes the homepage.

This section shows how to create the homepage file, configure its front matter, and verify that content appears in the browser. Write a simple introduction for test.

### Creating the homepage file

The file named `_index.md` defines the homepage of the site. Hugo treats this file differently from other content files. For a single-page portfolio, this is the only content file needed.

Hugo provides a command to create content files with the correct front matter automatically. This avoids mistakes that can happen when creating files manually.

**Exercises**

1. With the server still running, open a new terminal window.
2. Navigate to the `my-portfolio` directory in the new terminal.
3. Run `hugo new _index.md` to create the homepage.
4. Open `content/_index.md` in a text editor.
5. Keep both terminal windows open (one for the server, one for commands).

---

### Viewing your first page

With the theme installed and the homepage file created, actual content can now be added that will display in the browser. This confirms that the setup is working correctly.

**Exercises**

1. In `content/_index.md`, below the front matter (after the second `---`), add self-introduction like:
   ```markdown
   # Hello, I'm [Your Name]
   
   I am a researcher working on interesting problems. This is my portfolio website where I share my work and projects. I have been working in the field of data science for several years, focusing on machine learning and statistical analysis.
   ```
2. Save the file and check the browser.
3. Verify that the heading and introduction text appear on the page.
4. Change the text to something different and watch it update automatically.
5. Add another paragraph of text to make the content longer.

---

### Setting up homepage front matter

Front matter is a block of information at the top of the content file. It sits between two lines of three dashes (`---`). Hugo reads this information to understand how to handle the page.

Now that there is content on the page, front matter settings can be modified to control how that content displays.

**Exercises**

1. Open `content/_index.md` and look at the front matter at the top.
2. Change `draft: true` to `draft: false`.
3. Change the `title` to `"Your Name - Portfolio"` (this appears in the browser tab).
4. The front matter should now look like:
   ```yaml
   ---
   title: "Your Name - Portfolio"
   draft: false
   ---
   ```
5. Save the file and verify the change in the browser tab title.

---

## Section 3: Building Your Portfolio Content

The site is now working and displaying content. This section focuses on structuring the portfolio effectively. This includes learning how to organize information using headings, create subsections for complex topics, and link to external resources.

A well-structured single-page portfolio uses headings to divide content into logical sections. This makes it easy for readers to scan the page and find the information they need.

### Creating the main sections

A single-page portfolio organizes all information on one page. Instead of clicking links to visit different pages, readers scroll down to see different sections.

Markdown headings divide content into logical sections. Each heading creates a visual break and helps readers understand what information comes next. Headings also create anchor points that navigation menus can link to.

**Exercises**

1. In `content/_index.md`, replace the simple introduction with:
   ```markdown
   # Hello, I'm [Your Name]
   
   Brief introduction paragraph about yourself.
   
   ## About Me
   
   Write 2-3 sentences about your background.
   
   ## Skills
   
   ## Projects
   
   ## Publications
   
   ## Contact
   ```
2. Add 2-3 sentences under each section heading.
3. Save and view the page at `http://localhost:1313/`.
4. Notice how headings create visual sections.
5. Try scrolling through the page to see the structure.

---

### Organizing subsections

Some portfolio sections contain multiple types of information. For example, a Skills section might include programming languages, frameworks, and tools. Using subsections (smaller headings) helps break down complex information into digestible pieces.

Subsections create hierarchy. They show which information belongs together and how different pieces relate to each other.

**Exercises**

1. Under `## Skills`, add:
   ```markdown
   ### Programming Languages
   Python, R, JavaScript
   
   ### Frameworks
   Hugo, React, TensorFlow
   
   ### Tools
   Git, Docker, LaTeX
   ```
2. Add a `## Experience` section with:
   - `### Current Position`
   - `### Previous Positions`
3. Write one sentence under each experience subsection.
4. Add a `## Education` section with subsections for each degree.
5. View how the hierarchy appears on the page.

---

### Linking to external resources

A portfolio should point to work without duplicating it. Instead of copying entire research papers or project documentation into the portfolio, link to where they already exist online.

Markdown makes linking simple. The link text goes in square brackets followed by the URL in parentheses.

**Exercises**

1. In the `## Projects` section, add:
   ```markdown
   ### Project Title
   Brief description of the project.
   [View on GitHub](https://github.com/username/repo) | [Live Demo](https://demo.com)
   ```
2. Replace the URLs with real links (or leave as placeholders).
3. In `## Publications`, add 3 papers with DOI or arXiv links:
   ```markdown
   - **Paper Title*- (2024) - Journal Name  
     [DOI Link](https://doi.org/10.xxx/xxx)
   ```
4. In `## Contact`, add:
   ```markdown
   - Email: [your.email@example.com](mailto:your.email@example.com)
   - GitHub: [github.com/username](https://github.com/username)
   - LinkedIn: [linkedin.com/in/username](https://linkedin.com/in/username)
   ```
5. Click the links to verify they work correctly.

---

## Section 4: Customizing Your Portfolio

The portfolio now has content and structure. This section covers customization options that make the portfolio more professional and easier to navigate. This includes configuring profile information, creating navigation that scrolls to different sections, and exploring alternative themes.

Theme configuration lets adaptation of the appearance and functionality to match needs without editing code or templates.

### Configuring the theme appearance

Beautiful Hugo theme provides configuration options to customize how the site looks and behaves. These settings are added to the `hugo.toml` file under a `[params]` section. Settings will be added one at a time to see how each one affects the site.

**Exercises**

1. Open `hugo.toml` and add a `[params]` section at the end with one setting:
   ```toml
   [params]
   subtitle = "Researcher and Data Scientist"
   ```
2. Restart the server with `hugo server -D` and notice the subtitle appears below the site title.
3. Change the subtitle text to something different. Restart and verify the change appears.
4. Add a second parameter below `subtitle`:
   ```toml
   favicon = "/images/favicon.ico"
   ```
5. Add a small favicon image to `static/images/favicon.ico`, restart the server, and verify it appears in the browser tab.

**Note about theme configuration:**

Each Hugo theme has its own unique configuration structure and options. Always refer to the theme documentation for specific configuration options. For Beautiful Hugo, see: https://github.com/halogenica/beautifulhugo

---

### Creating in-page navigation

On a multi-page site, navigation links take visitors to different pages. On a single-page portfolio, navigation links scroll to different sections of the same page. These are called anchor links.

An anchor link uses the section heading text to create a target. If there is a heading `## Projects`, it can be linked to with `#projects`. The browser then scrolls to that section when the link is clicked.

**Exercises**

1. In `hugo.toml`, add one menu item above the `[module]` section:
   ```toml
   [[menu.main]]
   name = "About"
   url = "#about-me"
   weight = 1
   ```
2. Look for the navigation menu in the site header and click "About" to see it scroll to that section.
3. Add a second menu item below the first:
   ```toml
   [[menu.main]]
   name = "Skills"
   url = "#skills"
   weight = 2
   ```
4. Add two more menu items for Projects and Contact:
   ```toml
   [[menu.main]]
   name = "Projects"
   url = "#projects"
   weight = 3
   
   [[menu.main]]
   name = "Contact"
   url = "#contact"
   weight = 4
   ```
5. Add a "Scroll to Bottom" link near the top of the content in `_index.md` (after the introduction paragraph):
   ```markdown
   [↓ Scroll to Bottom](#contact)
   ```
6. Save and click it to verify it jumps to the Contact section at the bottom.
7.  Add a "Back to Top" link at the end of the Contact section in `_index.md`:
   ```markdown
   [↑ Back to Top](#)
   ```
8.  Save, scroll down, and click it to jump back to the top.

---

**Exploring other themes:**

Hugo has hundreds of themes available with different designs and features. Each theme has its own configuration structure and options, so the documentation for any theme chosen will need to be read.

Browse available themes at https://themes.gohugo.io/. When finding a theme, follow its installation instructions and refer to its documentation for configuration options.

---