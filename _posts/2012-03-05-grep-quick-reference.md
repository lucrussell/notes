---
post_title: Grep Quick Reference
layout: post
published: true
tags:
  - linux
categories:
  - linux
---

## Grep Quick Reference
A quick reference for some handy grep statements.

The idea here is to be able to highlight a line in your IDE and execute it directly in a shell session. This saves some time trying to remember how to construct a particular command, and can be useful if you keep your development notes open in your IDE, in a dedicated project.

To set this up in IntelliJ family IDEs:
- Create a runner script, e.g. `command_runner.sh` which can execute supplied commands (see example below)
- Configure an External Tool in Settings:
    - Give it a name like "Execute with Bash"
    - Set the Program to your `command_runner.sh`
    - Set the Arguments to `$SelectedText$`
    - Set the Working Directory to `$ProjectFileDir$`
- Optionally assign a keyboard shortcut

This example simplified command runner script will pass the `$SelectedText$` to bash:

        #!/usr/bin/env bash
        eval "$@"


| Description  | Command |
| --- | --- |
| Show 2 lines of context before and after a matched line | grep -ir -C2 'word' * |
| Show the line number | grep -n 'word' * |
| Print file names only, containing the pattern | grep -ir -l 'word' * |
| Grep only in filenames with a particular extension | grep -ir --include=*.md 'word' |
| Exclude files with a particular extension | grep -ir --exclude=*.md 'word' |
| Recursive grep, searching for patterns in `patterns.txt` | find . -name *.md -exec grep -Hn -f patterns.txt {} \; |
| Recursive grep for `word` in all `.md` files | find . -name *.md -exec grep -Hn 'word' {} \\; |
| Count total occurences of `word`, including cases when a line contains multiple occurences | grep -oir 'word' * &#124; wc -l |
| Grep multiple strings with the `--perl-regexp` option | grep -r --perl-regexp 'hello&#124;goodbye' *|
| Count total occurences of `word`, including cases when a line contains multiple occurences | grep -oir 'word' * &#124; wc -l |
| Grep multiple strings with the `--perl-regexp` option | grep -r --perl-regexp 'hello&#124;goodbye' *|

(note `|` is escaped as `&#124;` in the table above)
