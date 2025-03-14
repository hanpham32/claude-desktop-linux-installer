# Branch Protection Rules

To ensure code quality and stability, we've implemented branch protection rules for the `main` branch. Follow these steps to configure them in your GitHub repository:

1. Go to your repository on GitHub
2. Click on "Settings"
3. In the left sidebar, click on "Branches"
4. Under "Branch protection rules", click "Add rule"
5. For "Branch name pattern", enter `main`
6. Configure the following settings:

## Required settings

- [x] Require a pull request before merging
  - [x] Require approvals (recommended: at least 1)
- [x] Require status checks to pass before merging
  - [x] Require branches to be up to date before merging
  - Status checks that are required:
    - [x] Shellcheck Syntax Validation
    - [x] Test Installation on Ubuntu
    - [x] Test Installation on Debian
    - [x] Test Installation on Arch Linux
- [x] Include administrators

## Optional (but recommended) settings

- [x] Restrict who can push to matching branches
  - Add specific users/teams who should have push access
- [x] Allow force pushes (NOT recommended for `main`)
- [x] Allow deletions (NOT recommended for `main`)

7. Click "Create" or "Save changes"

These settings ensure that:

1. All code changes must go through pull requests
2. Pull requests must pass all required CI/CD checks
3. Pull requests must be reviewed before merging
4. The `main` branch is protected from direct pushes, force pushes, and deletions

This helps maintain a high-quality codebase and provides an audit trail of changes.
