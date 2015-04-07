# Pro Git

**date: 20140730-15:39**
**tags: git software-development**
**Chacon, Scott, Pro Git, 2009**

# Chapter 1 Getting Started

### Think as Data

The major difference between Git and any other VCS(subversion and friends included) is the way Git thinks about its data. 

Git thinks of its data more like a set of snapshots of a mini file system. Every time you commit, or save the state of your project in Git, it basically takes a picture of what your files look like at that moment and stores a reference to that snapshot.

### SHA-1 hash for Checksum

The mechanism that Git uses for this check-summing is called a SHA-1 hash. This is a 40-character string composed of hexadecimal characters (0–9 and a–f) and calculated based on the contents of a file or directory structure in Git. A SHA-1 hash looks something like this:

### Only Add Data

nearly all of actions in Git only add data to the Git database.

### Three Main States

 - committed : data is safely stored in your local database
 - modified : you've changed the file but have not committed it to your database yet
 - staged : you have marked a modified file in its current version to go into your next commit snapshot

### Normal Git Workflow

modify file in local directory --> stage files, adding snapshots to your staging area --> commit files in staging area and stores that snapshot permanently to Git directory

# Chapter 2 Git Basics

##### Git Clone

```
$ git clone git://github.com/username/projectname.git
$ git clone git://github.com/username/projectname.git localdirectory
```

##### Check Status

this command is to determine which file are in which state.

```
$ git status
```

##### Staging Modified Files

```
$ git add [file]
```

Git stage the file exactly as it is when you run <code>git add</code>. If you modify a file after staging, you have to run <code>git add</code> again.

##### Ignoring Files

.gitignore is a log file listing patterns that match those files to be ignored.

```
$ git git-ignore [file]
```

example of .gitignore

```
# a comment this is ignored
*.a # no .a files
!lib.a # but do track lib.a, even though you’re ignoring .a files above
/TODO # only ignore the root TODO file, not subdir/TODO
build/ # ignore all files in the build/ directory
doc/*.txt # ignore doc/notes.txt, but not doc/server/arch.txt
`

##### Viewing Staged and Unstaged Changes

`git diff --cached` to see what you've staged that will go into your next commit.

```
$ git diff
$ git diff --cached 
or
$ git diff --staged
```

##### Committing Changes

```
$ git commit
$ git commit -m "leave comments here" // if comments leave as blank, aborting commit.
$ git commit -a -m "leave comments here" //skip stagging (git add part)
```

##### Removing Files

To remove a file from Git, you have to remove it from your tracked file (more accurately removing it from your staging area) and then commit.

To keep the file in your working tree but remove it from your staging area, you can:
 - add it to .gitignore
 - use `--cached` option

```
$ git rm [file]
$ git rm --cached [file]
```

pass pattern: note \ is necessary because Git does its own filename expansion in addition to your shell's filename expansion. this command removes all files that have the .log extension in the log/ directory.

```
$ git rm log/\*.log
$ git rm \*~  // removes all files that end with .
```

##### Moving Files

```
$ git mv [file_from] [file_to]
```

##### Viewing the Commit History

```
$ git log
$ git log p -2  // -p shows the diff introduced, -2 limits the output to only the last two entries
$ git log --stat  // abbreviated stats
```

`--pretty` changes the log output to formats, other options inlcuding *short*, *full*, *fuller*. Use *format* to specify your own log output format.

```
$ git log --pretty=online
$ git log --pretty=format:"%h - %an, %ar : %s"
```

`--since` and `--until` are useful for time-limiting options.

##### Changing Last Commit

```
$ git commit --amend
```

##### Unstaging a Staged File

```
$ git reset HEAD [file]
```

###### Unmodifying a modified file

```
$ git checkout -- file  // to discard changes in working directory
```

### Working with Remotes

remote repositories are versions of your project that are hosted on the Internet or network somewhere.

##### Displaying Remote Repositories

```
$ cd [directory]
$ git remote -v
```

##### Adding Remote Repositories

```
$ git remote add [shortname] [url]
```

##### Fetch and Pulling Remote

```
$ git fetch [remote-name]
$ git fetch [shortname]  // if you have add remote repositories
```

##### Pushing Remote

```
$ git push origin master  // push your master branch to your origin server
```

##### Inspecting Remote

```
$ git remote show origin
```

##### Removing and Renaming Remotes

```
$ git remote rename [old_shortname] [new_shortname]  // rename remote
$ git remote rm [shortname]  // remove remote
```

##### Tagging


# Chapter 3 Git Branching

killer feature

Branching means you diverge from the main line of development and continue to do work without messing with that main line.

##### Gib Object Type

This part of notes are taken from ["O'Reilly: Version Control with Git"](http://shop.oreilly.com/product/9780596520137.do).

**Blob**

Each version of the file is represented as a *blob*. Blob, a contraction of "binary large object", is a term that's commonly used in computing to refer to some variable or file that can contain any data and whose internal structure is ignored by the program.

**Tree**

A *tree* object represents one level of directory information. It records blob identifiers, path names, and a bit of metadata for all the files in one directory. It can also recursively reference other (sub)tree objects and thus build a complete hierarchy of files and subdirectories.

**Commits**

A *commit* object holds metadata for each change introduced into repository, including the author, committer, commit date, and log message. Each commit points to a tree object that captures, in one complete snapshot, the state of the repository at the time the commit was performed.

**Tags**

A tag object assigns an arbitary yet presumably human readable name to a specific object, usually a commit.

-----

A branch in Git is simply a light weight movable pointer to one of commits. The default branch name in Git is master.

**Creating New Branch**

```
$ git branch [new_branch]
```

Git keeps a special pointer `HEAD`. This is a pointer to the local branch you're currently on. To switch to an existing branch, you run the `git checkout` command.

```
$ git checkout [branch_switch_to]
```

**Merging Branch**

 - First checkout the branch you want to merge
 - Then run `git merge`

```
$ git checkout [branch_to_merge]
$ git merge [branch_merge_from]
```

After merging, your master branch and your merged-from branch point to the same place.

**Deleting Branch**

```
$ git branch -d [branch_to_delete]
```

##### Basic Merge

If merge branches have more than one parents, Git calculate for best common ancestor and automatcially create a new commit object that contains the merged work(merge commit).

##### Basic Merge conflict

If merge conflict, Git doesn't automatically create a new merge commit. Run `git status` to check conflicts.

To resolve conflicts, you can use `git mergetool` to open graphical tool.

##### Branch Management

```
$ git branch  // listing of your current branches, * prefixes master branch.
$ git branch -v  // to see last commit on each branch
$ git branch --merged/--no-merged  // to see which branches are already merged into the branch you're on.
```

##### Branches Work Flow

Many Git developers have a workflow that embraces this approach, such as having
only code that is entirely stable in their master branch possibly only code that has been or will be released. They have another parallel branch named develop or next that they work from or use to test stability it isn’t necessarily always stable, but whenever it gets to a stable state, it can be merged into master. It’s used to pull in topic branches (short-lived branches, like your earlier iss53 branch) when they’re ready, to make sure they pass all the tests and don’t introduce bugs.

 - master branch
 - develop branch
 - test branch
 - topic branch

# Chapter 4 Git on the Server

### The protocols

Git has four major network protocols to transfer data:
 - Local
 - Secure Shell (SSH)
 - Git
 - HTTP

##### Local Protocol

The remote repository is in another directory on disk. 

To add local repository

```
$ git remote add local_proj /opt/git/project.git
```

##### SSH Protocol

Most common. SSH access to servers is already set up in most places. SSH is also the only network-based protocol that you can easily read from and write to.

To clone a Git repository over SSH:

```
$ git clone ssh://user@server:project.git
$ git clone user@server:project.git  // git assumes ssh if you aren't explicit
```

##### Git Protocol

Git repository is available for everyone to clone or it isn't. This means that there is generally no pushing over this protocol.

##### HTTP/S Protocol