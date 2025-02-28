# The Missing Software Engineering Course

This is the source for <a href="https://keshvadi.github.io/linux/">The Shell webbook</a>. It is built through Github Pages.

Updates to the textbook are recorded in the commit history of this repository.

# Source Code Formatting

This repository has auto-formatting enabled. The preferred way to format source is through Prettier on your local machine. Install Node on your computer, run `npm install -g yarn`, and then run `yarn`. To format code, use the `yarn prettier` command, which will automatically format all .md and .html files.

There is also a GitHub Action to format code which can be dispatched manually. Go to the Actions tab, find the Auto-Format Source action, and manually trigger a workflow dispatch against the target branch.

A CI check is enabled which runs Prettier and fails if Prettier detects any formatting errors.

<!--
run locally:
> bundle exec jekyll serve
 -->
