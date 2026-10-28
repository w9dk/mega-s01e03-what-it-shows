---
name: gh-course-repo-routine
description: "Use gh to prepare and verify a public GitHub repository and its challenge issues after the human approves the repository name, visibility, and publication scope."
---

# Gh Course Repo Routine

Use this when a MEGA.dev challenge requires a public repository and GitHub issues.

## Approval and access

- Before creating a repository or publishing files/issues, show the human the exact repository name, public visibility, files, and issue titles/counts. Wait for approval of that set.
- Check `gh auth status` before mutations. If it is not signed in, ask the human to complete `gh auth login -h github.com`; never request or handle their token.
- Check each command's `--help` for the flags used. Do not install another GitHub client when `gh` is already available.
- Keep credentials, local paths, and private data out of public files and issue bodies.

## Routine

1. Prepare the repository files locally and inspect the final contents.
2. Initialize and commit the local repository.
3. Create and push the approved public repository with `gh repo create <name> --public --source <path> --remote origin --push`.
4. Verify the remote repository URL and public visibility with `gh repo view`.
5. For each approved issue, create it with `gh issue create --repo <owner/name> --title <title> --body-file <file>`. Record the returned URL and number.
6. Verify each issue with `gh issue view <url> --json number,title,body,state,url`; confirm its title and body match the approved draft.

If any command fails or creates a different public result than approved, stop and report the exact result before trying another mutation.
