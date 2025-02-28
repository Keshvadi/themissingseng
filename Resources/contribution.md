---
title: Contribution Guide
parent: Resources
nav_order: 103
layout: default
---

## Contribution Guide

This webbook is built using the [Just the Docs](https://just-the-docs.github.io/just-the-docs/) theme for Jekyll. We welcome contributions from the community! This guide outlines how to set up your local environment, make changes, and submit them for review.

---

### Setting Up Your Local Environment

To preview your changes locally before submitting them, you'll need to build and run the site on your computer. Follow the instructions in the "Building and previewing your site locally" section of the Just the Docs template repository:

[https://github.com/just-the-docs/just-the-docs-template?tab=readme-ov-file#building-and-previewing-your-site-locally](https://github.com/just-the-docs/just-the-docs-template?tab=readme-ov-file#building-and-previewing-your-site-locally)

In summary, you'll need:

1.  **Ruby:** Just the Docs is built with Jekyll, which requires Ruby.
2.  **Bundler:** A Ruby gem for managing project dependencies. Install it with `gem install bundler`.
3.  **Jekyll:** A static site generator.
4.  **Git**

The linked instructions provide detailed steps for installing these prerequisites and building the site. Essentially, you will:

- Clone the repository.
- Install the required gems using `bundle install`.
- Run the site locally using `bundle exec jekyll serve`.

---

### Making Changes

1.  **Fork the Repository:** If you haven't already, fork the repository on GitHub. This creates your own copy of the project where you can make changes.

2.  **Clone Your Fork:** Clone _your fork_ to your local machine:

    ```bash
    git clone [https://github.com/YOUR_USERNAME/linux.git](https://www.google.com/search?q=https://github.com/YOUR_USERNAME/linux.git)  # Replace YOUR_USERNAME with your GitHub username
    cd linux
    ```

3.  **Create a Branch:** Create a new branch for your changes. Use a descriptive branch name that reflects the content you're adding or modifying (e.g., `add-docker-commands`, `fix-typos-cicd`, `expand-html-section`).

    ```bash
    git switch -c your-branch-name
    ```

4.  **Make Your Changes:** Edit the Markdown files in the appropriate directories. Follow the style and formatting conventions used in the existing content (see "Content Guidelines" below).

5.  **Preview Your Changes:** Run the site locally using `bundle exec jekyll serve`. This will start a local web server (usually at `http://localhost:4000`). Open this address in your browser to see your changes. Jekyll will automatically rebuild the site whenever you save a file.

6.  **Commit Your Changes:** Once you're happy with your changes, commit them with clear and descriptive commit messages:

    ```bash
    git add .  # Stage all changes (or use 'git add <filename>' to stage specific files)
    git commit -m "Add a section on Docker volumes to the Docker Commands page"
    ```

7.  **Push Your Changes:** Push your branch to your forked repository on GitHub:

    ```bash
    git push -u origin your-branch-name
    ```

8.  **Create a Pull Request:** Go to your forked repository on GitHub. You should see a prompt to create a pull request from your newly pushed branch. Click the "Compare & pull request" button. Write a clear description of your changes, and submit the pull request.

---

### Content Guidelines

Before submitting your changes, please ensure they adhere to the following guidelines:

- **Accuracy:** All information should be technically accurate and up-to-date.
- **Clarity:** Write clear, concise, and easy-to-understand explanations. Avoid jargon where possible, and explain technical terms when necessary.
- **Consistency:** Follow the style and formatting of existing content. This includes:
  - **Markdown Formatting:** Use Markdown for headings, lists, code blocks, etc.
  - **Code Style:** Use backticks (`) for inline code and commands.  Use triple backticks (`) for code blocks, and specify the language (e.g., `bash, `python, `javascript, `html, `json).
  - **Command Examples:** Provide clear and practical examples for all commands. Include sample output where appropriate.
  - **Terminology:** Use consistent terminology throughout the webbook.
  - **Front Matter:** Use consistent Front Matter.
- **Completeness:** Provide complete explanations and examples. Don't assume prior knowledge beyond the target audience (undergraduate software engineering students).
- **Navigation Order (`nav_order`):**

  - The `nav_order` in the front matter determines the order of pages in the navigation.
  - `nav_order` values are based on their parent's numbering, for example:

    - Linux & Command Line: 20s
    - Docker: 50s
    - Git & Version Control: 60s
    - CI/CD: 70s
    - Web Fundamental: 80s
    - Cloud Computing: 90s
    - About: 101
    - Contribution Guide: 102
    - Resourses: 103

  - When adding a _new_ page, choose an appropriate `nav_order` value that fits within the existing structure. If adding a page within a section, increment the `nav_order` of subsequent pages if necessary to maintain a logical order.

- **Parent Page:**
  - Make sure you added the correct `parent` to the Front Matter.
- **Keep it simple**:
  - The content are for undergarduate student, so make sure to avoid making it very complicated.

---

### Review Process

Once you've submitted a pull request, a maintainer of the project will review your changes. They may provide feedback or request changes. Please be responsive to any feedback and address any requested changes. Once your changes are approved, they will be merged into the main branch and become part of the webbook.

Thank you for contributing!
