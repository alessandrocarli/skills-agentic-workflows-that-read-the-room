---
name: update-github-info
on:
  schedule:
    - cron: "0 9 * * *"
  workflow_dispatch:
permissions:
  contents: read
engine: copilot
model: gpt-4o
tools:
  github:
    allowed:
      - get_file_contents
  web-fetch:
  edit:
network:
  allowed:
    - defaults
    - github.blog
    - github.com
    - awesome-copilot.github.com
safe-outputs:
  create-pull-request:
    draft: true
    max: 1
---

# Update GitHub Info

Maintain the practical GitHub Info page for Mona.

1. Read `notes/mona-notes.md` before making any changes.
2. Use the GitHub repository API tools to read repository guidance and reference files. Do not use terminal, CLI, or sandboxed commands for that repository reading.
3. Use the `web-fetch` tool, not `shell`, `curl`, or any command-line request, to read `https://github.blog/latest/`, `https://github.blog/changelog/`, and `https://awesome-copilot.github.com/workflows/`. Do not ask for permission to run shell commands for these URLs. If `web-fetch` cannot access a source, leave the content unchanged and use the `noop` safe output.
4. Update `site/content/github-info.md` with concise, practical developer guidance based on useful recent items. Preserve the existing editorial angle and mention the source for every item taken from the GitHub Blog or GitHub Changelog.
5. Use the `edit` tool to make the file change. Do not modify unrelated files.
6. Use the `create-pull-request` safe output to open a draft pull request for Mona to review. Include a concise summary, the source URLs, and the validation performed in the pull request body. Never write directly to `main`.

If there are no worthwhile updates or the content would be speculative, leave the content unchanged and do not open a pull request.