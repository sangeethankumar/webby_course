# Bootstrap Layout and Content Components

Bootstrap provides components for organizing and displaying content in structured ways. Cards create contained sections for projects, publications, or profiles. Containers and grids establish page layout and control how content responds to different screen sizes.

Here we will see:

- how cards display content in structured boxes
- how containers control page width
- how the grid system creates responsive layouts

---

## Section 1: Cards and Content Display

Cards are flexible content containers with multiple options for headers, footers, images, and body content. They provide a consistent way to display related information in distinct sections. Cards help organize portfolio content like projects, publications, or skill categories.

This section covers creating basic cards, adding headers and footers, using card images, creating card groups, and styling card components.

| Bootstrap Class | Description |
|-----------------|-------------|
| `card` | Main card container |
| `card-body` | Main content area of the card |
| `card-title` | Title heading inside card |
| `card-text` | Paragraph text inside card |
| `card-header` | Header section at top of card |
| `card-footer` | Footer section at bottom of card |
| `card-img-top` | Image at top of card |
| `card-group` | Groups multiple cards together |

---

### Creating basic cards

A card requires the `card` class on a div element. Inside the card, `card-body` creates the main content area. Within the card body, `card-title` styles headings and `card-text` styles paragraphs. Cards provide visual separation and structure for content.

Cards work well for displaying individual projects, research papers, or profile sections.

---

**Example** Create a card for a project:

```html
<div class="card">
    <div class="card-body">
        <h3 class="card-title">Machine Learning Project</h3>
        <p class="card-text">A research project investigating neural network applications in genomics.</p>
    </div>
</div>
```

Save and observe the content now appears in a bordered container.

---

**Exercise** Create a second card below the first one for a different project. Save and verify both cards appear with borders and spacing.

---

**Exercise** Add a third paragraph with `class="card-text"` to the first card's body. Save and verify it displays with appropriate styling.

---

**Exercise** Change the heading level from `<h3>` to `<h5>` in one of your cards, save, and observe the title becomes smaller but still maintains card-title styling.

---

### Adding headers and footers to cards

Card headers and footers provide additional sections at the top and bottom of cards. `card-header` creates a distinct header area, often used for categories or labels. `card-footer` creates a footer area, useful for metadata or action buttons.

Headers and footers are placed outside the `card-body` element but inside the main `card` container.

---

**Example** Add a header and footer to a card:

```html
<div class="card">
    <div class="card-header">
        Research Project
    </div>
    <div class="card-body">
        <h3 class="card-title">Machine Learning in Genomics</h3>
        <p class="card-text">Investigating neural network applications.</p>
    </div>
    <div class="card-footer">
        Status: Ongoing
    </div>
</div>
```

Save and observe the header and footer appear with different background styling.

---

**Exercise** Remove the footer, save, and observe the card now has only a header and body.

---

**Exercise** Add the footer back and change the text to show a date like "Completed: January 2025". Save and verify it displays.

---

**Exercise** Create a new card with a header labeled "Publication", a title, description, and a footer showing "Published: 2024". Save and verify all sections appear correctly.

---

### Using images in cards

Cards can include images using `card-img-top`, which displays an image at the top of the card spanning its full width. The image goes outside the `card-body`, placed directly under the opening `card` tag or after a `card-header`.

Images in cards work well for project screenshots, research photos, or visual representations of work.

---

**Example** Add an image to a card:

```html
<div class="card">
    <img src="/images/project1.jpg" class="card-img-top" alt="Project screenshot">
    <div class="card-body">
        <h3 class="card-title">Data Visualization Project</h3>
        <p class="card-text">Interactive visualization of research data.</p>
    </div>
</div>
```

Save and observe the image appears at the top of the card with the content below.

---

**Exercise** Change the image source to a different image from your static folder, save, and verify the new image displays.

---

**Exercise** Add a card footer below the card-body with text like "View Project", save, and verify the image, body, and footer all appear in order.

---

**Exercise** Create a second card with an image, title, description, and footer. Save and verify both image cards display correctly.

---

### Creating card groups

Card groups connect multiple cards together as a single unit with connected borders. The `card-group` class wraps multiple card elements. Cards in a group have equal height and their borders connect, creating a unified appearance.

Card groups work well for displaying related items like a set of projects or publications.

---

**Example** Create a card group with two cards:

```html
<div class="card-group">
    <div class="card">
        <div class="card-body">
            <h3 class="card-title">Project One</h3>
            <p class="card-text">Description of first project.</p>
        </div>
    </div>
    <div class="card">
        <div class="card-body">
            <h3 class="card-title">Project Two</h3>
            <p class="card-text">Description of second project.</p>
        </div>
    </div>
</div>
```

Save and observe the cards connect together with equal heights.

---

**Exercise** Add a third card to the group, save, and verify all three cards connect with equal heights.

---

**Exercise** Add more text to one card's description, save, and observe all cards in the group expand to match the tallest card's height.

---

**Exercise** Add `class="mb-4"` to the `card-group` div to add margin below it, save, and verify spacing appears after the group.

---

### Styling cards with utilities

Bootstrap utility classes can be applied to cards and their components to control colors, spacing, and alignment. Background and text color classes work on `card`, `card-header`, `card-footer`, and `card-body` elements. This allows customization without writing CSS.

Utility classes help create visual hierarchy and draw attention to important cards.

---

**Example** Style a card with utilities:

```html
<div class="card bg-primary text-white mb-3">
    <div class="card-header">Featured Project</div>
    <div class="card-body">
        <h3 class="card-title">Important Research</h3>
        <p class="card-text">This project has significant implications.</p>
    </div>
</div>
```

Save and observe the card has a blue background with white text.

---

**Exercise** Change `bg-primary` to `bg-success`, save, and observe the card background becomes green.

---

**Exercise** Add `class="text-center"` to the card-body div, save, and verify the content centers within the card.

---

**Exercise** Create a new card with `class="card border-danger mb-3"` to give it a red border. Add content inside and save to verify the red border appears.

---

**Exercise** Apply shadow utilities: add `shadow-lg` to a card's class list, save, and verify the card appears elevated with a strong shadow.

---

## Section 2: Containers

Bootstrap containers wrap page content and control its maximum width and horizontal centering. Containers provide the foundation for page layout by ensuring content doesn't stretch too wide on large screens and maintains appropriate margins. Different container types serve different layout needs.

This section covers using fixed-width containers, creating full-width layouts, and applying spacing utilities to containers.

| Bootstrap Class | Description |
|-----------------|-------------|
| `container` | Fixed-width responsive container |
| `container-fluid` | Full-width container |
| `py-`, `px-`, `p-` | Padding utilities for containers |
| `my-`, `mx-`, `m-` | Margin utilities for containers |

---

### Using fixed-width containers

Containers wrap page content and control its maximum width. The `container` class creates a responsive fixed-width container that centers content with appropriate margins. Content inside a container maintains readable line lengths and doesn't stretch across very wide screens.

Containers should wrap the main content of your page but go outside individual sections.

---

**Example** Wrap page content in a container:

```html
<body>
    <div class="container">
        <h1 class="display-1 text-center">Research Portfolio</h1>
        {{ .Content }}
    </div>
</body>
```

Save and observe the content is now centered with margins on the sides.

---

**Exercise** Resize your browser window from wide to narrow and observe how the container maintains appropriate margins at different widths.

---

**Exercise** Add a second container div inside the body for a different section of content, save, and verify both containers center their content with appropriate margins.

---

**Exercise** Remove the container temporarily (keep the content but delete the `<div class="container">` tags), save, and observe how the content stretches to fill the full browser width without margins. Add the container back.

---

### Using full-width containers

The `container-fluid` class creates a container that spans the full width of the viewport with small padding on the sides. This is useful for sections that should stretch across the entire screen, such as hero sections, full-width image galleries, or backgrounds that need to reach the edges.

Full-width containers still provide the benefits of container structure without limiting content width.

---

**Example** Create a full-width container for a hero section:

```html
<div class="container-fluid bg-primary text-white">
    <h1 class="display-1 text-center">Research Portfolio</h1>
    <p class="text-center">Welcome to my work</p>
</div>
```

Save and observe the background color extends to the full width of the browser.

---

**Exercise** Change `container-fluid` back to `container`, save, and observe the colored background no longer reaches the edges.

---

**Exercise** Change back to `container-fluid`, add another `container-fluid` section below with `bg-light` background and different content. Save and verify both full-width sections display correctly.

---

**Exercise** Create a layout with a `container-fluid` for the header and a regular `container` for the main content. Save and observe how the header spans full width while the content is constrained.

---

### Adding spacing to containers

Containers work well with spacing utilities to control internal padding and external margins. Padding utilities like `py-5` add vertical space inside the container, while margin utilities like `my-4` add space outside the container.

Spacing helps separate different sections and improves visual hierarchy.

---

**Example** Add vertical padding to a container:

```html
<div class="container py-5">
    <h1 class="display-1 text-center">Research Portfolio</h1>
    {{ .Content }}
</div>
```

Save and observe comfortable spacing appears at the top and bottom of the container.

---

**Exercise** Change `py-5` to `py-2`, save, and observe less padding inside the container.

---

**Exercise** Add `px-4` along with `py-5`: `class="container py-5 px-4"`, save, and verify extra horizontal padding appears on the sides.

---

**Exercise** Create a `container-fluid` with `class="container-fluid bg-dark text-white py-5 my-4"`, save, and observe how padding and margin utilities work together to create spacing inside and outside the container.

---

## Section 3: Grid System

Bootstrap's grid system divides pages into 12 columns, allowing flexible layouts that respond to screen size. Rows group columns together, and column classes control width and responsive behavior. The grid system creates professional layouts that automatically adapt to different devices.

This section covers creating rows and columns, making responsive layouts, adding spacing between columns, and combining grids with cards.

| Bootstrap Class | Description |
|-----------------|-------------|
| `row` | Creates a grid row |
| `col` | Automatic width column |
| `col-6`, `col-4`, etc. | Column with specific width (out of 12) |
| `col-md-6`, `col-lg-4`, etc. | Responsive column sizes |
| `g-3`, `g-4`, etc. | Gap spacing between columns |

---

### Creating rows and columns

The grid system uses rows and columns to create layouts. A `row` creates a horizontal group, and `col` elements inside it create columns. By default, columns share available space equally. Rows must be inside a container.

The grid divides horizontal space into 12 equal parts. Columns can span multiple parts by specifying numbers like `col-6` (half width) or `col-4` (one third).

---

**Example** Create a two-column layout:

```html
<div class="container">
    <div class="row">
        <div class="col">
            <h2>About Me</h2>
            <p>I am a researcher specializing in computational biology.</p>
        </div>
        <div class="col">
            <h2>Skills</h2>
            <ul>
                <li>Python</li>
                <li>R</li>
                <li>JavaScript</li>
            </ul>
        </div>
    </div>
</div>
```

Save and observe the content appears in two equal-width columns.

---

**Exercise** Add a third `<div class="col">` with content inside the same row, save, and observe the content now splits into three equal columns.

---

**Exercise** Change the first column from `col` to `col-8` and the second from `col` to `col-4`, save, and observe the first column is now twice as wide as the second.

---

**Exercise** Create a new row below with two columns where one uses `col-3` and the other uses `col-9`. Save and verify the second column is three times wider than the first.

---

### Making responsive layouts

Responsive column classes control how layouts change at different screen sizes. Classes like `col-md-6` mean "half width on medium screens and larger, full width on smaller screens". Breakpoint prefixes include `sm` (small), `md` (medium), `lg` (large), and `xl` (extra large).

Responsive classes stack columns vertically on mobile devices while showing them side-by-side on desktops.

---

**Example** Create a responsive two-column layout:

```html
<div class="row">
    <div class="col-md-6">
        <h2>Projects</h2>
        <p>My current research projects.</p>
    </div>
    <div class="col-md-6">
        <h2>Publications</h2>
        <p>Recent published work.</p>
    </div>
</div>
```

Save, resize your browser from wide to narrow, and observe columns stack vertically on narrow screens but sit side-by-side on wider screens.

---

**Exercise** Change `col-md-6` to `col-lg-6` on both columns, save, resize your browser, and observe the columns now stack at a wider breakpoint.

---

**Exercise** Create a three-column layout with `col-md-4` on each column, save, and verify they appear in three columns on medium screens and stack on small screens.

---

**Exercise** Create a layout where columns use `col-12 col-md-6 col-lg-4`. Save, resize your browser to different widths, and observe: full width on small screens, two columns on medium screens, three columns on large screens.

---

### Adding spacing between columns

Gap utilities add spacing between columns in a row. The `g-` prefix with a number adds gutters (spacing) between all columns and rows. `g-3` provides moderate spacing, while `g-5` provides more spacing. These classes go on the `row` element.

Spacing prevents content from appearing cramped when using multiple columns.

---

**Example** Add spacing to a row:

```html
<div class="row g-4">
    <div class="col-md-6">
        <h2>Project One</h2>
        <p>Description here.</p>
    </div>
    <div class="col-md-6">
        <h2>Project Two</h2>
        <p>Description here.</p>
    </div>
</div>
```

Save and observe comfortable spacing appears between the columns.

---

**Exercise** Change `g-4` to `g-2`, save, and observe the spacing decreases.

---

**Exercise** Change `g-2` to `g-5`, save, and observe more spacing appears between columns.

---

**Exercise** Create a row with three columns using `col-md-4` and add `g-3` to the row. Save and verify even spacing appears between all three columns.

---

### Combining grids with cards

Cards work well inside grid columns to create layouts of projects, publications, or other content. Each column can contain a card, and the grid system controls how many cards appear per row at different screen sizes.

This combination creates professional portfolio layouts that respond to screen size.

---

**Example** Create a grid of project cards:

```html
<div class="row g-4">
    <div class="col-md-6 col-lg-4">
        <div class="card h-100">
            <div class="card-body">
                <h3 class="card-title">Project One</h3>
                <p class="card-text">Description of the project.</p>
            </div>
        </div>
    </div>
    <div class="col-md-6 col-lg-4">
        <div class="card h-100">
            <div class="card-body">
                <h3 class="card-title">Project Two</h3>
                <p class="card-text">Description of the project.</p>
            </div>
        </div>
    </div>
    <div class="col-md-6 col-lg-4">
        <div class="card h-100">
            <div class="card-body">
                <h3 class="card-title">Project Three</h3>
                <p class="card-text">Description of the project.</p>
            </div>
        </div>
    </div>
</div>
```

Note: `h-100` makes cards fill the full height of their column.

Save, resize your browser, and observe three columns on large screens, two columns on medium screens, and stacked on small screens.

---

**Exercise** Add a fourth card column with the same classes, save, and verify the grid wraps to create a second row on large screens.

---

**Exercise** Add an image using `card-img-top` to one of the cards, save, and verify the card still aligns properly with others in the grid.

---

**Exercise** Add `class="shadow"` to all cards in your grid, save, and verify all cards display with elevation.

---

**Exercise** Change the responsive classes to `col-sm-6 col-xl-3` on all columns, save, resize your browser, and observe: two columns on small screens, four columns on extra-large screens.

---