---
title: 01. Git Configuration
description: Configure Git with ignored files, custom commit message templates and Git LFS tracking.
date: "2025-03-08T00:34:15+06:00"
tags: ["devlog"]
categories: ["trading-platform"]
author: "Jayen"
---

Git can be customized to have certain behavior. I want to have the following:

-   Git commit messages to the repository must follow the
    [Conventional Commits](https://www.conventionalcommits.org/en/v1.0.0/) specification.
-   All text files committed to the repository must have a UNIX `lf` line ending.
-   A generic `.gitignore` file that contains OS specific files to be ignored from Git's tracking.
-   Use Git LFS to track media files and binaries.

To achieve this, I'll need to add the following 4 files:

```
trading-platform/
├── .gitattributes  # configure Git LFS tracked files
├── .gitconfig      # use custom commit message template
├── .gitmessage     # commit message template
└── .gitignore      # ignore files from Git's tracking
```

## `.gitattributes`

```
# EOL of text files
* text=auto eol=lf

# Git LFS tracked files
*.png filter=lfs diff=lfs merge=lfs -text
*.jpg filter=lfs diff=lfs merge=lfs -text
*.jpeg filter=lfs diff=lfs merge=lfs -text
*.webp filter=lfs diff=lfs merge=lfs -text
*.mp3 filter=lfs diff=lfs merge=lfs -text
*.mp4 filter=lfs diff=lfs merge=lfs -text
*.webm filter=lfs diff=lfs merge=lfs -text
*.avi filter=lfs diff=lfs merge=lfs -text
```

## `.gitconfig`

```
[commit]
    template = .gitmessage
```

To use this custom config file, the following command needs to be ran after the repository has been
successfully cloned.

```bash
git config --local include.path ../.gitconfig
```

## `.gitmessage`

```
type(scope): message
```

## `.gitignore`

There's a repository containing templates for all commonly used .gitignore files based on Operating
Systems and languages. I've used the following templates for this repository.

-   [Windows](https://github.com/github/gitignore/blob/main/Global/Windows.gitignore)
-   [macOS](https://github.com/github/gitignore/blob/main/Global/macOS.gitignore)
-   [Linux](https://github.com/github/gitignore/blob/main/Global/Linux.gitignore)
-   [Node](https://github.com/github/gitignore/blob/main/Node.gitignore)

```
## Windows
[Windows Template]

## MacOS
[macOS Template]

## Linux
[Linux Template]

## NodeJS
[Node Template]
```
