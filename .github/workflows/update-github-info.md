---
name: update-github-info
on:
  schedule: daily
  workflow_dispatch:

permissions:
  contents: read
  pull-requests: read

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
    reviewers: [mona]
    allowed-files:
      - site/content/github-info.md

model: gpt-4.1
---

# Update GitHub Info

Keep Mona's GitHub Info content current using concise, practical information for developers.

## Instructions

1. Read `notes/mona-notes.md` and `site/content/github-info.md` before drafting.
2. Fetch https://github.blog/latest/, https://github.blog/changelog/, and https://awesome-copilot.github.com/workflows/ with the `web-fetch` tool. Use those official sources to identify recent items relevant to the site's existing themes: GitHub collaboration, GitHub Copilot, or GitHub Actions.
3. Update only `site/content/github-info.md`. Keep summaries short and practical, preserve useful existing guidance, and include a direct source link whenever information comes from a fetched source. Do not add claims that are not supported by the fetched sources.
4. If none of the sources has a relevant update, make no content changes and do not open an empty pull request.
5. When there is a meaningful update, use the `create-pull-request` safe output to open one pull request for Mona to review. Summarize what changed and cite the official source links in the pull request description. Never push changes directly to the default branch or change files outside `site/content/github-info.md`.
