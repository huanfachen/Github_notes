# Notes on Github

## Author: Huanfa Chen

## References

- [Basic tutorial on Github](http://swcarpentry.github.io/git-novice/)
- [Excellent lecture on open science](http://swcarpentry.github.io/git-novice/10-open/index.html)
- [Advanced on Github: My Git Workflow by Oliver Steele](https://blog.osteele.com/2008/05/my-git-workflow/)
- [Better Explained: Learning Git](https://betterexplained.com/articles/aha-moments-when-learning-git/)

## Diagram

![img](https://github.com/huanfachen/Github_notes/raw/main/git-transport.png)

Credit [here](https://images.osteele.com/2008/git-transport.png)

## Commands

- `git log`
  - show the project’s history of using `git commit`
- `git diff [file]`
  - show differences of a file in workspace and staging area. If a file has been git added, `git diff` will show nothing
- Explaining git as taking snapshots of changes over the life of a project
  - `git add` specifies what will go in a snapshot (putting things in a staging area), `git commit` then actually takes the snapshot and makes a permanent record of it (as a commit) and put the snapshot in the local repo
  - It is always better to explicitly add things to the staging area instead of using `git add .` or `git commit -a`.
- Directories in Git
  - Git does not track directories on their own, only files within them. This is why you will see `.gitkeep` files in otherwise empty directories. These files are not special and their sole purpose is to populate a directory so that Git adds it to the repo.
- `git push -u`
  - This option is synonymous with the `--set-upstream-to` option for the `git branch` command, and is used to associate the current branch with a remote branch so that the `git pull` command can be used without any arguments. To do this, simply use `git push -u origin master` once the remote has been set up.
- `git checkout`
  - Updates files in the working tree (aka workspace) to match the version in the index or the specified tree. If no pathspec was given, *git checkout* will also update `HEAD` to set the specified branch as the current branch.

## Repos

- Rules
  - A local Git repository can be connected to one or more remote repositories.
- commands
  - **git push origin master**: push to the master branch of the repo of origin
  - **git remote:** list the shortnames of each remote handle you've specified
  - **git remote add [name] [url]**: to add a new remote
  - **git remote remove [name]**: removes a remote. Note that it doesn’t affect the remote repo at all. It just removes the link to it from the local repo.
  - **git remote set-url [name] [newurl]**: changes the URL
  - **git remote rename [oldname] [newname]**: changes the local alias by which a remote is known
- names of repo
  - `origin`: the default shortname that Git uses for a remote repository when you clone that remote repository. It refers to a URI, like git@.… If you use `git clone`, the `origin` would be automatically set up.
  - `remote`: a remote is a copy of the repository that is hosted somewhere else. There can be multiple remote
  - `master`: the default branch
  - `HEAD`: a file for storing current branch info (or the hash value of the latest commit). If you use `checkout` to change the branch, HEAD will change. To see what HEAD points to, you can use `cat .git/HEAD`. Usually it is `refs/heads/master`, which is a file that normally has the hash value of the latest commit of master.
- Seeing branches as virtual directories in the .git folder
  - `git checkout master`: switch to master branch (`cd master`)
  - `git branch dev`: create new branch from existing (`cp * dev`) but not changing branches. Like Save As. You still need to `cd` with `git checkout dev`
  - `git merge dev`: (when in master) pull in changes from dev (`cp dev/* .`)
  - `git branch`: list all branches (`ls`)
  - `git branch -a`: list all local and remote branch
  - A good inner dialogue: **change to dev directory (checkout)... make changes... save changes (add/commit)... change to master directory... copy in changes from dev (merge)**.
  - 

## Questions

- `Syntax in .gitignore. Can I use regular expression?`

  - gitignore does not support full regular expressions. It only supports [unix fnmatch](https://man7.org/linux/man-pages/man3/fnmatch.3.html) style patterns.
  - If you want to ignore files in a folder `result`, use `result/` in .gitignore
  - If you simply use `result`, Git treats it as a shell glob pattern and checks for a match against the pathname relative to the location (not clear)
  - we can check the status of ignored files using **git status \-\-ignored**
  - If you really want to git add a file without changing the .gitignore, you can use `git add -f file_name`

- How would you ignore all `.dat` files in your root directory except for `final.dat`?

  - ```
    *.dat
    !final.dat
    ```

  - The rules are executed in the order.

  - If you have previously committed .dat files before adding the .gitignore rules, these .dat files will not be ignored. Only future additions of `.dat` files will be ignored

- How to undo local changes before adding?

  - `git checkout a.txt` will undo local changes and restore file from staging area
  
- How to undo `git add a.txt` but keeping the local changes?

  - `git reset HEAD foo.txt` will remove from staging area (local copy still modified)

- If I delete a file using `git rm` by mistake, how can I get it back from staging area?

  - `git rm` will remove file from current virtual directory and index
  - Use `git checkout HEAD file`. This command will restore file & index from HEAD

- If I delete a file using `rm a.txt` by mistake, how can I get it back?

  - Use `git checkout a.txt`

- How to undo `git commit`

  - `git reset --soft HEAD^`: undo commit & keep changes in the working tree
  - `git reset --hard HEAD^`: undo commit and reset working tree to the last commit

- How to set up the SSH for Github and use a password manager to remember passwords?

- **The Owner pushed commits to the repository without giving any information to the Collaborator. How can the Collaborator find out what has changed with command line? And on GitHub?**

  - On the command line, the Collaborator can use `git fetch origin master` to get the remote changes into the local repository, but without merging them. Then by running `git diff master origin/master` the Collaborator will see the changes output in the terminal.
  - On GitHub, the Collaborator can go to the repository and click on “commits” to view the most recent commits pushed to the repository.

- Suggestions on resolving conflicts?

  - Pull from upstream more frequently, especially before starting new work
  - Use topic branches to segregate work, merging to master when complete
  - Make smaller more atomic commits
  - Where logically appropriate, break large files into smaller ones so that it is less likely that two authors will alter the same file simultaneously

- **How to resolve a conflict regarding a text file when your `git push origin main` fails due to the newer updates on the origin? You want to merge the updates of origin first and then update your changes** 

  - `git pull origin main`: merge the newer updates from origin to local repo. Note that this will create a commit and you would need to input the message.
  - Then, `git push origin main`
  - Note that the version control system does not allow people to overwrite each other’s changes blindly, but highlights conflicts so that they can be resolved.

- What if the conflict happens to a binary file `mars.png` which can’t be merged?

  - There are two copies of a.png. If you want to use the local version (called HEAD), use the following.

    - `git checkout HEAD mars.png`
    - `git add mars.png`
    - `git commit -m ‘Use local version of mars.png’`

  - We can also keep both images by renaming, removing, and adding them

    - ```
      git checkout HEAD mars.jpg
      git mv mars.jpg mars-surface.jpg
      git checkout 439dc8c0 mars.jpg
      mv mars.jpg mars-sky.jpg
      git rm mars.jpg
      git add mars-surface.jpg
      git add mars-sky.jpg
      git commit -m "Use two images: surface and sky"
      ```

- **Conflicts can also be minimized with project management strategies**
  - Clarify who is responsible for what areas with your collaborators
  - Discuss what order tasks should be carried out in with your collaborators so that tasks expected to change the same lines won’t be worked on simultaneously
  - If the conflicts are stylistic churn (e.g. tabs vs. spaces), establish a project convention that is governing and use code style tools (e.g. `htmltidy`, `perltidy`, `rubocop`, etc.) to enforce, if necessary
- 

