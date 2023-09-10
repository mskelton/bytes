---
title: Vim Jump to Column
date: 2023-09-10
tags: vim
---

In Vim, sometimes I want to jump to a specific column. For example, jumping to
column 80 (the print width of the file), to do some reformatting. Thankfully,
this is pretty easy using the `|` command.

```vim
80|
```

Without any arguments, `|` will take you to the beginning of the line, but with
a count, you can jump to any column you want.
