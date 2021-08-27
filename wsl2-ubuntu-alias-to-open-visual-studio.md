---
layout: default
date: 2021-08-21
title: WSL2 Ubuntu Alias to Open Visual Studio
tags: [WSL2, til, published]
---

I recently reinstalled WSL2 on my Windows machine, and I'm trying to work exclusive through that shell, even when I open Windows-based applications.

VS Code already does this really well, and the integration is great. I, however, work in Visual Studio somewhat regularly, so I wanted the same type of experience as `code .`.

Here's my `.zshrc`:

```bash
export PATH="/mnt/c/Program Files (x86)/Microsoft Visual Studio/2019/Enterprise/Common7/IDE/:$PATH"

...

alias vs="devenv.exe *.sln > /dev/null 2>&1 &"
```

Note that I add the Visual Studio 2019 path to the `$PATH` environment variable (this is obviously different based on the different Visual Studio versions), then I set an alias at the bottom to fire up Visual Studio for the solutions in the current director with the `vs` alias. I added in the `> /dev/null 2>&1 &` to run it in the background and to pipe output and erros to `stdout`.