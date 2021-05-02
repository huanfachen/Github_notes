# Notes on Github

## Author: Huanfa Chen

## References

- [Basic tutorial on Github](http://swcarpentry.github.io/git-novice/)
- [Advanced on Github: My Git Workflow by Oliver Steele](https://blog.osteele.com/2008/05/my-git-workflow/)

## Diagram

![img](C:\Users\Huanfa Chen\Documents\GitHub\Github_notes\git-transport.png)



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

