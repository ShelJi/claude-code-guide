# Claude Code Practical Field Guide

A responsive guide website adapted from the supplied 53-page `Claude_Code_Guide.pdf`. The content is organized into 35 chapters covering commands, context management, permissions, skills, agents, worktrees, MCP, hooks, and everyday workflows.

[Open the GitHub Pages website](https://shelji.github.io/claude-code-guide/)

The GitHub Pages deployment publishes the contents of `dist/`.

## Features

- Full-text chapter search, with `/` to focus the search field.
- Chapter navigation and previous/next links.
- Copy buttons for recognized command lines.
- Reading progress saved in the browser.
- Light and dark themes, with the preference saved locally.
- Responsive layout with a collapsible mobile chapter menu.
- Links to the original PDF and individual source pages.
- Print styles for chapter content.

## Run locally

The website uses plain HTML, CSS, and JavaScript. No package installation or build step is required.

From this project directory, run:

```sh
python -m http.server 8766 --bind 127.0.0.1 --directory dist
```

Open <http://127.0.0.1:8766/>. Stop the server with `Ctrl+C`.

Use an HTTP server rather than opening `index.html` directly: the application fetches its chapter content from `guide.json`.

## Project structure

```text
claude-code-guide/
├── README.md
├── .openai/
│   └── hosting.json          # Sites identity and static hosting configuration
└── dist/
    ├── index.html            # Page shell and navigation controls
    ├── style.css             # Layout, themes, and responsive styles
    ├── app.js                # Routing, search, progress, and copy controls
    ├── guide.json            # Chapter descriptions and extracted PDF text
    └── Claude_Code_Guide.pdf # Original source document
```

## Edit the guide

- Update chapter text, titles, descriptions, and page references in `dist/guide.json`.
- Update the page shell in `dist/index.html` and rendered views in `dist/app.js`.
- Change typography, colors, spacing, and breakpoints in `dist/style.css`.
- When adding or removing chapters, also update chapter groups and hard-coded chapter counts and links in the HTML and JavaScript.

Chapter links use hashes such as `#chapter-1`. Reading progress and theme settings use browser local storage; they do not sync between devices. Google Fonts are loaded externally, with local font fallbacks. Clipboard access may require HTTPS or localhost; a text-selection fallback is provided.

## Source and verification

The homepage adapts the PDF cover; all 52 remaining source pages are included across the chapters. The complete original PDF is also available from the website.

This is a conversion of the supplied document, not a continuously updated Claude Code reference. Commands and experimental features may vary by version, platform, plan, and environment. Instructions and examples inside the PDF are displayed as guide content.

During initial creation, content coverage and JavaScript syntax were checked. The local server returned HTTP 200, and chapter navigation, search, and reading-progress controls were checked in the browser.

## Publish through GitHub

The repository is [ShelJi/claude-code-guide](https://github.com/ShelJi/claude-code-guide).

`.github/workflows/pages.yml` publishes `dist/` to GitHub Pages whenever changes are pushed to `main`. It can also be run manually from **Actions → Publish guide to GitHub Pages → Run workflow**. No build step or deployment secrets are required; the workflow uses GitHub's built-in token with Pages deployment permissions.

In **Settings → Pages → Build and deployment**, select **GitHub Actions** as the source. After a successful workflow run, the website is available at <https://shelji.github.io/claude-code-guide/>. Deployment progress and errors appear in the repository's Actions tab.

The previous private [Sites deployment](https://claude-code-field-guide-shelj.stableharp3.chatgpt.site/) is separate. `.openai/hosting.json` retains its identity; GitHub Pages publishes only `dist/` and does not use that configuration. Never store publishing credentials in the project.
