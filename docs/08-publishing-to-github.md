# 8 — Publishing the project to GitHub

This repository is designed to be published **without** including personal network information or photos of a private residence.

## Option A: GitHub website (no command line required)

1. Go to [github.com/new](https://github.com/new).
2. Choose a descriptive repository name such as `liftmaster-la400dc-local-homeassistant` and set **Public**.
3. Avoid selecting **Initialize with README** if you plan to push this prepared folder as a Git repository (the folder already contains one).
4. On your computer, unzip the prepared files and follow the `git` commands below, replacing `OWNER` and `REPOSITORY`.

## Option B: GitHub CLI

Install and authenticate [GitHub CLI](https://cli.github.com/), then run from the repository folder:

```bash
git init
git add .
git commit -m "Initial LiftMaster LA400DC local Home Assistant guide"
git branch -M main
gh repo create liftmaster-la400dc-local-homeassistant --public --source=. --remote=origin --push
```

If you're already in a git repository, **don't** re-run `git init` blindly; check your existing remote first.

## Option C: Existing empty GitHub repository

```bash
git init
git add .
git commit -m "Initial documentation and configurations"
git branch -M main
git remote add origin https://github.com/OWNER/REPOSITORY.git
git push -u origin main
```

## Review before pushing

- [ ] All real Wi-Fi secrets and ESPHome encryption keys removed.
- [ ] No private street address, GPS coordinates, personal names, serial numbers or identifiable home photographs.
- [ ] Confirm all wiring and safety limitations are clearly described.
- [ ] Confirm hardware revisions, official documentation links, and script examples are correct for the target model.
- [ ] Validate YAML locally in the actual ESPHome and Home Assistant versions before presenting it as tested.
- [ ] Obtain permission before publishing any images showing another person's property.

**If making a public repository, do not assume Git history is private:** removing a secret in a later commit does not remove it from earlier commits. Audit before the *first* commit.
