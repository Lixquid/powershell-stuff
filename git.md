<h1 align="center">Git for Dummies</h1>

[↖︎ Back to Index](index.html)

> Anything surrounded in `<angle>` brackets are required, and must be filled in.
> 
> Anything surrounded in `[square]` brackets are optional.

## Reference Workflow

#### New

1. `git init` OR `git clone <repo>`

#### Doing Work

1. `git pull`
2. *Make changes to files*
3. `git add -A`
4. `git status`
5. `git commit -m "<message>"`
6. `git push`

#### Resolving Merge Conflicts

1. `git pull`
2. `git status`
3. *Edit files with merge conflicts*
4. `git add -A`
5. `git status`
6. `git commit -m "Resolved merge conflict"`
7. `git push`

## Simple

- `git init`: Create a new empty repository.
- `git status`: Get the current status of the repository.

- `git add <filename> [filename2]`: Add a file to the index.
- `git add -A`: Add everything to the index.
- `git reset <filename>`: Removes a file from the index.
- `git reset`: Removes everything from the index.

- `git commit -m "<message>"`: Packages everything in the index into a commit.

## Advanced

- `git log`: Get a list of commits, including their hashes.

- `git checkout <commit_hash>`: Changes working directory to look like it did
  at the point in time that commit was created.
- `git checkout master`: Reverts to most up-to-date files.

## Social

- `git clone <URL>`: Pulls down a copy of a repo onto your local machine.

- `git pull`: Fetches any changes made to the remote repo, and updates your
  local repo.
  
  **Warning**: You may encounter something called a *merge conflict*; see
  section *Merge Conflict* below.
- `git push`: Pushes any changes to your local repository to the remote repo.
  You can only do this if you have all changes from the remote repo in your
  local repo (usually by `git pull`ing first).

- `git stash`: Hides all changes since your most recent commit into a temporary
  commit, leaving you with a clean working directory to `checkout`, etc.
- `git stash pop`: Re-applies any changes hidden by `git stash` allowing you
  to continue working.

## Merge Conflict

``` shell
$ git pull
remote: Counting objects: 3, done.
remote: Total 3 (delta 0), reused 0 (delta 0)
Unpacking objects: 100% (3/3), done.
From remote
   d1297bd..7995d4b  master     -> origin/master
Auto-merging file
CONFLICT (content): Merge conflict in file
Automatic merge failed; fix conflicts and then commit the result.
```

Oh no! Merge conflict! Everything is on fire and the apocalypse is here. What
do the numbers mean Mason?!

Don't Panic™. A "Merge Conflict" occurs when two people have made changes to
the same file, and Git can't figure out how to merge them, hence the conflict.

Typically, it's also quite trivial to solve. The files that have both been
edited can be seen with `git status`:

``` shell
$ git status
On branch master
Your branch and 'origin/master' have diverged,
and have 1 and 1 different commit each, respectively.
  (use "git pull" to merge the remote branch into yours)
You have unmerged paths.
  (fix conflicts and run "git commit")

Unmerged paths:
  (use "git add <file>..." to mark resolution)

	both modified:   file

no changes added to commit (use "git add" and/or "git commit -a")
```

In this example, both people have modified `file`. Inspecting `file` shows the
changes:

``` shell
$ cat file
echo "Hello"
<<<<<<< HEAD
echo "Wonderful"
=======
echo "Magical"
>>>>>>> 7995d4b95a956ec658fc8d81cf6ca00f9e6112a4
echo "World!"
```

Everything between the `<<<<<<<` and `>>>>>>>` is stuff Git is having trouble
with. The changes between `HEAD` and `=======` is everything in your commit,
and everything between `=======` and the other `>>>>>>>` is changes in the
competing commit.

To resolve the problem, it's as simple as editing the file. Remove / move /
change the contents of the file as you see fit to resolve the issue. (Make sure
you remove the `<<<<<<<`, `=======`, and `>>>>>>>`!)

After the problem has been resolved, it's as simple as `git add`ing the changed
file to the index and creating another commit. This is a special commit known
as a *merge commit*, which is a commit with two parent commits. You can now
safely push your changes! (Unless someone's made some changes during this time,
in which case, go to the top of the section and repeat.)

<link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/4.0.0-alpha.5/css/bootstrap.min.css" integrity="sha384-AysaV+vQoT3kOAXZkl02PThvDr8HYKPZhNT5h/CXfBThSRXQ6jW5DO2ekP5ViFdi" crossorigin="anonymous">
<script src="https://maxcdn.bootstrapcdn.com/bootstrap/4.0.0-alpha.5/js/bootstrap.min.js" integrity="sha384-BLiI7JTZm+JWlgKa0M0kGRpJbF2J8q+qreVrKBC47e3K6BW78kGLrCkeRX6I9RoK" crossorigin="anonymous"></script>
