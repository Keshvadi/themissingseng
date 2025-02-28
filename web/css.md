---
title: CSS
parent: Web Fundamental
nav_order: 82
layout: default
---

## CSS (Cascading Style Sheets)

CSS is the language used to style HTML elements. It controls the presentation of web pages, including layout, colors, fonts, and responsiveness. Without CSS, websites would be plain text and basic HTML structures.

---

## Core Concepts

- **Selectors:** Target specific HTML elements to apply styles to. Common selectors include:

  - **Element Selector:** `p` (selects all `<p>` elements)
  - **ID Selector:** `#my-id` (selects the element with `id="my-id"`)
  - **Class Selector:** `.my-class` (selects all elements with `class="my-class"`)
  - **Attribute Selector:** `[type="text"]` (select all the elements with type text)
  - **Descendant Selector:** `div p` (selects all `<p>` elements inside `<div>` elements)
  - **Child Selector:** `div > p` (selects all `<p>` elements that are _direct_ children of `<div>` elements)
  - **Adjacent Sibling Selector:** `h2 + p` (selects the `<p>` element immediately following an `<h2>` element)
  - **Universal Selector:** `*` (selects _all_ elements - use sparingly)

- **Properties:** Define the styles to apply (e.g., `color`, `font-size`, `margin`, `padding`, `width`, `height`).

- **Values:** Specify the settings for properties (e.g., `red`, `16px`, `10px`, `20%`).

- **Declarations:** A property-value pair (e.g., `color: red;`).

- **Declaration Blocks:** A group of declarations enclosed in curly braces `{}`.

- **Rulesets:** A selector followed by a declaration block. This is the fundamental building block of CSS.

  ```css
  /* This is a CSS comment */
  p {
    /* Selector: targets all <p> elements */
    color: blue; /* Declaration: sets the text color to blue */
    font-size: 16px; /* Declaration: sets the font size to 16 pixels */
  }

  #header {
    /* Selector: targets the element with id="header" */
    background-color: #eee; /* Declaration: sets the background color */
    padding: 20px; /* Declaration: adds padding around the content */
  }

  .button {
    /* Selector: targets all elements with class="button" */
    background-color: green;
    color: white;
    border: none;
    padding: 10px 15px;
  }
  ```

---

## Ways to Add CSS

- **Inline Styles (least recommended):** Applied directly to an HTML element using the `style` attribute. Avoid this for most styling, as it's difficult to maintain and overrides other styles.

  ```html
  <p style="color: red; font-size: 18px;">This text is red and 18px.</p>
  ```

- **Internal Stylesheet (Embedded):** Placed within `<style>` tags inside the `<head>` section of an HTML document. Useful for single-page websites or small projects.

  ```html
  <!DOCTYPE html>
  <html>
    <head>
      <title>My Page</title>
      <style>
        p {
          color: blue;
        }
      </style>
    </head>
    <body>
      <p>This text will be blue.</p>
    </body>
  </html>
  ```

- **External Stylesheet (most recommended):** CSS rules are placed in a separate `.css` file and linked to the HTML document using the `<link>` tag. This is the best practice for larger projects, as it promotes reusability, maintainability, and separation of concerns.

  ```html
  <!DOCTYPE html>
  <html>
    <head>
      <title>My Page</title>
      <link rel="stylesheet" href="styles.css" />
    </head>
    <body>
      <p>This text will be styled by styles.css.</p>
    </body>
  </html>
  ```

  `styles.css`:

  ```css
  p {
    color: green;
  }
  ```

---

## Key CSS Concepts

- **The Box Model:** Every HTML element is treated as a rectangular box, consisting of content, padding, border, and margin. Understanding the box model is crucial for controlling layout.

- **Cascading and Specificity:** "Cascading" refers to how styles are applied from multiple sources (browser defaults, external stylesheets, internal stylesheets, inline styles). "Specificity" determines which rules take precedence when there are conflicts. More specific selectors override less specific ones.

- **Inheritance:** Some CSS properties are inherited by child elements from their parent elements (e.g., `font-family`, `color`).

- **Display Property:** Controls how an element is displayed (`block`, `inline`, `inline-block`, `none`, `flex`, `grid`).

- **Positioning:** Controls the position of elements (`static`, `relative`, `absolute`, `fixed`, `sticky`).

- **Floats:** Used to position elements side-by-side (though Flexbox and Grid are generally preferred for layout).

- **Flexbox:** A powerful layout module for creating flexible and responsive one-dimensional layouts.

- **Grid:** A powerful layout module for creating complex two-dimensional layouts.

- **Media Queries:** Used to apply different styles based on the device's characteristics (e.g., screen size, orientation). Essential for creating responsive designs.
- **Pseudo-classes**: used to define a special state of an element. (For example, `:hover`, `:active`, `:visited`)
- **Pseudo-elements**: used to style specified parts of an element. (For example, `::before`, `::after`)

---
