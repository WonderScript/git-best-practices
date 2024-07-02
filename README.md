![Build Status](https://git-scm.com/images/logo@2x.png)
# Git Best Practices



This document aims to provide a standard for writing, versioning, and applying changes in Git.

The following sections will cover branching, writing proper comments on changes, presenting them correctly with merge requests, and proper versioning.

## Branches

This section provides a summary of Gitflow. For more details:


- [Gitflow Introduction by DataSift]

- [Gitflow Workflow by Atlassian]

Consider that for simplicity, some parts of the above sources have been altered, so the main reference is this document.

- **Master Branch**: This contains the project code (running version). Only the maintainers of each service are allowed to push to this branch. Remember to use bump-version for proper versioning, which is useful in many areas like sentry, staging, etc.

  - **Hotfix Branch**: Assume Mehrdad and Mohammad are working on specified features when the project manager suddenly notices an issue in the running project (which is naturally on the master branch) and wants it resolved quickly. Thus, they tell another developer to fix it promptly.


- **Development Branch**: Work on the project begins here. Developers can merge requests for maintainers to review and merge into development. Every merge updates the project staging.
  - **Feature Branch**: Suppose Mohammad is to work on login, and Mehrdad on home. They can each have their branches, such as feature/login and feature/home. When their work is done, these branches are merged into development and, if necessary, later into master.
  - **Hotfix branches**: are created without interfering with features, taken from master or development to fix the issue, and then merged back into master. Mehrdad and Mohammad continue their work without any issues.


```
git rebase --interactive <parent_branch>
```

After completing a hotfix, besides merging into master, merge it into development as well. This ensures that the hotfix changes are applied to all live branches of the project.

Always create hotfix branches from the latest version of the master.

Apply changes on master using merge requests. If you are a project maintainer and need to make a change on master, for example, applying a hotfix, use:

```
git checkout master
git merge --no-ff hotfix/login
git branch -d hotfix/login
git push origin master
```

The --no-ff flag ensures that every merge creates a new commit, preserving the feature branch history.

**Writing**
This section introduces a standard for writing commit messages based on the conventional commit standard. All developers must adhere to it, and non-compliant commits should not be merged.

For examples, see [Conventional Commits].

## Commits

#### Purpose of Standardization                
1. Using tools to automatically generate a CHANGELOG.md file.
2. Readability of Git history.
3. Enabling easier navigation through Git history to find specific changes.

### Standard to Follow

```
<type>(<scope>): <subject>
# blank line
<body>
# blank line
<footer>
```

### Definitions

- **Scope (optional)**: The area where changes occur, such as file name, package name, API name, algorithm name, or any other name understandable to an external developer.

- **Type (mandatory)**: The type of commit made, including:
  - feat (feature)
  - fix
  - docs
  - refactor
  - style (changes that do not affect the code meaning, e.g., spacing)
  - chore (specific message to show routine tasks or maintenance)
  - perf (changes positively affecting program speed)
  - ci (Cindicate the continuous integration (CI) system-related changes)
  - build (changes related to the build process)
  - revert (changes related to revert a previous commit)

- **Subject (mandatory)**: A brief explanation of the work done in one line, maximum 50 characters, imperative, and capitalized without a period at the end.

- **Body (optional)**:  Separated by a blank line from the subject, each line should be no more than 72 characters, imperative, present tense, answering "why," "how," and "where," possibly referencing other commits.

- **Footer (optional)**: Includes references such as issue numbers closed by the commit or Trello cards.

```
feat(2FA): Add two factor authentication

Add new menus to improve navigation. These new menus are intended to improve the user experience. Implement URL handling in the  function to differentiate between local and external redirects. Additionally.

Closes #32
```

### Tools

- **Node.js**: Commitizen, Commitlint




















[//]: # (These are reference links used in the body of this note and get stripped out when the markdown processor does its job. There is no need to format nicely because it shouldn't be seen. Thanks SO -)

[Gitflow Introduction by DataSift]: <https://docs.github.com/en/pages>
[Gitflow Workflow by Atlassian]: <https://www.atlassian.com/git/tutorials/comparing-workflows/gitflow-workflow>
[Conventional Commits]: <https://www.conventionalcommits.org>
