---
name: update-github-info
description: Keep Mona's GitHub Info content current with official GitHub Blog and Changelog updates.
on:
  schedule:
    - cron: "0 9 * * *"
  workflow_dispatch:
permissions:
  contents: read
tools:
  edit:
  web-fetch:
network:
  allowed:
    - github.blog
    - github.com
    - awesome-copilot.github.com
safe-outputs:
  create-pull-request:
    max: 1
    draft: true
    base-branch: main
    allowed-files:
      - site/content/github-info.md
---

# Update Mona's GitHub Info

Maintain the content used by Mona's GitHub Info website.

1. Read `notes/mona-notes.md` before making editorial decisions.
2. Use the `web-fetch` tool to read:
   - https://github.blog/latest/
   - https://github.blog/changelog/
    - https://awesome-copilot.github.com/workflows/
3. Use GitHub repository API tools to read repository guidance and reference files. Do not use the terminal, CLI, or sandboxed commands for repository guidance or external public guidance.
4. Identify a small set of recent, useful updates for developers. Keep summaries short and practical, and include the official source URL and whether each item comes from the GitHub Blog or GitHub Changelog.
5. Use the `edit` tool to update only `site/content/github-info.md`. Preserve its existing Markdown structure and retain useful existing content while refreshing stale update entries.
6. Use the `create-pull-request` safe output to open one draft pull request for Mona to review. Describe the sources consulted and summarize the content changes in the pull request body. Never write directly to `main`.

If the official pages contain no meaningful new updates, leave the content unchanged and do not create a pull request.