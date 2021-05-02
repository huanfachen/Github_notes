# Notes on Github

## Author: Huanfa Chen

## References

- [Basic tutorial on Github](http://swcarpentry.github.io/git-novice/)
- [Advanced on Github: My Git Workflow by Oliver Steele](https://blog.osteele.com/2008/05/my-git-workflow/)

## Diagram

![img](C:\Users\Huanfa Chen\Documents\GitHub\Github_notes\git-transport.png)

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
- 
- `git push -u`
  - This option is synonymous with the `--set-upstream-to` option for the `git branch` command, and is used to associate the current branch with a remote branch so that the `git pull` command can be used without any arguments. To do this, simply use `git push -u origin master` once the remote has been set up.

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
  - `origin`: the default shortname that Git uses for a remote repository when you clone that remote repository. It refers to a URI, like git@...
  - `remote`: a remote is a copy of the repository that is hosted somewhere else. There can be multiple remote
  - `master`: the default branch

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

- How to undo `git add a.txt` ?

  - `git checkout a.txt` will undo local changes (local copy still modified)
  - `git reset HEAD foo.txt` will remove from staging area (local copy still modified)
  - `git reset HEAD~` will undo commit??

- How to set up the SSH for Github and use a password manager to remember passwords?

- The Owner pushed commits to the repository without giving any information to the Collaborator. How can the Collaborator find out what has changed with command line? And on GitHub?

  - On the command line, the Collaborator can use `git fetch origin master` to get the remote changes into the local repository, but without merging them. Then by running `git diff master origin/master` the Collaborator will see the changes output in the terminal.
  - 

