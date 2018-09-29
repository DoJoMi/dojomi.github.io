# dojomi.github.io

```bash
#!/bin/bash
printf "%s" "# dojomi.github.io" >> README.md
git add README.md
git commit -m "first commit"
git push
git config --global credential.helper 'cache --timeout=3600'

git checkout -b src
git submodule init
git submodule add https://github.com/calintat/minimal.git themes/minimal
git submodule update --remote themes/minimal

cat > config.toml <<EOF
baseURL = "https://dojomi.github.io"
languageCode = "en-us"
title = "dojomi.github.io"
theme = "minimal"

[params]
    author = "DoJoMi"
    description = "$ do | more;"
    githubUsername = "#"
    accent = "red"
    showBorder = true
    backgroundColor = "white"
    font = "Raleway"
    highlight = true
    highlightStyle = "solarized-dark"
    highlightLanguages = ["bash" ,"go", "haskell", "kotlin", "scala", "swift"]

[[menu.main]]
    url = "https://dojomi.github.io/centbox/"
    name = ">_ centbox"
    weight = 1

[[menu.icon]]
    url = "https://github.com/dojomi/"
    name = "github"
    weight = 2
EOF

mkdir content
git add .
git commit -m "added relevant files"
git push --set-upstream origin src

git worktree add -B master build origin/master

hugo -d build
cd build && git add .
git commit -m "Build output as of $(git log '--format=format:%H' master -1)"
git push
```
