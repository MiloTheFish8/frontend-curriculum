# Development tools

## Chrome Dev Tools
<details>
<summary>Shortcuts and tips</summary>

- Shortcuts (menu => shortcuts)
  - `ctrl + F` search (by any word)
  - `ctrl + shift + F` search across all sources
  - `tab` `tab + shift` step forward / back when adding changes
  - `H` hide chosen element of the html (adds `visibility: hidden;`)
  - `F2` to be able to edit html
  - `+` in styles will create a selector for the element
  - `shift + click` on color will change it's output
- `document.body.contentEditable = true;`
- can change sizes in the block with metrics
- in the device emulation can pick pixel density
- settings => coverage lets to see all the rules, which are not applied to the page

</details>

<details>
<summary>Elements tab</summary>

- last selected element has `== $0` added, browser creates this variable to access from the Console tab: print `$0` or `console.dir($0);`

</details>

<details>
<summary>Accessibility</summary>

- [ ] [Emulate vision deficiencies in DevTools](https://addyosmani.com/blog/emulate-vision-deficiencies-devtools/)

</details>

<details>
<summary>Block the request</summary>

- Network - resource - block request

</details>

<details>
<summary>Service Workers</summary>

- Application => Service Worker

</details>

<details>
<summary>Learn more</summary>

- [Learn How To Debug JavaScript with Chrome DevTools](https://codeburst.io/learn-how-to-debug-javascript-with-chrome-devtools-9514c58479db)

</details>

## Git and GitHub
<details>
<summary>How to setup git on mac or win?</summary>

- download git (both mac and win)
- download terminal
- for ru version (if needed): `environment` => `set LC_ALL=ru_RU.UTF-8` and `set LANG=ru_RU.UTF-8`

</details>

<details>
<summary>What are git line endings (and how to setup)?</summary>

- set inside `.gitattributes` file
- `*.md text` for text file to be converted `CRLF` (win) => `LF` (macOS, linux)
- `*.png binary` for `-text -diff` macros

</details>

<details>
<summary>How to config git?</summary>

```bash
git config --global user.name "<name>"
git config -g user.email "<email>"

# stored in the user's dir .gitconfig file path: ~/.gitconfig
git config --list
cat ~/.gitconfig
```

</details>

<details>
<summary>How to init repository with git?</summary>

```bash
# to add git to current folder
git init
```

</details>

<details>
<summary>How to use help in git?</summary>

```bash
git help <command>
```

</details>

<details>
<summary>How to check status?</summary>

```bash
git status
```

</details>

<details>
<summary>How to stage files for commit (index)?</summary>

```bash
# dir current add to index files for commit
git add .
# add particular file(s)
git add <path-to-file>
```

</details>

<details>
<summary>How to add, rename, checkout, show a commit?</summary>

```bash
# creates a save
git commit -m "<message>"
# to correct the last commits message (amend changes hash)
git commit --amend -m "<message>"
# switches to commit, shows log till this commit
git checkout <commit hash>
# to get back to the last commit in the branch
git checkout master
# shows commit file content (info about commit) -p readable format
git cat-file -p <commit hash>
# to show the changes in the commit
git show <commit hash>
```

</details>

<details>
<summary>How to get what changed?</summary>

```bash
# not staged
git diff
# staged
git diff --staged
# compare the file to another branch (same file)
git diff <branch name> -- <file name>
# to show the changes of the commit
git show <commit hash>
```

</details>

<details>
<summary>How to work with commits log?</summary>

```bash
# history
git log
git log --oneline
# shows the whole log (all the branches)
git log --all
git log --graph
# shows only 1/2/3/4/... last commits
git log -1<2/3/4...>
```

</details>

<details>
<summary>How to restore some file to some commit if all the changes are already commited?</summary>

```bash
# returns and stages
git checkout <commit-hash> path/to/file.js
git commit -m "<message>"
```

</details>

<details>
<summary>How to unstage staged file (not yet commited)?</summary>

```bash
git reset HEAD path/to/file.js
```

</details>

<details>
<summary>How to delete file and remove from git?</summary>

```bash
# these 2 commands remove file from commit and delete from folder
git rm <file>
git commit --amend --no-edit
```

</details>

<details>
<summary>How to remove file from git but save the changes?</summary>

```bash
# these 2 commands remove file from commit and keep unstaged in folder
# file will be both delete (staged) and untracked
git rm --cached <file>
git commit --amend --no-edit
```

</details>

<details>
<summary>Git commands (general)</summary>

```bash
# unstage a file but leave its actual changed untouched
git restore --staged <file name>
# for not commited, reset file to last commit, 
# even if the file was deleted, can't reverse this command
# discard your local changes in a file
git checkout <file>
git restore <file name>
# undo all the local changes in the working copy
git restore .
# resets file to the state in the commit
git checkout <commit hash> <file>
git restore --source <commit hash> <file name>
# to undo the last commit with getting changes back to unstaged
# --mixed changes are not being discarded
# HEAD~1 the commit before the last one
git reset --mixed HEAD~1
```

</details>

<details>
<summary>How to create a branch?</summary>

- `HEAD` indicates current state (where we currently are)
- when we create a new commit in a branch, the pointer jumps to the last commit
```bash
# or without hash for current commit, creates a pointer to commit
git checkout -b <branch name> [<commit hash>]
```

</details>

<details>
<summary>How to switch to another branch and back?</summary>

```bash
# to switch branch
git checkout <branch name>
# new command to replace the checkout
git switch <branch name>
# switch back to previously active branch
git switch -
```

</details>

<details>
<summary>How to merge branches?</summary>

```bash
# creates a merge commit, the pointer will be current branch
git merge <branch to merge> -m "<message>"
```

</details>

<details>
<summary>How to add a remote repository (and push and check added)?</summary>

```bash
# to link remote and local repos
git remote add origin <git@github.com:mary/repo-name.git>
# shows remote repos
git remote -v
git push -u origin master
```

</details>

<details>
<summary>How to push from one to another branch (also to change the branch name)?</summary>

```bash
git push origin <local-branch-to-push>:<where-to-push>
# to rename current local branch
git branch -m <new-branch-name>
```

</details>

<details>
<summary>How to delete the branch from the remote repository?</summary>

```bash
# to remove branch (nothing to branch to delete)
git push :<where-to-push>
```

</details>

<details>
<summary>How to get all the changes in all branches from the remote repository?</summary>

```bash
# to get all branches from repo
git fetch origin
```

</details>

<details>
<summary>How to create a new branch from an existing one?</summary>

```bash
# to create a new branch from existing pointer
git checkout -b <new-branch-name> origin/<branch-name>
```

</details>

<details>
<summary>How to link the current branch to another one (and show the existing links)?</summary>

```bash
# to link current branch to repo branch
git branch --set-upstream-to=origin/<name>
# to show links between branches
git branch -vv 
```

</details>

<details>
<summary>How to create a new SSH-key?</summary>

- store private key only on your computer
- load public key to repo
```bash
# creates a folder in user's folder, create an SSH key in this folder
mkdir ~/.ssh
# switch to folder
cd ~/.ssh
# -t rsa - key type
# -b 4096 - key length (bit)
ssh-keygen -t rsa -b 4096 -C "<email@email.com>"
# enter the key name
# enter password
# copy content to github
cat <key>.pub
# to check if the key works
ssh -T -i ~/.ssh/<key> git@github.com
# permission denied?
ssh -T git@github.com
# for settings (also using the appropriate private key)
~/.ssh/config
# add to the config file
Host github.com
    IdentityFile ~/.ssh/key
```

</details>

<details>
<summary>Learn more</summary>

- [Git Book](https://git-scm.com/book/en/v2)
- [Git How To](https://githowto.com/)
- [Основные команды для работы с Git и GitHub через консоль](https://github.com/ivan1kazantsev/dev-helper/tree/master/cmdline/git)
- [gitignore](https://docs.github.com/en/github/using-git/ignoring-files)
- [gitattributes](https://git-scm.com/docs/gitattributes)
- [Шпаргалка по Git. Решение основных проблем](https://htmlacademy.ru/blog/boost/frontend/first-aid-git)
- [Работа с Git через консоль](https://htmlacademy.ru/blog/boost/frontend/git-console)

</details>

<details>
<summary>Practice</summary>

- [Learn Git Branching](https://learngitbranching.js.org/)

</details>

## Terminal
<details>
<summary>Common commands</summary>

```bash
# full path to current dir
pwd
# change dir
cd
# to previous folder
cd -
# creates a dir or file
mkdir name
touch name

ls <path/to>
# vertically
ls -1
# +hidden
ls -a
ls -1 -a
# or instead of . add path to open dir or file
open .
start .
# shows the content
cat <file>
```

</details>

## Dev Servers

## Bundlers

## Linters
<details>
<summary>Learn more</summary>

- [Getting Started with ESLint](https://eslint.org/docs/user-guide/getting-started)
- [ES Lint configuring](https://eslint.org/docs/user-guide/configuring)
- [ES Lint rules](https://eslint.org/docs/rules/)
- [ES Lint preset configs](https://www.npmjs.com/search?q=eslint-config)

</details>