---
name: Git-commiter
description: Git best practices
license: MIT
compatibility: opencode
---

# Git

- Do one commit per feature. Use ATOMIC commit.
- Use a rebase based workflow.
- Branches names are: `feature/`, `doc/`, `fix/`.
- Commit messages always starts with a tag: [bump], [doc], [feature], [fix], 
  [hotfix], [refactor], [unfeature], etc.
- After the tag, capitalized first letter is.
- Commit title are 50 chars long, but 72 can sometimes be ok.
- All commit should have a body, with references and explaination. Futures
  developers muse be able to document themself with commit body.
- When possible, use this wording (`close`, `closes`, `closed`, `fix`, `fixes`,
  `fixed`, `resolve`, `resolves`, `resolved`) to refer to other issues.
- Always add a `.gitignore` file.
