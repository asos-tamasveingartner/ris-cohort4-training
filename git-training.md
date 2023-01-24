# ASOS Cohort Git Training

## Part 2 - Getting a Copy of a Repository and Looking Inside

### What We'll Cover

Here are the commands we'll cover in this section, along with a one-liner about what it does `git --help`:
- [`init`](https://git-scm.com/docs/git-init) - Create an empty Git repository or reinitialize an existing one
- [`clone`](https://git-scm.com/docs/git-clone) - Clone a repository into a new directory
- [`branch`](https://git-scm.com/docs/git-branch) - List, create, or delete branches
- [`log`](https://git-scm.com/docs/git-log) - Show commit logs
- [`show`](https://git-scm.com/docs/git-show) - Show various types of objects

### Commands In More Detail

#### `git init`

From the Git help page:

> This command creates an empty Git repository - basically a .git directory with subdirectories for objects, refs/heads, refs/tags, and template files. An initial branch without any
> commits will be created (see the --initial-branch option below for its name).<br/>
> ...

##### When Is It Used?

If we're starting a new project and want to use version control, then we use the command `git init`.

##### Tasks

1. Make a new directory on your computer and initialise a new git repository.
2. Inspect the `.git` folder that's been created.


#### `git clone`

From the Git help page:

> Clones a repository into a ***newly created directory***, creates ***remote-tracking branches*** for each branch in the cloned repository (visible using git branch --remotes), and creates and
> checks out an ***initial branch*** that is forked from the cloned repository’s currently active branch. </br></br>
> After the clone, a plain git ***fetch*** without arguments will update all the remote-tracking branches, and a git ***pull*** without arguments will in addition merge the remote master branch into
> the current master branch, if any (this is untrue when "--single-branch" is given; see below).<br/>
> ...

##### When Is It Used?

So you've realised that teamwork makes the dream work, and that sharing code via email, MS Teams or pen drives (or maybe even floppy disks!)
is a challenge in itself! 

One of your teammates has given you a link to some code on a remote repository, and they've asked you to help out. The first thing
that you need to do is to take a ***copy*** of their code, this is where `git clone` comes in!

Remember, it's a copy, so you're free to chop and change the code as you see fit!

##### Tasks

1. Clone this repository: https://github.com/Coveros/helloworld
2. Take a look in the `.git` folder. What differences do you see?


#### `git branch`

From the Git help page:

> If --list is given, or if there are no non-option arguments, existing branches are listed; the current branch will be highlighted in green and marked with an asterisk.<br/>
> Any branches checked out in linked worktrees will be highlighted in cyan and marked with a plus sign.<br/>
> Option -r causes the remote-tracking branches to be listed, and option -a shows both local and remote branches. <br/>
> ...<br/>
> The -c and -C options have the exact same semantics as -m and -M, except instead of the branch being renamed, it will be copied to a new name, along with its config and reflog.<br/>
> ...<br/>
> With a -d or -D option, <branchname> will be deleted. You may specify more than one branch for deletion. If the branch currently has a reflog then the reflog will also be deleted.<br/>

There's lots of options that you can pass into the `branch` command, but we'll focus on just listing and creating branches,
and how we delete a ***local*** branch.

##### When Is It Used?

You've `cloned` your teammate's repository and had a poke about the code. By default, you took a copy of their `main` branch
(this can also be called `master` or `trunk`). Although this is a copy of the code, there's various reasons why you may 
not necessarily want to work on this branch. Can you think of any?

##### Tasks

Using the example repository above:

1. List all the branches contained in the repository.
2. List all the branches, including remote ones, in the repository.
3. Create a copy of the `main` branch and name it `my-feature`.
4. List all the branches again and note the new branch.
5. Finally, delete the `my-feature` branch.


#### `git log`

From the Git help page:

> List commits that are reachable by following the parent links from the given commit(s), but exclude commits that are reachable from the one(s) given with a ^ in front of them. The
> output is given in reverse chronological order by default.<br/><br/>
> You can think of this as a set operation. Commits reachable from any of the commits given on the command line form a set, and then commits reachable from any of the ones given with ^ in
> front are subtracted from that set. The remaining commits are what comes out in the command’s output. Various other options and paths parameters can be used to further limit the result.

Err, what? Simply put, `log` is an easy way of viewing the history of the repository. By default, `log` will show you
the history of your current branch. You can get information such as:
- The commit SHA;
- Latest Commit Author;
- Latest Commit time and date;
- Commit description;
- Information about various tags and branches.

By passing different options to the `log` command you can get much more information. 

##### When Is It Used?

The `log` command is useful when you want to get information about what is changed, why it's been changed (if a good 
commit messaged has been included!), when and by whom.

##### Tasks

Using the repository above:
1. Use the `log` command to inspect the repository history? Who changed the repository last? What does the commit message say?
2. Use the Git documentation to find a way to search for commits from that `author`.


#### `git show`

From the Git help page:

> Shows one or more objects (blobs, trees, tags and commits).<br/>
> For commits it shows the log message and textual diff. It also presents the merge commit in a special format as produced by git diff-tree --cc.<br/>
> ...

##### When Is It Used?

One of the most common usages of `show` is to inspect commit. By default `git show` will show you the changes from the latest commit.

Remember that commit SHA from the previous task? That's a reference to a specific commit. Git allows us to pass in references (SHAs) to the `show` command to inspect the commit.

##### Tasks

Using the repository above:
1. Use the `show` command to inspect the latest commit.
2. Using the results of the `log` command above, inspect some of the latest commit author's other commits. 


## Part 3 - Creating Our Own Branch, Making Changes, Checking What's Changed

### What We'll Cover

Here are the commands we'll cover in this section, along with a one-liner about what it does `git --help`:
- [`checkout`](https://git-scm.com/docs/git-checkout) - Switch branches or restore working tree files
- [`status`](https://git-scm.com/docs/git-status) - Show the working tree status
- [`diff`](https://git-scm.com/docs/git-diff) - Show changes between commits, commit and working tree, etc

### Commands In More Detail

#### `git checkout`

From the Git help page:

> Updates files in the working tree to match the version in the index or the specified tree. If no pathspec was given, git checkout will also update HEAD to set the specified branch as
> the current branch. <br/>
> ... <br/>
> Specifying -b causes a new branch to be created as if git-branch(1) were called and then checked out. In this case you can use the --track or --no-track options, which will be 
> passed to git branch. As a convenience, --track without -b implies branch creation; see the description of --track below.

Okay, so you've taken a copy of a repository and by default you're on the `main` branch, but you don't want to stay here.

##### When Is It Used?

There's two scenarios that we'll cover here:
1. Switching to another branch that already exists;
2. Switching to another branch that doesn't exist yet.

##### Tasks

Using the repository above:
1. Use the `branch` command list to list all the branches, then use `checkout` to switch to one of those branches.
2. Use the `checkout` command to switch back to the `main` branch, then create a new branch off `main` called `my-branch`


#### `git status`

From the Git help page:

> Displays paths that have differences between the index file and the current HEAD commit, paths that have differences between the working tree and the index file, and paths in the
> working tree that are not tracked by Git (and are not ignored by gitignore(5)). <br/>
> ...

Too many words! `git status` lists files have changed (if they're tracked), or files that have been added and aren't on our ignore list.

It doesn't show us the actual chances... that will come later!

##### When Is It Used?

You've been hack, hack, hacking away. Adding new code, ripping out old cold, refactoring other bits. You've changed so many 
files that you've lost track! `git status` will do a good job in reminding you. Remember the three types of files:
1. Tracked and modified;
2. Tracked and unmodified; and
3. Untracked.

##### Tasks

Using the repository above:
1. Have a look at the code and change something. What does the status command tell you?
2. Create a new Java file in the same directory as `HelloWorld.java`. What does the status command tell you now?
3. Take a look at the `.gitignore` file, then build the project (`mvn package`), look at what files have been added to the directory.
   Before you run the status command this time, have a think about what you expect to see. Then run the status command.


#### `git diff`

From the Git help page:

> Show changes between the working tree and the index or a tree, changes between the index and a tree, changes between two trees, changes resulting from a merge, changes between two blob 
> objects, or changes between two files on disk.

Where `git status` showed us what *files* changed, `git diff` will show us what actually changed in those files.

##### When Is It Used?

After changing all those files you now want to see what actually changed! `git diff` is your friend here!

##### Tasks

Using the repository above:
1. Use the diff command to inspect your changes from the previous task.
2. Use the diff command to compare your changes to changes in another branch (use the documentation if you need a hint on how to do this).
3. How would you inspect the changes in a single file instead of all modified files?


## Part 4 - Saving Our Changes, Undoing Changes That We Don't Need

### What We'll Cover

Here are the commands we'll cover in this section, along with a one-liner about what it does `git --help`:
- [`add`](https://git-scm.com/docs/git-add) - Add file contents to the index
- [`reset`](https://git-scm.com/docs/git-reset) - Reset current HEAD to the specified state
- [`commit`](https://git-scm.com/docs/git-commit) - Record changes to the repository
- [`revert`](https://git-scm.com/docs/git-revert) - Revert some existing commits
- [`stash`](https://git-scm.com/docs/git-stash) - Stash the changes in a dirty working directory away
- [`push`](https://git-scm.com/docs/git-push) - Update remote refs along with associated objects

### Commands In More Detail

#### `git add`

From the Git help page:

> This command updates the index using the current content found in the working tree, to prepare the content staged for the next commit. 
> ...

##### When Is It Used?

You've written some beautiful code, tested it (you wrote the tests first of course...), and now you're at a point where
you want to save those changes. This is the first step in that process - indicating to Git which files you want to change.
When you run the `add` command it puts the selected files into the *staging* area.

##### Tasks

Using the repository above:
1. Use some of the files that were changed in the previous tasks and add them to the staging area.
2. Run the status and diff commands and inspect the output. Is it what you expected? If it's not what you expected try to
   figure out what's happening and update the commands to get the expected output.


#### `git reset`

From the Git help page:

> In the first three forms, copy entries from <tree-ish> to the index. In the last form, set the current branch head (HEAD) to <commit>, optionally modifying index and working tree to
> match. The <tree-ish>/<commit> defaults to HEAD in all forms.

That's a bit wordy. `reset` will the files to another branch or commit ID.

##### When Is It Used?

Two of the most common scenarios that we use `git reset` are:
1. To un-stage files (soft reset); and
2. To remove all changes (hard reset).

It's important to know the difference. If you've changed a file and then do a soft reset your changes will still be there
when you do a soft reset. If you do a hard reset your changes will be gone.

##### Tasks

Using the repository above:
1. Add some changes to a file, add those changes to the staging area, then un-stage them (without deleting your changes).
2. Add some changes to a file, add those changes to the staging area, then un-stage them (deleting your changes).


#### `git commit`

From the Git help page:

> Create a new commit containing the current contents of the index and the given log message describing the changes. The new commit is a direct child of HEAD, usually the tip of the
> current branch, and the branch is updated to point to it (unless no branch is associated with the working tree, in which case HEAD is "detached" as described in git-checkout(1)).
> ...

The first sentence is the most important - we're saving our changes and leaving a comment as to *why* those changes were made.

##### When Is It Used?

You're up to the point where you've added new code, tested it, put it in the staging area indicating to Git that you want to save
these files, now it's time to perform the save. Running the commit command will create a record of what has changed and by whom.

##### Tasks

Using the repository above:
1. Make some changes to the files above, add them to the staging area, and commit them.
2. Use the log command to inspect the logs.


#### `git revert`

From the Git help page:

> Given one or more existing commits, revert the changes that the related patches introduce, and record some new commits that record them. This requires your working tree to be clean (no
> modifications from the HEAD commit).

This is Git's equivalent to CTRL+Z / CMD+Z.

##### When Is It Used?

If we want to undo a commit then we can use `git revert`. This will create a commit which reverses the changes.
There are ways to undo changes without adding a revert commit...

##### Tasks

Using the repository above:
1. Revert the commit you added in the previous task.
2. How would you revert the commit without using the revert command? Hint: it's one of the commands already covered.


#### `git stash`

From the Git help page:

> Use git stash when you want to record the current state of the working directory and the index, but want to go back to a clean working directory. The command saves your local
> modifications away and reverts the working directory to match the HEAD commit.


We've talked about saving our files using the add and commit commands, `git stash` is another way of saving changes.

##### When Is It Used?

If you've made some code changes, but you don't feel like they're ready to commit (or maybe you don't want to commit them, but you want to keep *somewhere*),
stashing them might be a better alternative. The difference here is that when you stash changes they won't appear in your log.
Another important difference is that you won't accidentally push the changes (see next command).

##### Tasks

Using the repository above:
1. Change some files and then stash them.
2. Use the documentation to find out how to list and view your stashes.
3. Use the documentation to find out how to get your changes back into your workspace. There's different commands that can
   be used for this so explore a few.


#### `git push`

From the Git help page:

> Updates remote refs using local refs, while sending objects necessary to complete the given refs.

Time to share your changes with other folk!

##### When Is It Used?

Your code is complete, and now you want to share it with other people! All the commands up to this point have only affected
your local copy. That changes after we run `git push`; this will update the code in the remote repository (the same place
you got the code from originally).

##### Tasks

Using the repository above:
1. Push your changes up to the remote repository (use your own branch for this), then Use the web browser to inspect the changes.


## Part 5 - Getting The Latest Code

Someone else in your team has followed all the steps above, now we'll explore how we update our local copy to reflect those changes.

### What We'll Cover

Here are the commands we'll cover in this section, along with a one-liner about what it does `git --help`:
- [`merge`](https://git-scm.com/docs/git-merge) - Join two or more development histories together
- [`fetch`](https://git-scm.com/docs/git-fetch) - Download objects and refs from another repository
- [`pull`](https://git-scm.com/docs/git-pull) - Fetch from and integrate with another repository or a local branch

### Commands In More Detail

#### `git fetch`

From the Git help page:

> Fetch branches and/or tags (collectively, "refs") from one or more other repositories, along with the objects necessary to complete their histories. Remote-tracking branches are updated
> (see the description of <refspec> below for ways to control this behavior).

Performs a sync with the remote repository so you know what's changed.

##### When Is It Used?

One of your teammates has updated the repository that you've both been working on. Your branch (and all the other branches)
won't automatically update, you have to tell Git to do this. The first step is asking Git to ask "What has changed?"
This is where `git fetch` comes in. Note: we're not bringing the changes into our branch, that comes next.

##### Tasks

Using the repository above:
1. Run the fetch command and inspect the output.


#### `git merge`

From the Git help page:

> Incorporates changes from the named commits (since the time their histories diverged from the current branch) into the current branch. This command is used by git pull to incorporate
> changes from another repository and can be used by hand to merge changes from one branch into another.

Take my changes and take those changes, and smash 'em together!

##### When Is It Used?

Your teammate has some changes that you want, `git merge` is how you get your hands on them. There's a few different ways
you can merge their changes in:
- Fast-forward - this pulls the changes in without creating a *merge* commit.
- No-fast-forward - This pulls in the changes but will create a *merge* commit.

##### Tasks

Using the repository above:
1. Try out the different types of merge (remember you can revert a merge when you need to)


#### `git pull`

From the Git help page:

> Incorporates changes from a remote repository into the current branch. If the current branch is behind the remote, then by default it will fast-forward the current branch to match the
> remote. If the current branch and the remote have diverged, the user needs to specify how to reconcile the divergent branches with --rebase or --no-rebase (or the corresponding
> configuration option in pull.rebase).

This does the fetch and merge (with fast-forward if possible) commands in one go.

##### When Is It Used?

If you want to pull changes into your local branch in one command.

##### Tasks

Using the repository above:
1. Revert the changes from the previous tasks and run the pull command instead.


### References

- [Git Reference Page](https://git-scm.com/docs)
