# git.plugin.zsh

> A git aliases plugin for zsh

## Installation

### Znap

I recommend using [Znap](https://github.com/marlonrichert/zsh-snap) or installing the plugin manually. You can also install it using any 3rd-party framework or plugin manager you like, but I won't document that here.

Just add this to your .zshrc file:

`znap source eckertalex/git.plugin.zsh`

To update, run `znap pull`.

### Oh My Zsh

1. Clone the repository:

   `git clone --depth=1 https://github.com/eckertalex/git.plugin.zsh.git ${ZSH_CUSTOM:-$HOME/.oh-my-zsh/custom}/plugins/git`

2. Include it in your `~/.zshrc`

   `plugins=(... git)`

## Default branch name

`git.plugin.zsh` respects `init.defaultBranch` setting that was [introduced in git 2.28](https://github.blog/2020-07-27-highlights-from-git-2-28/#introducing-init-defaultbranch).
The order for resolving the default branch name is as follows:

1. `init.defaultBranch` if it is set and the branch exists
2. `main` if it exists
3. `master` as fallback

## Usage

### Status

| Alias | Command         | Description                                  |
| ----- | --------------- | -------------------------------------------- |
| `gst` | `git status`    | Show the working tree status                 |
| `gss` | `git status -s` | Show the working tree status in short-format |

### Branch

| Alias   | Command                                     | Description                                                     |
| ------- | ------------------------------------------- | --------------------------------------------------------------- |
| `gb`    | `git branch -vv`                            | Show all local branches with last commit message                |
| `gba`   | `git branch -a -v`                          | Show all branches with last commit message                      |
| `gbd`   | `git branch -d`                             | Delete branch                                                   |
| `gbd!`  | `git branch -D`                             | Force delete branch                                             |
| `gbage` |                                             | list local branches and display their age                       |
| `gbsup` | git set upstream to origin/_current-branch_ | Set upstream to origin/_current_branch_                         |
| `gbmv`  |                                             | Rename _old_ branch to _new_ branch, including in origin remote |

### Local Files

| Alias   | Command                           | Description                                                                                                  |
| ------- | --------------------------------- | ------------------------------------------------------------------------------------------------------------ |
| `ga`    | `git add`                         | Add file contents to the index                                                                               |
| `gaa`   | `git add --all`                   | Add all file contents to the index                                                                           |
| `gau`   | `git add --update`                | Update the index just where it already has a matching entry                                                  |
| `gapa`  | `git add --patch`                 | Interactively choose hunks of patch between the index and the work tree                                      |
| `grm`   | `git rm`                          | Removes file from the working tree and the index                                                             |
| `grmc`  | `git rm --cached`                 | Removes file from the index                                                                                  |
| `grs`   | `git restore`                     | _Discard_. Restore the worktree for matching paths                                                           |
| `grss`  | `git restore --source`            | Restore from a different commit                                                                              |
| `grst`  | `git restore --staged`            | _Unadd_. Reset the index for matching paths. Same as `git reset`                                             |
| `grst!` | `git restore --staged --worktree` | _Unadd and discard_. Reset the index and restore the worktree for matching paths. Same as `git reset --hard` |

### Clean

| Alias      | Command                            | Description                                                                                                    |
| ---------- | ---------------------------------- | -------------------------------------------------------------------------------------------------------------- |
| `gclean`   | `git clean -di`                    | Delete all untracked files. Ignored files will be untouched                                                    |
| `gclean!`  | `git clean -dfx`                   | Delete all untracked and ignored files                                                                         |
| `gclean!!` | `git reset --hard; git clean -dfx` | _Unadd, discard, and clean_. Reset the index, restore the worktree, and delete all untracked and ignored files |

### Reset

| Alias  | Command                   | Description                                                     |
| ------ | ------------------------- | --------------------------------------------------------------- |
| `grh`  | `git reset HEAD~1`        | _Uncommit_. Remove last commit and keep worktree                |
| `grh!` | `git reset --hard HEAD~1` | _Uncommit and discard_. Remove last commit and discard worktree |

### Commit

| Alias   | Command                                | Description                                                   |
| ------- | -------------------------------------- | ------------------------------------------------------------- |
| `gc`    | `git commit -v`                        | Commit changes in index                                       |
| `gc!`   | `git commit -v --amend`                | Amend last commit                                             |
| `gcn!`  | `git commit -v --amend --no-edit`      | Amend last commit, don't edit commit message                  |
| `gca`   | `git commit -v -a`                     | Commit all changes                                            |
| `gca!`  | `git commit -v -a --amend`             | Amend last commit with all changes                            |
| `gcan!` | `git commit -v -a --no-edit --amend`   | Amend last commit with all changes, don't edit commit message |
| `gcv`   | `git commit -v --no-verify`            | Commit changes in index, don't run pre-push hook              |
| `gcav`  | `git commit -v -a --no-verify`         | Commit all changes, don't run pre-push hook                   |
| `gcav!` | `git commit -v -a --no-verify --amend` | Amend last commit with all changes, don't run pre-push hook   |
| `gcm`   | `git commit -m`                        | Commit changes in index with commit message                   |
| `gcam`  | `git commit -a -m`                     | Commit all changes with commit message                        |

### Checkout

| Alias  | Command                             | Description                                   |
| ------ | ----------------------------------- | --------------------------------------------- |
| `gco`  | `git checkout`                      | Switch branches or restore working tree files |
| `gcob` | `git checkout -b`                   | Swtich and create a new branch                |
| `gcom` | `git checkout (git_default_branch)` | Switch to default branch                      |
| `gco-` | Checkout previous                   | Switch to previous branch/commit              |
| `gsw`  | `git switch`                        | Switch branches                               |
| `gswc` | `git switch -c`                     | Switch an create and new branch               |
| `gswm` | `git switch (git_default_branch)`   | Switch to default branch                      |
| `gsw-` | `git switch (git_default_branch)`   | Switch to previous branch/commit              |

### Fetch

| Alias | Command                   | Description                                                                                        |
| ----- | ------------------------- | -------------------------------------------------------------------------------------------------- |
| `gf`  | `git fetch`               | Fetch objects and refs                                                                             |
| `gfa` | `git fetch --all --prune` | Fetch from all remotes, before fetching remove any remote-tracking references that no longer exist |
| `gfo` | `git fetch origin`        | Update the remote-tracking branches from origin                                                    |

## Push

| Alias   | Command                                   | Description                                      |
| ------- | ----------------------------------------- | ------------------------------------------------ |
| `gp`    | `git push`                                | Update remote refs along with associated objects |
| `gp!`   | `git push --force-with-lease`             | Force push                                       |
| `gpo`   | `git push origin`                         | Push to origin                                   |
| `gpo!`  | `git push --force-with-lease origin`      | Force push to origin                             |
| `gpv`   | `git push --no-verify`                    | Push, don't run pre-push hook                    |
| `gpv!`  | `git push --no-verify --force-with-lease` | Force push, run pre-push hook                    |
| `ggp`   | push origin _current-branch_              | Push current branch to origin                    |
| `ggp!`  | `ggp --force-with-lease`                  | Force push current branch to origin              |
| `ggpu`  | `ggp --set-upstream`                      | Push and set upstream                            |
| `gpoat` |                                           | push all + tags to origin                        |

### Pull

| Alias   | Command                         | Description                                                              |
| ------- | ------------------------------- | ------------------------------------------------------------------------ |
| `gpl`   | `git pull`                      | Fetch from and integrate with another repository or a local branch       |
| `ggpl`  | pull origin _current-branch_    | Pull current branch from origin                                          |
| `gplr`  | `git pull --rebase`             | Pull and reconcile by rebase                                             |
| `gplra` | `git pull --rebase --autostash` | Pull and reconcile by rebase, automatically create temporary stash entry |

### Diff

| Alias  | Command                                       | Description                                                |
| ------ | --------------------------------------------- | ---------------------------------------------------------- |
| `gd`   | `git diff`                                    | Show changes between commits, commit and working tree, etc |
| `gds`  | `git diff --stat`                             | Show diff with stats                                       |
| `gdc`  | `git diff --cached`                           | Show index diff                                            |
| `gdsc` | `git diff --stat --cached`                    | Show index diff with stats                                 |
| `gdt`  | `git diff-tree --no-commit-id --name-only -r` | list changed files                                         |
| `gdw`  | `git diff --word-diff`                        | Show word diff                                             |
| `gdwc` | `git diff --word-diff --cached`               | Show index word diff                                       |
| `gdto` | `git difftool`                                | Show changes using common diff tools                       |

### Log

| Alias    | Command                                                                                     | Description                                                         |
| -------- | ------------------------------------------------------------------------------------------- | ------------------------------------------------------------------- |
| `glo`    | `git log --pretty=format:'%C(yellow)%h %Cred%ad %Cblue%an%Cgreen%d %Creset%s' --date=short` | Shows one line commit log with short date                           |
| `glg`    | `git log --stat`                                                                            | Shows commit log with stats                                         |
| `glgg`   | `git log --graph`                                                                           | Shows commit log with a graph                                       |
| `glgga`  | `git log --graph --decorate --all`                                                          | Shows all commit logs with a graph                                  |
| `glom`   | `git log --oneline --decorate --color (git_default_branch)..`                               | Shows one line commit log since branching from _git_default_branch_ |
| `gcount` | `git shortlog -sn`                                                                          | Summarizes commit count by author                                   |

### Rebase

| Alias   | Command                                         | Description                                |
| ------- | ----------------------------------------------- | ------------------------------------------ |
| `grb`   | `git rebase`                                    | Reapply commits on top of another base tip |
| `grbi`  | `git rebase --interactive`                      | Rebase interactively                       |
| `grba`  | `git rebase --abort`                            | Abort the rebase                           |
| `grbc`  | `git rebase --continue`                         | Continue the rebase                        |
| `grbs`  | `git rebase --skip`                             | Skip the rebase                            |
| `grbm`  | `git rebase (git_default_branch)`               | Rebase with default branch                 |
| `grbmi` | `git rebase (git_default_branch) --interactive` | Rebase with default branch interactively   |

### Stash & Work in Progress

| Alias    | Command                 | Description                                                                                                                                    |
| -------- | ----------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------- |
| `gsta`   | `git stash`             | Stash the changes in a dirty working directory away                                                                                            |
| `gstd`   | `git stash drop`        | Remove a single stash entry from the list of stash entries                                                                                     |
| `gstl`   | `git stash list`        | List the stash entries that you currently have                                                                                                 |
| `gstp`   | `git stash pop`         | Remove a single stashed state from the stash list and apply it on top of the current working tree state                                        |
| `gsts`   | `git stash show --text` | Show the changes recorded in the stash entry as a diff between the stashed contents and the commit back when the stash entry was first created |
| `gwip`   |                         | commit a work-in-progress branch                                                                                                               |
| `gunwip` |                         | uncommit the work-in-progress branch                                                                                                           |

### Cherry-pick

| Alias  | Command                      | Description                                           |
| ------ | ---------------------------- | ----------------------------------------------------- |
| `gcp`  | `git cherry-pick`            | Apply the changes introduced by some existing commits |
| `gcpa` | `git cherry-pick --abort`    | Abort the cherry-pick                                 |
| `gcpc` | `git cherry-pick --continue` | Continue the cherry-pick                              |
| `gcps` | `git cherry-pick --skip`     | Skip the cherry-pick                                  |

### Bisect

| Alias  | Command            | Description                                                |
| ------ | ------------------ | ---------------------------------------------------------- |
| `gbs`  | `git bisect`       | Use binary search to find the commit that introduced a bug |
| `gbss` | `git bisect start` | Start bisecting                                            |
| `gbsb` | `git bisect bad`   | Mark commit as bad                                         |
| `gbsg` | `git bisect good`  | Mark commit as good                                        |
| `gbsr` | `git bisect reset` | Reset bisecting                                            |

### Remote

| Alias   | Command                   | Description                                     |
| ------- | ------------------------- | ----------------------------------------------- |
| `gr`    | `git remote -vv`          | Manage set of tracked repositories              |
| `gra`   | `git remote add`          | Add a remote                                    |
| `grmv`  | `git remote rename`       | Rename a remote                                 |
| `grpo`  | `git remote prune origin` | Deletes stale references associated with origin |
| `grrm`  | `git remote remove`       | Remove the remote                               |
| `grset` | `git remote set-url`      | Changes URLs for the remote                     |
| `grup`  | `git remote update`       | Fetch updates                                   |

### Tags

| Alias | Command              | Description                     |
| ----- | -------------------- | ------------------------------- |
| `gt`  | `git tag`            | Create, list, delete            |
| `gtl` | `git tag --list`     | List all tags                   |
| `gtd` | `git tag -d`         | Delete a tag                    |
| `gtv` | `git tag \| sort -V` | List all tags sorted by version |

### Miscellaneous

| Alias      | Command             | Description                                                     |
| ---------- | ------------------- | --------------------------------------------------------------- |
| `g`        | `git`               | The `git` command                                               |
| `gcl`      | `git clone`         | Clone a repository into a new directory                         |
| `gm`       | `git merge`         | Join two or more development histories together                 |
| `gbl`      | `git blame -b -w`   | Show what revision and author last modified each line of a file |
| `gignored` |                     | list temporarily ignored files                                  |
| `gcf`      | `git config`        | Get and set repository or global options                        |
| `gcfl`     | `git config --list` | List all config entries                                         |

## Changelog

### 2023-02-21

- Initial commit
