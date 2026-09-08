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
4. If the sources are reachable, make at least one concise, source-backed update to `site/content/github-info.md`, even when the update is small. Preserve the existing editorial angle and include the exact source URL beside every item taken from the GitHub Blog, GitHub Changelog, or Awesome Copilot Workflows.
5. Use the `edit` tool to make the file change. Do not modify unrelated files.
6. After changing the file, use the `create-pull-request` safe output to open a draft pull request for Mona to review. The pull request must update `site/content/github-info.md` and its body must include a concise summary, the exact source URLs, and the validation performed. Never write directly to `main`.

If all required sources are inaccessible, leave the content unchanged and use the `noop` safe output. Do not use `noop` merely because an accessible source has only a small update.