---
title: PDF and Image Manipulation
parent: Common Use Cases
nav_order: 44
layout: default
---

## PDF and Image Manipulation

The command line provides powerful tools for manipulating PDF and image files, often offering more efficient and scriptable alternatives to graphical applications. This section covers some common utilities.

---

### PDF Manipulation

#### `pdftk` (PDF Toolkit)

- **Description:** A versatile tool for manipulating PDF files. It can merge, split, rotate, encrypt, decrypt, and more. `pdftk` is _not_ usually installed by default.

- **Installation:**

  - Debian/Ubuntu: `sudo apt install pdftk-java`
  - CentOS/Fedora: `sudo yum install pdftk` / `sudo dnf install pdftk` (may require enabling the EPEL repository first)
  - If `pdftk` is not available, `qpdf` (see below) is a good alternative for many tasks.

- **Example Usage:**

  ```bash
  pdftk file1.pdf file2.pdf cat output combined.pdf  # Merge multiple PDFs
  pdftk input.pdf cat 1-3 output part1.pdf        # Extract pages 1-3
  pdftk input.pdf cat 4-end output part2.pdf      # Extract pages 4 to the end
  pdftk input.pdf burst output page_%02d.pdf      # Split a PDF into individual pages (page_01.pdf, page_02.pdf, etc.)
  pdftk input.pdf rotate 90 output rotated.pdf     # Rotate all pages 90 degrees clockwise
  pdftk input.pdf cat 1-endright output rotated.pdf # Rotate all pages 90 degrees clockwise
  pdftk input.pdf cat 1-endleft output rotated_left.pdf # Rotate all pages 90 degrees counter-clockwise
  pdftk input.pdf cat 1-enddown output upside_down.pdf # Rotate all pages 180 degrees
  pdftk input.pdf background background.pdf output output.pdf # apply a background
  pdftk input.pdf dump_data output report.txt       # Extract metadata
  pdftk secured.pdf input_pw foopass output unsecured.pdf # decrypt a file
  pdftk input.pdf output secured.pdf owner_pw foo user_pw baz allow printing # encrypt a file
  ```

---

#### `qpdf`

- **Description**: `qpdf` is a command-line tool that does structural, content-preserving transformations on PDF files.
- **Installation**:
  - Debian/Ubuntu: `sudo apt install qpdf`
  - CentOS/Fedora: `sudo yum install qpdf` / `sudo dnf install qpdf`
- **Example Usage:**
  ```bash
    qpdf --empty --pages file1.pdf file2.pdf -- out.pdf # Merge PDF files
    qpdf in.pdf --pages in.pdf 1-5 -- out.pdf           # get pages of a file
    qpdf --decrypt input.pdf output.pdf                 # decrypt a file
    qpdf --encrypt user_password owner_password 40bit -- input.pdf output.pdf # encrypt a file
  ```
