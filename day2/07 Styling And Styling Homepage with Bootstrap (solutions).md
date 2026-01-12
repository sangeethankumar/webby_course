# Styling with Bootstrap - SOLUTIONS

Bootstrap is a CSS framework that provides pre-built styles for common HTML elements. Instead of writing CSS from scratch, Bootstrap classes can be added directly to HTML tags to style them. This makes it quick to create professional-looking pages without deep CSS knowledge.

Here we will see:

- how to add Bootstrap to a Hugo site
- how Bootstrap classes style text and typography
- how to use color, background, and spacing utilities
- how buttons and utility classes work

---

## Setup: Adding Bootstrap to Hugo

Bootstrap is loaded through a Content Delivery Network (CDN), which means the styles are hosted online and referenced in the HTML. The `<link>` tag in the `<head>` section tells the browser to load Bootstrap's stylesheet.

Hugo sites with custom layouts can add Bootstrap by including the CDN links in the layout file. This makes Bootstrap available for all HTML elements on the page.

| Bootstrap Concept | Description |
|-------------------|-------------|
| CDN | Content Delivery Network - hosts files online |
| `<link>` tag | HTML tag that loads external stylesheets |
| Bootstrap class | Pre-made style applied by adding to `class=""` |
| Utility class | Single-purpose class like `text-center` |

---

### Adding Bootstrap CDN links

The Bootstrap CDN provides the framework's CSS through a `<link>` tag. This tag goes in the `<head>` section of the HTML layout file. Once added, Bootstrap classes become available to use on any HTML element.

The `<link>` tag has two attributes: `href` points to Bootstrap's CSS file, and `rel="stylesheet"` tells the browser this is a stylesheet.

---

**Example** Open `layouts/index.html` and add Bootstrap's CSS link to the `<head>` section:

```html
<!DOCTYPE html>
<html>
<head>
    <title>My Portfolio</title>
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/css/bootstrap.min.css" rel="stylesheet">
</head>
<body>
    <h1>Research Portfolio</h1>
    {{ .Content }}
</body>
</html>
```

Save the file and refresh the browser. The page will look slightly different as Bootstrap's default styles are now applied.

---

**Exercise** Look at the heading in your browser and notice it now has a different font than before. This confirms Bootstrap is loaded.

**Solution:**
The heading should now display in Bootstrap's default font stack (system fonts) instead of the browser's default serif font. The spacing around the heading may also have changed.

---

**Exercise** Open browser DevTools (F12), go to the Network tab, refresh the page, and verify that `bootstrap.min.css` appears in the list of loaded files.

**Solution:**
In the Network tab, you should see a file named `bootstrap.min.css` loaded from `cdn.jsdelivr.net`. The file size should be around 200-300KB.

---

### Adding the viewport meta tag

The viewport meta tag tells mobile browsers how to scale the page. Bootstrap requires this tag to display correctly on mobile devices. Without it, pages may appear zoomed out or improperly sized on phones and tablets.

The viewport tag goes in the `<head>` section alongside other meta information.

---

**Example** Add the viewport meta tag to `layouts/index.html`:

```html
<head>
    <title>My Portfolio</title>
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/css/bootstrap.min.css" rel="stylesheet">
</head>
```

Save the file. The page appearance won't change on desktop, but this ensures proper display on mobile devices.

---

**Exercise** Resize your browser window to a narrow width (like a phone screen) and verify the page content adjusts appropriately.

**Solution:**
When you resize the browser window to a narrow width (300-400px), the content should remain readable and not require horizontal scrolling. Text should wrap appropriately.

---

**Exercise** Open DevTools, toggle device toolbar (Ctrl+Shift+M), and select a mobile device. Verify the page displays at an appropriate size for the screen.

**Solution:**
With device toolbar enabled and a mobile device selected (e.g., iPhone 12), the page should display at the device's width without appearing zoomed out. The content should be readable without pinch-to-zoom.

---

## Section 1: Typography and Text Styling

Bootstrap provides classes that control how text appears. These classes change text size, weight, alignment, and transform. Typography classes make content easier to read and help establish visual hierarchy.

This section covers styling headings, adjusting text size, controlling alignment, transforming case, and using display headings for emphasis.

| Bootstrap Class | Description |
|-----------------|-------------|
| `display-1` through `display-6` | Extra large heading styles |
| `fs-1` through `fs-6` | Font size utilities (1 largest, 6 smallest) |
| `fw-bold`, `fw-normal`, `fw-light` | Font weight utilities |
| `text-center`, `text-start`, `text-end` | Text alignment |
| `text-uppercase`, `text-lowercase`, `text-capitalize` | Text transform |

---

### Styling headings with display classes

Display classes create large, impactful headings that stand out from regular headings. They use `display-1` (largest) through `display-6` (smallest). Display headings are typically used for page titles or major section headers.

Display classes are added to heading tags like `<h1>` or `<h2>` using the `class` attribute.

---

**Example** Add a display class to the main heading:

```html
<h1 class="display-1">Research Portfolio</h1>
```

Save and observe the heading is now much larger and more prominent.

---

**Exercise** Change `display-1` to `display-4`, save, and observe the heading becomes smaller but still larger than a regular h1.

**Solution:**
```html
<h1 class="display-4">Research Portfolio</h1>
```

---

**Exercise** Add `class="display-2"` to one of your section headings (like `<h2>Skills</h2>`), save, and verify it becomes larger and more prominent.

**Solution:**
```html
<h2 class="display-2">Skills</h2>
```

---

**Exercise** Change `display-2` to `display-6`, save, and observe how the size changes. Try values between 1 and 6 to see the range of sizes available.

**Solution:**
```html
<h2 class="display-6">Skills</h2>
```
Then try `display-1`, `display-3`, `display-5` to see the range.

---

### Controlling text size with font size utilities

Font size utilities use `fs-1` through `fs-6` to adjust text size. These work on any text element, not just headings. Font size 1 is largest, font size 6 is smallest. This provides finer control than display classes.

Font size utilities are useful for emphasizing specific paragraphs or adjusting list item sizes.

---

**Example** Add font size to a paragraph:

```html
<p class="fs-3">Welcome to my research portfolio.</p>
```

Save and observe the paragraph is larger than normal paragraphs.

---

**Exercise** Change `fs-3` to `fs-5`, save, and observe the paragraph becomes smaller.

**Solution:**
```html
<p class="fs-5">Welcome to my research portfolio.</p>
```

---

**Exercise** Add `class="fs-4"` to a different paragraph in your layout, save, and compare it to other paragraphs to see the size difference.

**Solution:**
```html
<p class="fs-4">I am a researcher specializing in computational biology.</p>
```

---

**Exercise** Add `class="fs-6"` to your footer paragraph, save, and verify it displays smaller than regular text.

**Solution:**
```html
<p class="fs-6">Last updated: January 2025</p>
```

---

### Adjusting font weight

Font weight classes control how bold or light text appears. `fw-bold` makes text bold, `fw-normal` uses regular weight, and `fw-light` makes text thinner. Font weight helps establish visual hierarchy and emphasis.

Weight classes can be applied to any text element including headings, paragraphs, and list items.

---

**Example** Make a paragraph bold:

```html
<p class="fw-bold">I specialize in computational biology and machine learning.</p>
```

Save and observe the paragraph text is now bold.

---

**Exercise** Change `fw-bold` to `fw-light`, save, and observe the text becomes thinner.

**Solution:**
```html
<p class="fw-light">I specialize in computational biology and machine learning.</p>
```

---

**Exercise** Add `class="fw-bold"` to a list item in your Skills section, save, and verify it appears bolder than other list items.

**Solution:**
```html
<li class="fw-bold">Python</li>
```

---

**Exercise** Combine font size and weight: add `class="fs-4 fw-bold"` to a paragraph, save, and verify it is both larger and bold.

**Solution:**
```html
<p class="fs-4 fw-bold">I specialize in computational biology and machine learning.</p>
```

---

### Aligning text

Text alignment classes position text horizontally. `text-center` centers text, `text-start` aligns to the left (default in English), and `text-end` aligns to the right. Alignment helps organize page layouts and draw attention to specific content.

Text alignment applies to the entire element and all text within it.

---

**Example** Center the main heading:

```html
<h1 class="display-1 text-center">Research Portfolio</h1>
```

Save and observe the heading is now centered.

---

**Exercise** Change `text-center` to `text-end`, save, and observe the heading moves to the right side.

**Solution:**
```html
<h1 class="display-1 text-end">Research Portfolio</h1>
```

---

**Exercise** Change it back to `text-center`, save, and verify it returns to center.

**Solution:**
```html
<h1 class="display-1 text-center">Research Portfolio</h1>
```

---

**Exercise** Add `class="text-center"` to a paragraph, save, and verify the paragraph text is centered.

**Solution:**
```html
<p class="text-center">Welcome to my research portfolio.</p>
```

---

### Transforming text case

Text transform classes change capitalization. `text-uppercase` makes all letters uppercase, `text-lowercase` makes all lowercase, and `text-capitalize` capitalizes the first letter of each word. These transformations happen through CSS without changing the actual HTML content.

Text transform is useful for styling headings, buttons, or labels consistently.

---

**Example** Make a heading uppercase:

```html
<h2 class="text-uppercase">About Me</h2>
```

Save and observe the heading displays in all caps even though the HTML has mixed case.

---

**Exercise** Change `text-uppercase` to `text-lowercase`, save, and observe all letters become lowercase.

**Solution:**
```html
<h2 class="text-lowercase">About Me</h2>
```
This will display as "about me".

---

**Exercise** Change it to `text-capitalize`, save, and observe each word's first letter becomes capitalized.

**Solution:**
```html
<h2 class="text-capitalize">About Me</h2>
```
This will display as "About Me" (each word capitalized).

---

**Exercise** Add `class="text-uppercase"` to a paragraph, save, and verify the entire paragraph appears in uppercase.

**Solution:**
```html
<p class="text-uppercase">I am a researcher specializing in computational biology.</p>
```

---

## Section 2: Colors, Backgrounds, and Spacing

Bootstrap provides utility classes for colors, backgrounds, and spacing. These utilities let you quickly add visual polish without writing custom CSS. Color and background classes use Bootstrap's color system, while spacing utilities control margins and padding.

This section covers applying text colors, adding background colors, controlling margins, adjusting padding, and combining utilities.

| Bootstrap Class | Description |
|-----------------|-------------|
| `text-primary`, `text-secondary`, etc. | Text color utilities |
| `bg-primary`, `bg-secondary`, etc. | Background color utilities |
| `m-1` through `m-5` | Margin utilities (1 smallest, 5 largest) |
| `mt-`, `mb-`, `ms-`, `me-` | Margin top, bottom, start (left), end (right) |
| `p-1` through `p-5` | Padding utilities (1 smallest, 5 largest) |
| `pt-`, `pb-`, `ps-`, `pe-` | Padding top, bottom, start (left), end (right) |

---

### Adding text colors

Bootstrap's text color classes follow a semantic naming system. `text-primary` uses the primary theme color (typically blue), `text-secondary` uses gray, `text-success` uses green, `text-danger` uses red, and so on. These colors provide meaning and visual consistency.

Text color classes can be applied to any text element.

---

**Example** Add color to a heading:

```html
<h2 class="text-primary">Skills</h2>
```

Save and observe the heading is now blue (or your theme's primary color).

---

**Exercise** Change `text-primary` to `text-success`, save, and observe the heading becomes green.

**Solution:**
```html
<h2 class="text-success">Skills</h2>
```

---

**Exercise** Add `class="text-secondary"` to a paragraph, save, and verify it displays in gray.

**Solution:**
```html
<p class="text-secondary">Welcome to my research portfolio.</p>
```

---

**Exercise** Try different colors: add `text-danger` to one element, `text-warning` to another, and `text-info` to a third. Save and observe the different colors.

**Solution:**
```html
<p class="text-danger">This text is red.</p>
<p class="text-warning">This text is yellow/orange.</p>
<p class="text-info">This text is light blue.</p>
```

---

### Adding background colors

Background color classes use the same color system as text colors but apply to the element's background. Common classes include `bg-primary`, `bg-light`, `bg-dark`, and others. Background colors work best on elements with padding to prevent text from touching edges.

Background colors cover the entire element area.

---

**Example** Add a background color to a section:

```html
<div class="bg-light p-3">
    <h2>About Me</h2>
    <p>I am a researcher specializing in computational biology.</p>
</div>
```

Save and observe the section has a light gray background with padding.

---

**Exercise** Change `bg-light` to `bg-primary`, save, and observe the background becomes blue. Note that you may need to add `text-white` to make the text readable on the dark background.

**Solution:**
```html
<div class="bg-primary text-white p-3">
    <h2>About Me</h2>
    <p>I am a researcher specializing in computational biology.</p>
</div>
```

---

**Exercise** Add `class="bg-warning"` to a different div, save, and verify it has a yellow background.

**Solution:**
```html
<div class="bg-warning p-3">
    <h2>Projects</h2>
    <p>Here are my current projects.</p>
</div>
```

---

**Exercise** Create a new div around your contact section with `class="bg-dark text-white p-3"`, save, and verify it has a dark background with white text.

**Solution:**
```html
<div class="bg-dark text-white p-3">
    <h2>Contact</h2>
    <p>Email: name@example.com</p>
</div>
```

---

### Adding margins

Margin utilities add space outside an element. `m-1` through `m-5` add margin on all sides, with higher numbers creating more space. Directional margins like `mt-3` (margin-top) or `mb-4` (margin-bottom) add space on specific sides only.

Margins create separation between elements and improve readability.

---

**Example** Add margin above a heading:

```html
<h2 class="mt-5">Projects</h2>
```

Save and observe more space appears above the heading.

---

**Exercise** Change `mt-5` to `mt-2`, save, and observe less space above the heading.

**Solution:**
```html
<h2 class="mt-2">Projects</h2>
```

---

**Exercise** Add `class="mb-4"` (margin-bottom) to a paragraph, save, and verify more space appears below it.

**Solution:**
```html
<p class="mb-4">I am a researcher specializing in computational biology.</p>
```

---

**Exercise** Add `class="m-3"` (margin all sides) to a div, save, and observe space appears around all sides of the element.

**Solution:**
```html
<div class="m-3 bg-light p-3">
    <h2>About Me</h2>
    <p>Content here.</p>
</div>
```

---

### Adding padding

Padding utilities add space inside an element, between its border and content. Like margins, padding uses `p-1` through `p-5` for all sides, or directional classes like `pt-3` (padding-top) for specific sides.

Padding is essential when using background colors to prevent text from touching edges.

---

**Example** Add padding to a section with a background:

```html
<div class="bg-light p-4">
    <h2>Contact</h2>
    <p>Email: name@example.com</p>
</div>
```

Save and observe the text has comfortable space from the edges of the colored background.

---

**Exercise** Change `p-4` to `p-1`, save, and observe the space inside becomes smaller.

**Solution:**
```html
<div class="bg-light p-1">
    <h2>Contact</h2>
    <p>Email: name@example.com</p>
</div>
```

---

**Exercise** Change `p-1` to `p-5`, save, and observe more space inside the element.

**Solution:**
```html
<div class="bg-light p-5">
    <h2>Contact</h2>
    <p>Email: name@example.com</p>
</div>
```

---

**Exercise** Add `class="py-3"` (padding top and bottom only) to a paragraph, save, and verify vertical space appears but not horizontal.

**Solution:**
```html
<p class="py-3">I am a researcher specializing in computational biology.</p>
```

---

### Combining color and spacing utilities

Multiple Bootstrap classes can be used together on the same element. Classes are separated by spaces in the `class` attribute. This allows complex styling by combining colors, backgrounds, spacing, and typography.

Combining utilities reduces the need for custom CSS.

---

**Example** Create a styled callout section:

```html
<div class="bg-primary text-white p-4 mb-4">
    <h3 class="text-center">Current Research</h3>
    <p class="fs-5">I'm currently investigating machine learning applications in genomics.</p>
</div>
```

Save and observe the combined effect of background color, text color, padding, margin, text centering, and font size.

---

**Exercise** Add `class="bg-success text-white p-3 mt-5 mb-3"` to a div containing one of your sections, save, and verify all the utilities apply correctly.

**Solution:**
```html
<div class="bg-success text-white p-3 mt-5 mb-3">
    <h2>Skills</h2>
    <p>My technical skills include Python, R, and JavaScript.</p>
</div>
```

---

**Exercise** Create a new div around your About Me section with `class="bg-light p-4 mb-4"` and add `class="text-center text-primary"` to the heading inside. Save and verify the styling.

**Solution:**
```html
<div class="bg-light p-4 mb-4">
    <h2 class="text-center text-primary">About Me</h2>
    <p>I am a researcher specializing in computational biology.</p>
</div>
```

---

**Exercise** Experiment by combining different utilities: try `bg-warning text-dark p-5 mt-4` on an element, save, and observe how all the utilities work together.

**Solution:**
```html
<div class="bg-warning text-dark p-5 mt-4">
    <h2>Projects</h2>
    <p>Check out my recent projects.</p>
</div>
```

---

## Section 3: Buttons and Utilities

Bootstrap provides button styles and additional utility classes that enhance functionality and appearance. Button classes make links and buttons look professional and interactive. Utility classes handle common needs like rounding corners, adding shadows, and controlling display.

This section covers styling links as buttons, using button variants, adjusting button sizes, adding border radius, and using shadow utilities.

| Bootstrap Class | Description |
|-----------------|-------------|
| `btn` | Base button class (required for all buttons) |
| `btn-primary`, `btn-secondary`, etc. | Button color variants |
| `btn-lg`, `btn-sm` | Button size modifiers |
| `rounded`, `rounded-circle`, `rounded-pill` | Border radius utilities |
| `shadow`, `shadow-sm`, `shadow-lg` | Shadow utilities |

---

### Creating buttons from links

The `btn` class transforms links into styled buttons. Bootstrap buttons require two classes: `btn` (base styling) and a color variant like `btn-primary`. These classes make links look like clickable buttons instead of underlined text.

Links styled as buttons remain functional hyperlinks but appear more prominent.

---

**Example** Convert a link to a button:

```html
<a href="mailto:name@example.com" class="btn btn-primary">Contact Me</a>
```

Save and observe the link now appears as a blue button.

---

**Exercise** Change `btn-primary` to `btn-success`, save, and observe the button becomes green.

**Solution:**
```html
<a href="mailto:name@example.com" class="btn btn-success">Contact Me</a>
```

---

**Exercise** Add `class="btn btn-secondary"` to a different link in your Contact section, save, and verify it displays as a gray button.

**Solution:**
```html
<a href="https://linkedin.com/in/profile" class="btn btn-secondary">LinkedIn</a>
```

---

**Exercise** Try different button variants: add `btn-warning`, `btn-danger`, and `btn-info` to three different links. Save and observe the different colors.

**Solution:**
```html
<a href="#" class="btn btn-warning">Warning Button</a>
<a href="#" class="btn btn-danger">Danger Button</a>
<a href="#" class="btn btn-info">Info Button</a>
```

---

### Using button outline variants

Outline buttons have a colored border and text but transparent background. They use classes like `btn-outline-primary` instead of `btn-primary`. Outline buttons provide a lighter visual appearance while maintaining the button structure.

Outline buttons are useful for secondary actions or when you want less visual weight.

---

**Example** Create an outline button:

```html
<a href="https://github.com/yourusername" class="btn btn-outline-primary">View GitHub</a>
```

Save and observe the button has a blue border and blue text but no background color.

---

**Exercise** Change `btn-outline-primary` to `btn-outline-success`, save, and observe the border and text become green.

**Solution:**
```html
<a href="https://github.com/yourusername" class="btn btn-outline-success">View GitHub</a>
```

---

**Exercise** Add both a solid button and an outline button next to each other: `<a class="btn btn-primary">Primary</a> <a class="btn btn-outline-primary">Outline</a>`. Save and compare their appearance.

**Solution:**
```html
<a href="#" class="btn btn-primary">Primary</a>
<a href="#" class="btn btn-outline-primary">Outline</a>
```

---

**Exercise** Create an outline danger button with `class="btn btn-outline-danger"` for a link, save, and verify it has a red border with red text.

**Solution:**
```html
<a href="#" class="btn btn-outline-danger">Delete</a>
```

---

### Adjusting button sizes

Button size modifiers make buttons larger or smaller. `btn-lg` creates large buttons, `btn-sm` creates small buttons, and buttons without size modifiers use the default medium size.

Button sizes help establish visual hierarchy and match buttons to their context.

---

**Example** Create a large button:

```html
<a href="#" class="btn btn-primary btn-lg">Get Started</a>
```

Save and observe the button is larger than default buttons.

---

**Exercise** Change `btn-lg` to `btn-sm`, save, and observe the button becomes smaller.

**Solution:**
```html
<a href="#" class="btn btn-primary btn-sm">Get Started</a>
```

---

**Exercise** Add three buttons with different sizes next to each other: one with `btn-lg`, one with no size modifier, and one with `btn-sm`. Save and compare their sizes.

**Solution:**
```html
<a href="#" class="btn btn-primary btn-lg">Large</a>
<a href="#" class="btn btn-primary">Default</a>
<a href="#" class="btn btn-primary btn-sm">Small</a>
```

---

**Exercise** Make your "Contact Me" button large by adding `btn-lg` to its classes, save, and verify it stands out more prominently.

**Solution:**
```html
<a href="mailto:name@example.com" class="btn btn-primary btn-lg">Contact Me</a>
```

---

### Adding rounded corners

Border radius utilities control how rounded element corners appear. `rounded` adds moderate rounding, `rounded-pill` creates pill-shaped elements with fully rounded ends, and `rounded-circle` creates perfect circles (requires equal width and height).

Rounding can apply to any element, not just buttons.

---

**Example** Make a button pill-shaped:

```html
<a href="#" class="btn btn-primary rounded-pill">Contact Me</a>
```

Save and observe the button has fully rounded ends.

---

**Exercise** Remove `rounded-pill` so the button has default Bootstrap rounding, save, and observe the corners are only slightly rounded.

**Solution:**
```html
<a href="#" class="btn btn-primary">Contact Me</a>
```

---

**Exercise** Add `class="rounded"` to a div with background color, save, and verify the div corners become rounded.

**Solution:**
```html
<div class="bg-light p-4 rounded">
    <h2>About Me</h2>
    <p>Content here.</p>
</div>
```

---

**Exercise** Add `class="rounded-circle"` to a small div (you'll need to set equal width and height in inline style like `style="width: 100px; height: 100px;"` to see the circle effect). Save and observe it becomes circular.

**Solution:**
```html
<div class="bg-primary rounded-circle" style="width: 100px; height: 100px;"></div>
```

---

### Adding shadows

Shadow utilities add depth to elements. `shadow-sm` creates a subtle shadow, `shadow` creates a medium shadow, and `shadow-lg` creates a prominent shadow. Shadows make elements appear to float above the page.

Shadows work well on cards, buttons, or important sections.

---

**Example** Add a shadow to a section:

```html
<div class="bg-light p-4 shadow">
    <h2>Featured Project</h2>
    <p>Description of the project.</p>
</div>
```

Save and observe the section appears to lift off the page.

---

**Exercise** Change `shadow` to `shadow-lg`, save, and observe the shadow becomes more pronounced.

**Solution:**
```html
<div class="bg-light p-4 shadow-lg">
    <h2>Featured Project</h2>
    <p>Description of the project.</p>
</div>
```

---

**Exercise** Change `shadow-lg` to `shadow-sm`, save, and observe the shadow becomes more subtle.

**Solution:**
```html
<div class="bg-light p-4 shadow-sm">
    <h2>Featured Project</h2>
    <p>Description of the project.</p>
</div>
```

---

**Exercise** Add shadows to your buttons by including `shadow` in their class list: `class="btn btn-primary shadow"`. Save and verify the buttons have more depth.

**Solution:**
```html
<a href="mailto:name@example.com" class="btn btn-primary shadow">Contact Me</a>
```

---

**Exercise** Create a section with multiple utilities combined: `class="bg-primary text-white p-4 mb-4 rounded shadow-lg"`. Save and observe how all the utilities work together to create a polished appearance.

**Solution:**
```html
<div class="bg-primary text-white p-4 mb-4 rounded shadow-lg">
    <h2>Current Research</h2>
    <p>I'm investigating machine learning applications in genomics.</p>
</div>
```

---