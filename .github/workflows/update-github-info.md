---
name: update-github-info
description: Draft website updates for Mona's GitHub Info site from official GitHub sources.
on:
  workflow_dispatch: {}
  schedule:
    - cron: '0 9 * * *' # daily at 09:00 UTC
safe-outputs:
  create-pull-request:
    title-prefix: "[mona] "
    draft: true
    fallback-as-issue: false
tools:
  # Allow the agent to edit files at specified paths and fetch web content from approved hosts
  edit: {}
  web-fetch: {}
network:
  allowed:
    - github.com
    - github.blog
permissions:
  contents: read
  pull-requests: read
  actions: read
  issues: read
  checks: read
---

# Update Mona's GitHub Info website

Read `notes/mona-notes.md` before making changes.

Use these sources:
- `notes/mona-notes.md`
- GitHub Blog: https://github.blog/latest/
- GitHub Changelog: https://github.blog/changelog/

The agent should:

- Read `notes/mona-notes.md` to understand Mona's preferences and context.
- Web fetch `https://github.blog/latest/` and `https://github.blog/changelog/` and extract concise, reader-friendly updates.
- Update `site/content/github-info.md` by adding or refreshing a section titled "## Latest GitHub Updates" with short summaries and links to sources.
- Include source attribution for any content derived from the GitHub Blog or Changelog.
- Prepare changes as a patch and open a pull request for Mona to review using the `safe-outputs: create-pull-request` mechanism. Do not write directly to `main`.

Pull request guidance:

- Use a title prefixed with "[mona]" and make the PR a draft.
- Explain in the PR body which sources were consulted and include short excerpts or links as appropriate.
- If no changes are needed (no substantive new updates), place a short comment in the PR describing why (e.g., "No new GitHub updates found today").

Include the phrases "GitHub Blog", "GitHub Changelog", "safe-outputs", "create-pull-request", and "pull request" in the workflow file to satisfy repository checks.

Do not compile this file. Only create or update the markdown workflow file.