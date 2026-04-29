# gitflow_project

## Overview
This repository teaches Git Flow. Below is a mermaid gitGraph diagram that visualizes the main branches used in Git Flow and typical branch transitions.

`mermaid
gitGraph
   commit id: "init"
   branch develop
   commit id: "start dev"
   branch feature/my-feature
   commit id: "work on feature"
   checkout develop
   merge feature/my-feature
   branch release/1.0.0
   checkout master
   merge release/1.0.0
   tag v1.0.0
   branch hotfix/urgent-fix
   checkout master
   merge hotfix/urgent-fix
   tag v1.0.1
`

## What is Git Flow?
Git Flow is a branching model that defines a strict branching strategy: a long-lived 'master' (or 'main') for production, a 'develop' branch for ongoing development, short-lived 'feature/*', 'release/*', and 'hotfix/*' branches for work.

## Beginner Assignment: Implementing Git Flow (step-by-step)
Follow these steps in this repository to practice Git Flow. Commands assume your remote is named 'origin' and your default branch is 'master'. Replace names where appropriate.

1. Clone the repo:

   git clone https://github.com/nsrnkably/gitflow_project.git
   cd gitflow_project

2. Create the develop branch (from master):

   git checkout -b develop master
   git push -u origin develop

3. Start a feature branch:

   git checkout -b feature/add-login develop
   # make changes
   git add .
   git commit -m "Add login feature"
   git push -u origin feature/add-login

4. Open a Pull Request to merge feature/add-login into develop; after review merge using --no-ff to preserve branch history.

   git checkout develop
   git pull origin develop
   git merge --no-ff feature/add-login
   git push origin develop

5. Create a release branch when ready for release:

   git checkout -b release/1.0.0 develop
   # update version, docs, run tests
   git add .
   git commit -m "Prepare release 1.0.0"
   git push -u origin release/1.0.0

   # After final checks, merge into master and develop, and tag
   git checkout master
   git merge --no-ff release/1.0.0
   git tag -a v1.0.0 -m "Release 1.0.0"
   git push origin master --tags

   git checkout develop
   git merge --no-ff release/1.0.0
   git push origin develop

6. Hotfix process (urgent fix on production):

   git checkout -b hotfix/urgent-fix master
   # fix bug
   git add .
   git commit -m "Fix critical bug"
   git push -u origin hotfix/urgent-fix

   # After tests, merge into master and develop
   git checkout master
   git merge --no-ff hotfix/urgent-fix
   git tag -a v1.0.1 -m "Hotfix 1.0.1"
   git push origin master --tags

   git checkout develop
   git merge --no-ff hotfix/urgent-fix
   git push origin develop

## Tasks for the student
- Create a feature branch, implement a small feature, open a PR to develop, and merge.
- Create a release branch, bump version, and perform the release merge into master with tagging.
- Simulate a hotfix from master and merge the fix back into develop.
- Write brief notes in this README describing what you did for each step.

Happy learning!