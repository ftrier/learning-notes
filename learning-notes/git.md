# Git Cheat Sheet

## Configuration
```sh
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
```

## Basic Commands
```sh
git init                # Initialize a new repository
git clone <url>         # Clone a repository
git status              # Show status of changes
git add <file>          # Stage file(s)
git commit -m "msg"     # Commit staged changes
git log                 # Show commit history
```

## Branching
```sh
git branch              # List branches
git branch <name>       # Create new branch
git checkout <name>     # Switch branch
git checkout -b <name>  # Create and switch branch
git merge <name>        # Merge branch into current
```

## Remote Repositories
```sh
git remote -v                   # List remotes
git remote add origin <url>     # Add remote
git push origin <branch>        # Push branch
git pull origin <branch>        # Pull changes
git fetch                       # Fetch from remote
```

## Undoing Changes
```sh
git checkout -- <file>      # Discard changes in file
git reset HEAD <file>       # Unstage file
git revert <commit>         # Revert a commit
git reset --hard <commit>   # Reset to commit (DANGEROUS)
```
## Rebasing and Merging

> **Golden Rule:** Never rewrite public history. Avoid rebasing or force-pushing branches that others may have pulled.

```sh
git rebase <branch>         # Rebase current branch onto <branch>
git rebase -i <commit>      # Interactive rebase
git merge <branch>          # Merge <branch> into current branch
```

## Stashing
```sh
git stash              # Stash changes
git stash apply        # Apply stashed changes
```

## Useful Tips
* `.gitignore` to exclude files
* `git diff` to see changes
* `git tag <tag>` to tag commits

## Best Practices

* Commit often with clear, descriptive messages.
* Use branches for features, fixes, and experiments.
* Pull and fetch regularly to stay up to date.
* Review changes before committing (`git diff`).
* Avoid force-pushing to shared branches.
* Keep your main branch deployable.
* Resolve conflicts promptly and carefully.
* Use `.gitignore` to avoid committing sensitive or unnecessary files.
* Clean up merged branches to keep the repository tidy.
* Backup your repository by pushing to remote regularly.

## Merge vs Rebase

### Merge
```
A---B---C feature

D---E---F main
```
After merging `feature` into `main`:

```
A---B---C feature
            \
D---E---F-----G main (merge commit)
```

### Rebase

```
A---B---C feature

D---E---F main
```
After rebasing `feature` onto `main`:

```
D---E---F---A'---B'---C' feature
             (rebased)
```

