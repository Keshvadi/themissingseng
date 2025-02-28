---
title: HTML
parent: Web Fundamental
nav_order: 81
layout: default
---

## HTML (HyperText Markup Language)

HTML is the standard markup language for creating web pages. It uses tags to structure content, defining elements like headings, paragraphs, images, links, and more. Browsers interpret these tags to render the page visually. HTML provides the _structure_ and _content_ of a webpage; CSS provides the _style_, and JavaScript provides the _interactivity_.

---

## Core Concepts

- **Tags:** Keywords enclosed in angle brackets (`< >`). Most tags come in pairs: an opening tag (e.g., `<p>`) and a closing tag (e.g., `</p>`).
- **Elements:** An opening tag, a closing tag, and the content in between (e.g., `<p>This is a paragraph.</p>`).
- **Attributes:** Provide additional information about an element. They are placed within the opening tag and have a name and a value (e.g., `<img src="image.jpg" alt="A description of the image">`).
- **Structure:** HTML documents follow a specific structure:

  - `<!DOCTYPE html>`: Declares the document type (HTML5).
  - `<html>`: The root element.
  - `<head>`: Contains meta-information about the document (title, links to stylesheets, etc.). This content is _not_ displayed on the page itself.
  - `<body>`: Contains the visible content of the page.

- **Common Tags:**
  - `<h1>`, `<h2>`, `<h3>`, `<h4>`, `<h5>`, `<h6>`: Headings (from largest to smallest).
  - `<p>`: Paragraph.
  - `<a>`: Anchor (creates a hyperlink). Uses the `href` attribute to specify the link's destination.
  - `<img>`: Image. Uses the `src` attribute to specify the image source and the `alt` attribute to provide alternative text (for accessibility and SEO).
  - `<ul>`: Unordered list (bullet points).
  - `<ol>`: Ordered list (numbered).
  - `<li>`: List item (used inside `<ul>` or `<ol>`).
  - `<div>`: Division (a generic container for grouping elements).
  - `<span>`: Inline container (used for grouping inline elements).
  - `<br>`: Line break (a self-closing tag).
  - `<hr>`: Horizontal rule (a thematic break - also self-closing).
  - `<table>`: Table.
  - `<tr>`: Table row.
  - `<th>`: Table header cell.
  - `<td>`: Table data cell.
  - `<form>`: Form (for user input).
  - `<input>`: Input field (text, password, button, etc.).
  - `<textarea>`: Multi-line text input.
  - `<button>`: Button.
  - `<select>`: Drop-down list.
  - `<option>`: Option within a drop-down list.

---

## Example HTML Document

```html
<!DOCTYPE html>
<html>
  <head>
    <title>My First Web Page</title>
    <link rel="stylesheet" href="styles.css" />
  </head>
  <body>
    <h1>Welcome to My Page</h1>

    <p>
      This is a paragraph of text. You can add multiple lines of text within the
      `
    </p>
    <p>` tags, and it will display as a single block of text.</p>

    <p>
      Here’s another paragraph. You can use <strong>bold</strong> or
      <em>italic</em> text, add <a href="https://www.example.com">links</a>, or
      even include images:
    </p>

    <img src="image.jpg" alt="A sample image" width="300" />

    <ul>
      <li>Item 1</li>
      <li>Item 2</li>
      <li>Item 3</li>
    </ul>

    <footer>
      <p>&copy; 2025 My First Web Page</p>
    </footer>
  </body>
</html>
```
