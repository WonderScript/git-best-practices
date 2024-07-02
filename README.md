# Git Best Practices

![Build Status](https://git-scm.com/images/logo@2x.png)


This document aims to provide a standard for writing, versioning, and applying changes in Git.

The following sections will cover branching, writing proper comments on changes, presenting them correctly with merge requests, and proper versioning.

Branches
This section provides a summary of Gitflow. For more details:


- [Gitflow Introduction by DataSift]

- [Gitflow Workflow by Atlassian]

Consider that for simplicity, some parts of the above sources have been altered, so the main reference is this document.



[//]: # (These are reference links used in the body of this note and get stripped out when the markdown processor does its job. There is no need to format nicely because it shouldn't be seen. Thanks SO -)

[Gitflow Introduction by DataSift]: <https://docs.github.com/en/pages>
[Gitflow Workflow by Atlassian]: <https://www.atlassian.com/git/tutorials/comparing-workflows/gitflow-workflow>



- **Master Branch**: This contains the project code (running version). Only the maintainers of each service are allowed to push to this branch. Remember to use bump-version for proper versioning, which is useful in many areas like sentry, staging, etc.

  - **Hotfix Branch**: Assume Hadi and Nima are working on specified features when the project manager suddenly notices an issue in the running project (which is naturally on the master branch) and wants it resolved quickly. Thus, they tell another developer to fix it promptly.


- **Development Branch**: Work on the project begins here. Developers can merge requests for maintainers to review and merge into development. Every merge updates the project staging.
  - **Feature Branch**: Suppose Nima is to work on login, and Hadi on home. They can each have their branches, such as feature/login and feature/home. When their work is done, these branches are merged into development and, if necessary, later into master.
  - **Hotfix branches**: are created without interfering with features, taken from master or development to fix the issue, and then merged back into master. Hadi and Nima continue their work without any issues.


```
git rebase --interactive <parent_branch>
```
