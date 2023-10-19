# Coding Convention

## I. Git Commits
### A. Commit Types
+ feat – a new feature is introduced with the changes
+ fix – a bug fix has occurred
+ chore – changes that do not relate to a fix or feature and don't modify src or test files (for example updating dependencies)
+ refactor – refactored code that neither fixes a bug nor adds a feature
+ docs – updates to documentation such as the README or other markdown files
+ style – changes that do not affect the meaning of the code, likely related to code formatting such as white-space, missing semi-colons, and so on.
+ test – including new or correcting previous tests
+ perf – performance improvements
+ ci – continuous integration related
+ build – changes that affect the build system or external dependencies
+ revert – reverts a previous commit
+ BREAKING CHANGE: <description> - notes the reason for a breaking change within the commit

### B. Message Structure
```
<type>[optional scope]: <description>

[optional body]

[optional footer(s)]

Optional
Footnote: Closes D2IQ-<JIRA #>
```
### C. Commit Message Guide

> If applied, this commit will “commit message”
>
> &emsp; Good: If applied, this commit will “Add cart indicator to navbar”
> 
> &emsp; Bad: If applied, this commit will “adding cart indicator to navbar”

### D. References
+ [Dev.to - How to write better git commit messages](https://dev.to/ahmed0saber/how-to-write-better-git-commit-messages--40al)
+ [FreeCodeCamp - How to write better git commit messages](https://www.freecodecamp.org/news/how-to-write-better-git-commit-messages/)
