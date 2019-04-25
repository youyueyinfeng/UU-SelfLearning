# Svn

任务

- 掌握svn基本理念，常用名词（revision、wc等等）
- 掌握常用svn命令
- 掌握如何做分支的使用（如何创建branch、merge等）
- 使用svn管理自己的小程序代码（并尝试svn的常用命令，例如修改代码后提交）
- 模拟出一个代码出现冲突（conflict）的情况，并解决冲突



## Preface

In the world of open source software, the Concurrent Versions System (CVS) was the tool of choice for version control for many years. And rightly so. CVS was open source software itself, and its nonrestrictive modus operandi and support for networked operation allowed dozens of geographically dispersed programmers to share their work.

Subversion was designed to be a successor to CVS, and its originators set out to win the hearts of CVS users in two ways—by creating an open source system with a design (and “look and feel”) similar to CVS, and by attempting to avoid most of CVS's noticeable flaws.

### What is Subversion

Subversion is a free/open source *version control system* (VCS). Subversion manages files and directories, and the changes made to them, over time. This allows you to recover older versions of your data, or examine the history of how your data changed. 

#### Is Subversion the Right Tool

When Subversion was first designed and released, the predominant methodology of version control was *centralized version control*—a single remote master storehouse of versioned data with individual users operating locally against shallow copies of that data's version history. 

A newer methodology of version control called *distributed version control* has likewise garnered widespread attention and adoption. Distributed version control harnesses the growing ubiquity of high-speed network connections and low storage costs to offer an approach which differs from the centralized model in key ways.

There are pros and cons to each version control approach. Perhaps the two biggest benefits delivered by the DVCS tools are incredible performance for day-to-day operations (because the primary data store is locally held) and vastly better support for merging between branches (because merge algorithms serve as the very core of how DVCSes work at all). The downside is that distributed version control is an inherently more complicated model, which can present a non-negligible challenge to comfortable collaboration. Also, DVCS tools do what they do well in part because of a certain degree of control ability to implement path-based access control, the flexibility to update or backdate individual versioned data items, etc.



## Fundamental Concepts

### Version Control Basics

A version control system (or revision control system) is a system that tracks incremental versions (or revisions) of files and, in some cases, directories over time.

#### Repository

Repository is the central store of that system's data. The repository usually stores information in the form of a *filesystem tree*—a hierarchy of files and directories. Any number of *clients* connect to the repository, and then read or write to these files. 

What makes the repository special to a typical file server, is that as the files in the repository are changed, the repository remembers each version of those files.

#### Working copy

A working copy is, quite literally, a local copy of a particular version of a user's VCS-managed data upon which that user is free to work. Working copies appear to other software just as any other local directory full of files.

#### Versioning models

A versioning model is a strategies to enable collaborative editing and sharing of the various versions of digital informaiontion over time.

A fundamental problem to solve is file sharing. If two users modify a same file, how to avoid overwrite?

##### lock-modify-unlock solution

Many version control systems use a *lock-modify-unlock* model to address the problem of many authors clobbering each other's work. In this model, the repository allows only one person to change a file at a time.

But lock-modify-unlock model has many cons: 
- *Locking may cause administrative problems.* It need an adminstrator to release a lock if a user forgot he locked a file. 
- *Locking may cause unnecessary serialization.* Sometimes users just want to modify different part of a same file. 
- *Locking may create a false sense of security.* If FileA and FileB depend on one anther, the changes made to each may be semantically incompatible.

##### copy-modify-merge solution

Subversion, CVS, and many other version control systems use a *copy-modify-merge* model as an alternative to locking. 

In this model, each user's client contacts the project repository and creates a personal working copy. Users then work simultaneously and independently, modifying their private copies. Finally, the private copies are merged together into a new, final version. The version control system often assists with the merging, but ultimately, a human being is responsible to solve *conflicts* for making merging happen correctly.

The copy-modify-merge model may sound a bit chaotic, but in practice, it runs extremely smoothly. Users can work in parallel, never waiting for one another. When they work on the same files, it turns out that most of their concurrent changes don't overlap at all; conflicts are infrequent. And the amount of time it takes to resolve conflicts is usually far less than the time lost by a locking system.

The copy-modify-merge model is based on the assumption that files are contextually mergeable—that is, that the majority of the files in the repository are line-based text files (such as program source code). But for files with binary formats, such as artwork or sound, it's often impossible to merge conflicting changes. In these situations, Subversion use a feature called "Locking".

### Version Control the Subversion Way

#### Revisions

A Subversion client commits (that is, communicates the changes made to) any number of files and directories as a single atomic transaction. Each time the repository accepts a commit, this creates a new state of the filesystem tree, called a *revision*.

Each revision is assigned a unique natural number, one greater than the number assigned to the previous revision. The initial revision of a freshly created repository is numbered 0 and consists of nothing but an empty root directory.

Each revision is assigned a unique natural number, one greater than the number assigned to the previous revision. The initial revision of a freshly created repository is numbered 0 and consists of nothing but an empty root directory. Each revision number has a filesystem tree hanging below it, and each tree is a “snapshot” of the way the repository looked after a commit. Subversion's revision numbers apply to *the entire repository tree*, not individual files.

#### Addressing the Repository

Subversion client programs use URLs to identify versioned files and directories in Subversion repositories.

#### Subversion Working Copies

A Subversion working copy is an ordinary directory tree on your local system, containing a collection of files. 

After you've made some changes to the files in your working copy and verified that they work properly, Subversion provides you with commands to “publish” your changes to the other people working with you on your project (by writing to the repository). If other people publish their own changes, Subversion provides you with commands to merge those changes into your working copy by reading from the repository).

Each working copy contains a subdirectory named `.svn`, also known as the working copy's *administrative directory*. It helps Subversion recognize which of your versioned files contain unpublished changes, and which files are out of date with respect to others' work.

Prior to version 1.7, Subversion maintained `.svn` administrative subdirectories in *every* versioned directory of your working copy. Now, each working copy now has only one `.svn` subdirectory .

##### How the working copy works

For each file in a working directory, Subversion records two essential pieces of information:

- What revision your working file is based on (this is called the file's *working revision*)
- A timestamp recording when the local copy was last updated by the repository

Given this information, by talking to the repository, Subversion can tell which of the following four states a working file is in:

- Unchanged, and current

  The file has not been changed in the working directory, and no changes to that file have been committed to the repository since you last updated.

  An `svn commit` of the file will do nothing, and an `svn update` of the file will do nothing.

- Locally changed, and current

  The file has been changed in the working directory, and no changes to that file have been committed to the repository since you last updated.

  An `svn commit` of the file will succeed in publishing your changes, and an `svn update` of the file will do nothing.

- Unchanged, and out of date

  The file has not been changed in the working directory, but it has been changed in the repository. 

  An `svn commit` of the file will do nothing, and an `svn update` of the file will fold the latest changes into your working copy.

- Locally changed, and out of date

  The file has been changed both in the working directory and in the repository.

  An `svn commit` of the file will fail with an“out-of-date” error. The file should be updated first; an `svn update` command will attempt to merge the public changes with the local changes. If Subversion can't complete the merge in a plausible way automatically, it leaves it to the user to resolve the conflict.

##### Fundamental working copy interactions

A typical Subversion repository often holds the files (or source code) for several projects; usually, each project is a subdirectory in the repository's filesystem tree. In this arrangement, a user's working copy will usually correspond to a particular subtree of the repository.

To get a working copy, you must *check out* (creates a working copy of the project for you) some subtree of the repository. Like:

```shell
svn checkout http://svn.example.com/repos/calc
```

Then you make changes to `button.c`, and wish to publish the changes:

```
svn commit button.c -m "Fixed a typo in button.c."
```

To bring the project up to date:

```
svn update
```

##### Mixed-revision working copies

Subversion working copies do not always correspond to any single revision in the repository; they may contain files from several different revisions.

Revision id is decided by Central Repository. When you commit a file, Central Repository will arrange a ID for it. So, when you commit a file, the revision of that file is former than the rest of files.

```
calc/																calc/
	Makefile:4			  		# edit button.c						    Makefile:4
	integer.c:4      	=>    	# svn commit botton.c   => 			    integer.c:4 
	button.c:4												   			button.c:6
```

Mixed revisions are normal. After several commits (with no updates in between), your working copy will contain a whole mixture of revisions.

Updates and commits are separate. One of the fundamental rules of Subversion is that a “push” action does not cause a “pull” nor vice versa.  Just because you're ready to submit new changes to the repository doesn't mean you're ready to receive changes from other people.

Mixed revisions are useful. Perhaps you'd like to test an earlier version of a submodule contained in a subdirectory, or perhaps you'd like to figure out when a bug first came into existence in a specific file.

## Basic Usage

### Installation

For Debian 9:

```shell
sudo apt install subversion
```

Export a env to choose `vi` as normal editor.

```
export SVN_EDITOR=vi
```

### Creating and Configuring Your Repository

#### Creating

Subversion repository creation is an incredibly simple task.

```shell
mkdir -p ~/svn/repos
svnadmin create ~/svn/repos
```

It will create a new repository in the directory `~/svn/repos`. Present in the `db/` subdirectory of your repository is the implementation of the versioned filesystem. Your new repository's versioned filesystem begins life at revision 0, which is defined to consist of nothing but the top-level root (`/`) directory. 

Use `svnserve` to provide svn service.

```shell
svnserve -r -d ~/svn/
```

Check if service has been started.

```shell
netstat -nltp | grep 3690
```

Checkout the repos.

```shell
svn checkout svn://localhost/repos
```

#### Configuring

By default, user unauthenticated has no right to modify repo. Configure your repo to add authentication.  

Edit configure file `conf/svnserve.conf` in repository. Uncomment:

```shell
passwork-db = passwd
authz-db = authz
```

Edit file `conf/passwd` to add a user. Add:

```shell
# user = password
xxs = 123456
```

Edit file `conf/authz` to add right arrangement. Add:

```shell
# [repo name: relative path in repo]
# user = right
[repos:/]
xxs = rw
```

Now test:

```shell
cd [ws]
svn checkout svn://localhost/repos
cd repos
touch README.md
svn commit README.md
# input user and password first time
```

### Getting Data into Your Repository

You can get new files into your Subversion repository in two ways: *svn import* and *svn add*.

#### Importing Files and Directories

The *svn import* command is a quick way to copy an unversioned tree of files into a repository, creating intermediate directories as necessary.

You typically use this when you have an existing tree of files that you want to begin tracking in your Subversion repository.

```shell
svn import /path/to/mytree \
		   http://svn.example.com/svn/repo/some/project \
           -m "Initial import"
```

Use `svn list` to check the result of importing.

```shell
svn list http://svn.example.com/svn/repo/some/project
```

#### Recommended Repository Layout

Follow a repository layout convention will make the project tidy and easy to be recognized. 

```
repos
├── Project-A
│   ├── trunk
│   ├── branches
│   └── tags
└── Project-B
    ├── trunk
    ├── branches
    └── tags
```

### Creating a Working Copy

Most of the time, you will start using a Subversion repository by performing a *checkout* of your project. Checking out a directory from a repository creates a working copy of that directory on your local machine.

```shell
svn checkout http://svn.example.com/svn/repo/trunk
```

You can check out a specified subdirectoy by specifying that subdirectory's URL as the checkout URL:

```shell
svn checkout http://svn.example.com/svn/repo/trunk/src
```

### Basic Work Cycle

#### Update your working copy

When working on a project that is being modified via multiple working copies, you'll want to update your working copy to receive any changes committed from other working copies since your last update.

Use *svn update* to bring your working copy into sync with the latest revision in the repository.

```
svn update
```

#### Make Your Changes

You can make two kinds of changes to your working copy: *file changes* and *tree changes*. 

File changes will be detected automatically by Subversion. You edit file the way you normally do.

Tree changes are different. You should use Subversion operations to “schedule” files and directories for removing files, renaming files or directories, and copying files or directories to new locations.

Use `svn add` to add an item to the repo. If item is a directory, everything underneath will be added. 
Pass `--depth=empty` to add the diretory itself.

```shell
svn add FOO
svn add DIR --depth=empty
```

Use `svn delete` to delete an item from the repo. If item is a file, it will be deleted immediately from your working copy. If item is a directory, it will not be deleted until next `svn commit`.

```
svn delete FOO
```

Use `svn copy` to "copy" FOO to BAR. BAR will be added to repo immediately. Pass `--parents` option if you want to make directories as parent directories of BAR.

BAR will have the same history as FOO's. In client,  a new file BAR is copied from FOO to BAR. In server end, only a flag "BAR" will be made pointing to FOO.

```shell
svn copy FOO BAR
svn copy FOO new_dir/BAR --parents
```

`svn move` is same as running `svn copy; svn delete`. `BAR` is scheduled for addition as a copy of `FOO`, and `FOO` is scheduled for removal. Similarily, you can pass '--parents' to make parent dir.

```shell
svn move FOO BAR
svn move FOO new_dir/BAR --parents
```

`svn mkdir` is same as running `mkdir; svn add`. 

```shell
svn mkdir FOO
```

The differience between tree changes svn command like `svn add` and  URL-based operation like `svn import` is that, whether you need check out a working copy. The only advantage of URL-based operation is speed, especially when you only want to make some simple operation. 

#### Review Your Changes

It's usually a good performance to review and scrutinize changes before publishing them. 

To get an overview of your changes, use the *svn status* command.

```
svn status
```

The first column tells the status of a file or directory and/or its contents. `?` for not under version control, `A` for addition, `C` for conflict, `D` for deletion, `M` for modification.

Pass `-v` or `--verbose` will show status of *every* item in your working copy, even if it has not been changed:

```shell
svn status -v
```

The letters in the first column mean show status. The second column shows the working revision of the item. The third and fourth columns show the revision in which the item last changed, and who changed it.

Pass `-u` or `--show-updates` will contact the repo and get the current revision and others' modification.

```shell
svn status -u -v
```

Item marked by two asterisks will be modified next `svn update`. 

`svn diff` will display differences in file content. It prints the changes you've made to human-readable files in your working copy, in *unified diff* format which is compatible with `svn patch`.

```shell
svn diff
```

#### Fix Your Mistakes

Use `svn revert` to undo your work, *any* scheduled operation in your woking copy, and start over from scratch. 

```shell
svn revert FOO
```

#### Resolve Any Conflicts

Conflicts can occur any time you attempt to merge or integrate (in a very general sense) changes from the repository into your working copy.

```shell
svn update --non-interactive
```

When use `svn update` to pull down changes, you can get the information of changes from output. `U` for update, `G` for merged, and `C` for conflicts. Update means no local changes but updating with remote changes. Merge means merging local changes and remote changes. 

By default, when conflicts exist, `svn update` without option will lead to an interaction mode. Conflicts will be present in a sentence and several interaction choices.

```
(e)  edit             - change merged file in an editor
(df) diff-full        - show all changes made to merged file
(r)  resolved         - accept merged version of file
(dc) display-conflict - show all conflicts (ignoring merged version)
(mc) mine-conflict    - accept my version for all conflicts (same)
(tc) theirs-conflict  - accept their version for all conflicts (same)
(mf) mine-full        - accept my version of entire file (even non-conflicts)
(tf) theirs-full      - accept their version of entire file (same)
(p)  postpone         - mark the conflict to be resolved later
(l)  launch           - launch external tool to resolve conflict
(s)  show all         - show this list
```

Choose choice `df` or `dc` will display the information of all modification or just conflicts.

After viewing the conflicts, you can choose `mc`、`tc`、`mf`、`tf` to resolve the conflicts. 

Choose choice `p` to postpone conflict will reach the same performance with passing `--non-interactive`. Files with conflicts will be marked with `C`. 

For every postpon-fixed conflicted file, Subversion places three extra unversioned files in your working copy:

- *filename.mine*, the original file in working copy berfore update, containing local modifications.
- *filename.rOLDREV*, the file of BASE unmodified revision in working copy. *OLDREV* is the base revision number.
-  *filename.rNEWREV*, the file of revision in repo. *NEWREV*  is the up-to-date revision number.

Use `svn resolve` to fix the postpon conflicts. Passing `--accept` and an ARG to decide the resolution. ARG can be `base `、`working`、`mine-conflict`、`theirs-conflict`、`mine-full`、`theirs-full`.

Pass the `base` will make the file same with *filename.rOLDREV*, while `mf` responding to *filename.mine* and `tf` responding to *filename.rNEWREV*. Pass the latter four ARGs will get same result with choosing `mc`、`tc`、`mf`、`tf` in interaction mode. 

More often, we need to fix the conflicts by hand, not just choose one version. Edit the file and fix the conflicts, and then:

```shell
svn resolve --accept working FOO
```

Although `svn revert` will 'fix' conflicts, **notice** that, `svn update` will update the revision number of file to the revision number of repo, even if conflicts exists. That's mean `svn revert` *file* will make it same with *filename.rNEWREV*, not *filename.rOLDREV*.

#### Commit Your Changes

After fixing the conflicts, the status of the file is *modified*, so you commit it.

```shell
svn commit -m [FOO] "Corrected number of cheese slices."
```

### Examining History

Subversion keeps a record of every change ever committed and allows you to explore this history by examining previous versions of files and directories as well as the metadata that accompanies them.

#### Examining the Details of Historical Changes

`svn diff` shows line-level details of a particular change. 

Invoking `svn diff` with no options will compare your working files to the cached “pristine” copies in the `.svn` area:

```shell
svn diff
```

If a single `--revision` (`-r`) number is passed, your working copy is compared to the specified revision in the repository:

```shell
svn diff -r 3 FOO
```

Comparing between revisions is to separate two revisons by a colon:

```shell
svn diff -r 2:3 rules.txt
```

Comparing one revision to the previous revision is to use the `--change` (`-c`) option:

```shell
svn diff -c 3 FOO
```

You can compare even when you don't have a working copy on your local machine:

```shell
svn diff -c 5 http://svn.example.com/repos/example/trunk/text/rules.txt
```

#### Generating a List of Historical Changes

`svn log` will provide you with a record of who made changes to a file or directory, at what revision it changed, the time and date of that revision.

```shell
svn log
```

Note that the log messages are printed in *reverse chronological order* by default. If you wish to see a different range of revisions in a particular order or just a single revision, pass the `--revision` (`-r`) option:

```shell
svn log -r 5:19
svn log -r 19:5
svn log -r 8
```

You can also examine the log history of a single file or directory

```shell
svn log FOO
```

If you make a commit and immediately type `svn log` with no arguments, you may notice that your most recent commit doesn't show up in the list of log messages. It is because that when you commit changes to the repository, *svn* bumps only the revision of files (and directories) that it commits, so usually the parent directory remains at the older revision.

If you want even more information about a file or directory, *svn log* also takes a `--verbose` (`-v`) option.

```shell
svn log -r 8 -v
```

If you supply no path, Subversion uses the current working directory as the default target, checking the files underneath but ignoring the subdirectory.

You can integrate a difference report with log report, by passing `--diff`:

```shell
svn log -r 8 -v --diff
```

#### Browsing the Repository

You can view various revisions of files and directories without changing the working revision of your working copy. In fact, you don't even need a working copy to use either one.

##### Displaying file contents

You can get the content of a file of a sepecified version:

```shell
svn cat -r 2 FOO
```

##### Displaying line-by-line change attribution

`svn blame` (or `svn praise`, `svn annotate`, `svn ann`) shows each line of linear file with the username, the revision number. `svn blame` can be used to find out who modified the file latest.

`svn blame` will by default show line-by-line attribution of the file as it currently appears in the working copy. Lines with no attribution provided, have been modified in the working copy's version of the file.

```shell
svn blame FOO
```

You can use the `BASE` revision keyword to instead see the unmodified form of the file as it resides in your working copy.

```shell
svn blame FOO@BASE
```

You can also ask `svn blame` to display previous versions of the file.

```shell
svn blame FOO -r 2
```

Attempt to run the command on a binary file will cause an error.

##### Listing versioned directories

The *svn list* command shows you what files are in a repository directory without actually downloading the files to your local machine. Pass the `--verbose` (`-v`) flag to get more detailed listing:

```shell
svn list -v http://svn.example.com/repo/project
```

#### Fetching Older Repository Snapshots

You can use the `--revision` (`-r`) option with *svn update* to take an entire working copy “back in time”.

```shell
svn update -r [old_revision]
```

Notice that, the file are "back in time". Even if you modified the file at this state, you can not commit them. That 's why you can not use `svn update` to 'undo' committed changes.

Use `svn checkout ` to  create a whole new working copy from an older snapshot:

```shell
# Checkout the trunk from r1729
svn checkout http://svn.example.com/svn/repo/trunk@1729 trunk-1729
# Checkout the current trunk as it looked in r1729, (not found difference)
svn checkout http://svn.example.com/svn/repo/trunk -r 1729 trunk-1729
```

`svn export` to create a local copy of all or part of your repository without any `.svn` administrative directories included.

```shell
svn export http://svn.example.com/svn/repo/trunk trunk-export
svn export http://svn.example.com/svn/repo/trunk@1729 trunk-1729
svn export http://svn.example.com/svn/repo/trunk -r 1729 trunk-1729
```

### Dealing with Structural Conflicts

Conflicts may also happen to tree changes. For example, you are modifying a file while your teamate has already committed a rename operation to that file. Subversion can deal with this situation.

The solution of resolving tree conflicts vary from case to case. Please check[使用SVN命令行解决树冲突(tree conflict)](https://www.jianshu.com/p/e3cc83ca512d).

## Branching and Merging

### Using Branches

A branch allows you to save your not-yet-completed work frequently without interfering with others' changes and while still selectively sharing information with your collaborators.

#### Creating a Branch

Creating a branch is very simple—you make a copy of your project tree in the repository using the *svn copy* command. 

Normally, project's source code is rooted in `/**/trunk` directory, and branched are in `/**/branches`.

It's recommended that make a branch by `svn copy` on server side, which is a constant-time operation. Copying a directory on the client side is a linear-time operation, in that it actually has to duplicate every file and subdirectory within that working copy directory on the local disk.

```shell
svn copy http://svn.example.com/repos/calc/trunk \
         http://svn.example.com/repos/calc/branches/my-calc-branch \
         -m "Creating a private branch of /calc/trunk."
```

Subversion's repository has a special design. When you copy a directory, you don't need to worry about the repository growing huge—Subversion doesn't actually duplicate any data. Instead, it creates a new directory entry that points to an *existing* tree. If you're an experienced Unix user, you'll recognize this as the same concept behind a hard link. As further changes are made to files and directories beneath the copied directory, Subversion continues to employ this hard link concept where it can. It duplicates data only when it is necessary to disambiguate different versions of objects.

This is why you'll often hear Subversion users talk about “cheap copies.” It doesn't matter how large the directory is—it takes a very tiny, constant amount of time and space to make a copy of it. In fact, this feature is the basis of how commits work in Subversion: each revision is a “cheap copy” of the previous revision, with a few items lazily changed within. 

#### Working with Your Branch

Files in different branches (or say, copies) share the same history, but are used as two isolated file later.

### Basic Merging

In Subversion terminology, the general act of replicating changes from one branch to another is called *merging*, and it is performed using various invocations of the *svn merge*subcommand.

#### Keeping a Branch in Sync

While you are developing, your teanmate commit  an important changes to `/trunk`. It's in your best interest to replicate those changes to your own branch, just to make sure they mesh well with your changes. This is done by performing a *sync merge*—a merge operation designed to bring your branch up to date with any changes made to its ancestral parent branch since your branch was created.

To perform a sync merge, first make sure your working copy of the branch is “clean”. Caret (`^`) syntax can be used to avoid having to type out the entire `/trunk` URL. 

```shell
# cd ^/calc/branches/my-calc-branch
svn merge ^/calc/trunk
```

After performing the merge, you might also need to resolve some conflicts. At this point, the wise thing to do is look at the changes carefully with `svn diff`, and then build and test your branch. 

Unlike `svn update`, `.` won't be updated. So if you want to abort all the merge changes:

```shell
svn revert . -R
```

If you accept the merge changes or resolve the conflicts, commit the changes with the merge info:

```shell
svn commit -m "Merged latest trunk changes to my-calc-branch."
```

Although `svn patch ` seems can make the same performance on linear file, `svn merge` can merge changes on tree structure as well.  Even more important, this command records the changes that have been duplicated to your branch so that Subversion is aware of exactly which changes exist in each location. This is a critical feature that makes branch management usable; without it, users would have to manually keep notes on which sets of changes have or haven't been merged yet.

`svn merge` disable merges into mixed-revision working copies by default. These limitations mean that merges into mixed-revision working copies can result in unexpected text and tree conflicts.  Just update berfore merge:

```shell
svn update
svn merge ^/calc/trunk
```

#### Merge Changesets

`svn merge` would merge changeset r9238 into your working copy.

```shell
svn merge -c 9238
```

#### Subtree Merges and Subtree Mergeinfo

While this is a best practice, you may occasionally need to merge directly to some child of the branch root. This type of merge is called a *subtree merge* and the mergeinfo recorded to describe it is called *subtree mergeinfo*.

```shell
# cd ^/calc/branches/my-calc-branch
svn merge ^/trunk/doc/INSTALL doc/INSTALL -c 958
```

#### Reintegrating a Branch

After work for the new feature has been done, pull the changes of trunk, check it. If ok, commit it:

```shell
# cd ^/calc/branches/my-calc-branch
svn merge ^/calc/trunk
# build, test
svn commit -m "Final merge of trunk changes to my-calc-branch."
```

Then, replicate your branch changes back into the trunk. 

```shell
# cd ^/calc/trunk
svn update
svn merge --reintegrate ^/calc/branches/my-calc-branch
# build, test, verify, ...
svn commit -m "Merge my-calc-branch back into trunk!"
```

Merging branch into trunk is quite different with merging trunk to branch. Merging trunk to branch is straightforward. It just grab the changes of a contiguous range from the trunk, eg. r345:r356, and duplicate them to branch. However, when merging your branch back to the trunk, Svn cannot find a contiguously range. The feature branch is now a mishmash of both duplicated trunk changes and private branch changes. So, it can not use the same mathmatics with formmer. By specifying the `--reintegrate` option, you're asking Subversion to carefully replicate *only* those changes unique to your branch.

After reintergrate, the feature branch can be and good to be removed:

```shell
svn delete http://svn.example.com/repos/calc/branches/my-calc-branch \
             -m "Remove my-calc-branch, reintegrated with trunk in r391."
```

#### Mergeinfo and Previews

The basic mechanism Subversion uses to track changesets is by recording data in versioned properties. 

Specifically, merge data is tracked in the `svn:mergeinfo` property attached to files and directories.

```shell
# cd ^/calc/branches/my-calc-branch
svn propget svn:mergeinfo .
```

The `svn:mergeinfo` property is automatically maintained by Subversion whenever you run *svn merge*. Its value indicates which changes made to a given path have been replicated into the directory in question. 

Subversion also provides a subcommand, `svn mergeinfo`, which is helpful in seeing not only which changesets a directory has absorbed, but also which changesets it's still eligible to receive. 

The `svn mergeinfo` command requires a “source” URL (where the changes come from), and takes an optional “target”URL (where the changes merge to). If no target URL is given, it assumes that the current working directory is the target.

```shell
# Which changes have already been merged from trunk to branch?
svn mergeinfo ^/calc/trunk --show-revs merged
# Which changes are still eligible to merge from trunk to branch?
svn mergeinfo ^/calc/trunk --show-revs eligible
# an abstract graph display
svn mergeinfo ^/calc/trunk
```

#### Undoing changes

Another use for `svn merge` is to roll back a change that has already been commited, since `svn revert` can not deal this situation. `svn merge ` not only can add the diff but also can remove the diff.

```shell
svn merge url -c -33 ./ # remove the change of r33 in url
```

#### Resurrecting Deleted Items

Since theinformation in Svn repo is never lost, you can get your deleted file or directory back. Every object in the repository exists in a sort of two-dimensional coordinate system. The first coordinate is a particular revision tree, and the second coordinate is a path within that tree. 

First, use `svn log -v` to find out the revision that delete the file, and then `svn copy ` the file of that revision to the current working copy. 

```shell
cd ^/calc/trunk  # parent-dir
svn log -p
```

Then, get your file back. If the deletion of the file is the whole content of that revision change, you can use `svn merge` undo the changes to get the deleted file back. If there are a few operation of other files, you can use `svn revert` to discard the change.

```shell
svn merge ^/calc/trunk -c -[rid]
svn revert other-files
```

If the deletion is only the little part, you can use `svn copy` to simiply get the specified file back. 

```shell
svn copy ^/calc/trunk/deleted-file@[rid] ./deleted-file
```

The file that `svn copy` isn't really new. It's a direct descendant of the original, deleted file. Subversion copys it and remembers this operation. In the future, running `svn log` on this file will traverse back through the file's resurrection and through all the history it had prior to revision 807.

You can also create a new file with the same content of the deleted file, by using `svn copy`.

```shell
svn cat ^/calc/trunk/deleted-file@[rid] > ./deleted-file
svn add deleted-file
```



## 参考文献

1. [Version Control with Subversion](http://svnbook.red-bean.com/en/1.7/index.html)
2. [SVN 创建仓库操作](http://www.runoob.com/svn/svn-create-repo.html)
3. [centos搭建svn，解决认证失败问题](https://blog.csdn.net/wq3028/article/details/81459643)
4. [svn server运行和解决条目不可读问题 svn: E200001](https://www.158code.com/article/172)
5. [使用SVN命令行解决树冲突(tree conflict)](https://www.jianshu.com/p/e3cc83ca512d)
6. [SVN：代码回滚问题与switch](https://blog.51cto.com/janephp/1300561)