# Git

任务：

- Git教程，Beginner、Getting Started、Collaborating、Advanced Tips
- 尝试创建分支，合并到master，模拟出现代码冲突的情况，并解决冲突



## Beginner

### What is version control

Version control systems are a category of software tools that help a software team manage changes to source code over time. Version control software keeps track of every modification to the code in a special kind of database. If a mistake is made, developers can turn back the clock and compare earlier versions of the code to help fix the mistake while minimizing disruption to all team members.

Benefits of version control systems

- A complete long-term change history of every file.
- Branching and merging.
- Traceability.

### What is Git

By far, the most widely used modern version control system in the world today is Git. Git is a mature, actively maintained open source project originally developed in 2005 by Linus Torvalds.

Having a distributed architecture, Git is an example of a DVCS (hence Distributed Version Control System). Rather than have only one single place for the full version history of the software as is common in once-popular version control systems like CVS or Subversion (also known as SVN), in Git, every developer's working copy of the code is also a repository that can contain the full history of all changes.

It’s important to understand that Git’s idea of a “working copy” is very different from the working copy you get by checking out source code from an SVN repository. Unlike SVN, Git makes no distinction between the working copies and the central repository—they're all full-fledged Git repositories.

This makes collaborating with Git fundamentally different than with SVN. Whereas SVN depends on the relationship between the central repository and the working copy, Git’s collaboration model is based on repository-to-repository interaction. Instead of checking a working copy into SVN’s central repository, you push or pull commits from one repository to another.

Of course, there’s nothing stopping you from giving certain Git repos special meaning. For example, by simply designating one Git repo as the “central” repository, it’s possible to replicate a centralized workflow using Git. This is accomplished through conventions rather than being hardwired into the VCS itself.

In addition to being distributed, Git has been designed with performance, security and flexibility in mind.

#### Performance

The raw performance characteristics of Git are very strong when compared to many alternatives. Committing new changes, branching, merging and comparing past versions are all optimized for performance.

The algorithms implemented inside Git take advantage of deep knowledge about common attributes of real source code file trees, how they are usually modified over time and what the access patterns are.

The object format of Git's repository files uses a combination of delta encoding (storing content differences), compression and explicitly stores directory contents and version metadata objects.

#### Security

Git has been designed with the integrity of managed source code as a top priority.

e content of the files as well as the true relationships between files and directories, versions, tags and commits, all of these objects in the Git repository are secured with a cryptographically secure hashing algorithm called SHA1. 

#### Flexibility

Git is flexible in several respects: in support for various kinds of nonlinear development workflows, in its efficiency in both small and large projects and in its compatibility with many existing systems and protocols.

### Version control with Git

Git is the best choice for most software teams today.

- Git is good. Git has the functionality, performance, security and flexibility that most teams and individual developers need.
- Git is a de facto standard. Git is the most broadly adopted tool of its kind.
- Git is a quality open source project. The quality of the open source software is easily scrutinized. Git enjoys great community support and a vast user base. Documentation is excellent and plentiful, including books, tutorials and dedicated web sites. Being open source lowers the cost for hobbyist developers as they can use Git without paying a fee.

### Why Git for your organization

 Git isn’t just for agile software development—it’s for agile business.

#### Git for developers

- Feature Branch Workflow 
  Feature branches provide an isolated environment for every change to your codebase. When a developer wants to start working on something—no matter how big or small—they create a new branch. This ensures that the master branch always contains production-quality code.
- Distributed Development
  In SVN, each developer gets a working copy that points back to a single central repository. Git, however, is a distributed version control system. Instead of a working copy, each developer gets their own local repository, complete with a full history of commits.
  Having a full local history makes Git fast, since it means you don’t need a network connection to create commits, inspect previous versions of a file, or perform diffs between commits.
  Distributed development also makes it easier to scale your engineering team. If someone breaks the production branch in SVN, other developers can’t check in their changes until it’s fixed. With Git, this kind of blocking doesn’t exist. Everybody can continue going about their business in their own local repositories.
  And, similar to feature branches, distributed development creates a more reliable environment. Even if a developer obliterates their own repository, they can simply clone someone else’s and start a new.
- Pull Requests
  A pull request is a way to ask another developer to merge one of your branches into their repository. 
  This not only makes it easier for project leads to keep track of changes, but also lets developers initiate discussions around their work before integrating it with the rest of the codebase.
  When a developer gets stuck with a hard problem, they can open a pull request to ask for help from the rest of the team. 
  Alternatively, junior developers can be confident that they aren’t destroying the entire project by treating pull requests as a formal code review.
- Community
  In many circles, Git has come to be the expected version control system for new projects. If your team is using Git, odds are you won’t have to train new hires on your workflow, because they’ll already be familiar with distributed development. In addition, Git is very popular among open source projects. This means it’s easy to leverage 3rd-party libraries and encourage others to fork your own open source code.
- Faster Release Cycle
  These capabilities facilitate an agile workflow where developers are encouraged to share smaller changes more frequently. In turn, changes can get pushed down the deployment pipeline faster than the monolithic releases common with centralized version control systems.

#### Git for marketing

If you’re using a traditional development workflow that relies on a centralized VCS, all of these changes would probably be rolled up into a single release. Marketing can only make one announcement that focuses primarily on the game-changing feature, and the marketing potential of the other two updates is effectively ignored.

The shorter development cycle facilitated by Git makes it much easier to divide these into individual releases. This gives marketers more to talk about, more often. In the above scenario, marketing can build out three campaigns that revolve around each feature, and thus target very specific market segments.

#### Git for product management

More frequent releases means more frequent customer feedback and faster updates in reaction to that feedback. 

The feature branch workflow also provides flexibility when priorities change.

#### Git for designers

Feature branches lend themselves to rapid prototyping. Whether your UX/UI designers want to implement an entirely new user flow or simply replace some icons, checking out a new branch gives them a sandboxed environment to play with. 

Encapsulating user interface changes like this makes it easy to present updates to other stakeholders.

Pull requests take this one step further and provide a formal place for interested parties to discuss the new interface.

Perhaps the best part of prototyping with branches is that it’s just as easy to merge the changes into production as it is to throw them away. 

#### Git for customer support

Git’s streamlined development cycle avoids postponing bug fixes until the next monolithic release. A developer can patch the problem and push it directly to production. 

Faster fixes means happier customers and fewer repeat support tickets.

#### Git for anyone managing a budget

Git is all about efficiency.

### Install Git

Debian / Ubuntu (apt-get)

```shell
$ sudo apt-get update
$ sudo apt-get install git
```

Configure your Git username and email using the following commands. These details will be associated with any commits that you create:

```shell
$ git config --global user.name "Emma Paris"
$ git config --global user.email "eparis@atlassian.com"
```



## Getting Started

### Setting up a repository

A Git repository is a virtual storage of your project. It allows you to save versions of your code, which you can access when needed. 

#### git init - Initializing a new repository

To create a new repo, you'll use the `git init` command. `git init` is a one-time command you use during the initial setup of a new repo. 

Executing this command will create a new `.git`subdirectory in your current working directory, which contains all of the necessary Git metadata for the new repository. This metadata includes subdirectories for objects, refs, and template files. A `HEAD` file is also created which points to the currently checked out commit.

This will also create a new master branch. 

```shell
cd /path/to/your/existing/code
git init
```

or

```shell
git init <project directory>
```

If a project directory already has contained a `.git` configuration,  `git init` again will not override an existing `.git` configuration.

Initialize an empty Git repository, but omit the working directory. Shared repositories should always be created with the `--bare` flag. Conventionally, repositories initialized with the `--bare` flag end in `.git`. 

```shell
git init --bare <directory>
```

The `--bare` flag creates a repository that doesn’t have a working directory, making it impossible to edit files and commit changes in that repository. You would create a bare repository to git push and git pull from, but never directly commit to it. Central repositories should always be created as bare repositories because pushing branches to a non-bare repository has the potential to overwrite changes. Think of `--bare` as a way to mark a repository as a storage facility, as opposed to a development environment.

```shell
git init <directory> --template=<template_directory>
```

Initializes a new Git repository and copies files from the  `<template_directory>` into the repository. A powerful feature of templates that's exhibited in the default templates is Git Hook configuration. You can create a template with predefined Git hooks and initialize your new git repositories with common hooks ready to go.

#### git clone - Cloning an existing repository

`git clone` is used to create a copy or clone of remote repositories. You pass `git clone` a repository URL. When executed, the latest version of the remote repo files on the master branch will be pulled down and added to a new folder. The folder will contain the full history of the remote repository and a newly created master branch.

```shell
git clone <repo url>
```

`git clone ` will automatically configure your repo with a remote pointed to the Git URL you cloned it from. This means that once you make changes to a file and commit them, you can `git push`those changes to the remote repository.

```shell
git clone -branch <branch_name> <repo url>
git clone -branch <tag_name> <repo url>
```

The `-branch` argument lets you specify a specific a branch to clone instead of the branch the remote `HEAD` is pointing to, usually the master branch. In addition you can pass a tag instead of branch for the same effect. This is purely a convince utility to save you time from downloading the `HEAD` ref of the repository and then having to additionally fetch the ref you need.

```shell
git clone --depth 1 <repo>
```

Shallow clone. Clone the repository located at `<repo>` and only clone the history of commits specified by the option depth=1. In this example a clone of `<repo>` is made and only the most recent commit is included in the new cloned Repo. 

```shell
git fetch --unshallow
```

The command will change a shallow clone into a full clone.

```shell
git clone --bare <repo>
```

Similar to `git init --bare,` when the `-bare` argument is passed to `git clone,` a copy of the remote repository will be made with an omitted working directory. 

#### git add and git commit - Saving changes to the repository

Example

```shell
cd /path/to/project
echo "test content for git tutorial" >> CommitTest.txt
git add CommitTest.txt
git commit -m "added CommitTest.txt to the repo"
```

Add changes to the repository staging area and create a new commit with a message describing what work was done in the commit.

Another common use case for `git add` is the `--all` option. Executing `git add --all` will take any changed and untracked files in the repo and add them to the repo and update the repo's working tree.

#### git push - Repo-to-repo collaboration

Push or pull commits from one repository to another.

If you used `git init` to make a fresh repo, you'll have no remote repo to push changes to. A common pattern when initializing a new repo is to go to a hosted Git service like Bitbucket and create a repo there. The service will provide a Git URL that you can then add to your local Git repository and `git push` to the hosted repo. 

Add a remote repo url to your local repo. Map remote repository at `<remote_repo_url>`to a ref in your local repo under `<remote_name>`.

```shell
git remote add <remote_name> <remote_repo_url>
```

Once you have mapped the remote repo you can push local branches to it.

```shell
git push -u <remote_name> <local_branch_name>
```

If you used `git clone ` to set up your local repository, your repository is already configured for remote collaboration. It means that you can `git push` changes and commits to the remote repository.

#### git config - Configuration & set up

The `git config` command lets you configure your Git installation (or an individual repository) from the command line. This command can define everything from user info, to preferences, to the behavior of a repository. 

Git stores configuration options in three separate files:

- Local(individual repositories): `<repo>/.git/config` – Repository-specific settings.
- Global(user): `~/.gitconfig` – User-specific settings. 
  This is where options set with the --global flag are stored.
- System(entire system): `$(prefix)/etc/gitconfig` – System-wide settings.

When options in these files conflict, local settings override user settings, which override system-wide. 

Example:

Tell Git who you are.

```shell
git config --global user.name "John Smith"
git config --global user.email john@example.com
```

Select your favorite text editor.

```shell
git config --global core.editor vim
```

Add some SVN-like aliases.

```shell
git config --global alias.st status
git config --global alias.co checkout
git config --global alias.br branch
git config --global alias.up rebase
git config --global alias.ci commit
```

### Saving changes

Saving changes in Git vs SVN is a different process. SVN Commits or 'check-ins' are operations that make a remote push to a centralized server. This means an SVN commit needs Internet access in order to fully 'save' project changes. Git commits can be captured and built up locally, then pushed to a remote server as needed using the `git push -u origin master` command. The difference between the two methods is a fundamental difference between architecture designs. Git is a distributed application model whereas SVN is a centralized model. Distributed applications are generally more robust as they do not have a single point of failure like a centralized server.

#### git add

The `git add` command adds a change in the working directory to the staging area. It tells Git that you want to include updates to a particular file in the next commit. However, `git add` doesn't really affect the repository in any significant way—changes are not actually recorded until you run `git commit`.

The `git add` and `git commit` commands compose the fundamental Git workflow. 

First, you edit your files in the working directory. When you’re ready to save a copy of the current state of the project, you stage changes with `git add`. After you’re happy with the staged snapshot, you commit it to the project history with `git commit`. The `git reset` command is used to undo a commit or staged snapshot.

The primary function of the `git add` command, is to promote pending changes in the working directory, to the `git staging`area. It helps to think of it as a buffer between the working directory and the project history. Instead of committing all of the changes you've made since the last commit, the stage lets you group related changes into highly focused snapshots before actually committing it to the project history. As in any revision control system, it’s important to create atomic commits so that it’s easy to track down bugs and revert changes with minimal impact on the rest of the project.

The `git add` command should not be confused with `svn add`, which adds a file to the repository. Instead, `git add` works on the more abstract level of changes. This means that `git add` needs to be called every time you alter a file, whereas `svn add` only needs to be called once for each file.

Stage all changes in `<file>` for the next commit.

```shell
git add <file>
```

Stage all changes in `<directory>` for the next commit.

```shell
git add <directory>
```

Begin an interactive staging session that lets you choose portions of a file to add to the next commit. 

```shell
git add -p
```

Use `y` to stage the chunk, `n` to ignore the chunk, `s` to split it into smaller chunks, `e` to manually edit the chunk, and `q` to exit.

`git add` will change the stage index. `git ls-files -s` to show the snapshot id of stage index.

```shell
$ git ls-files -s
100644 67cc52710639e5da6b515416fd779d0741e3762e 0 reset_lifecycle_file
$ git add reset_lifecycle_file
100644 d7d77c1b04b5edd5acfc85de0b592449e5303770 0 reset_lifecycle_file
```

#### git commit

The `git commit` command captures a snapshot of the project's currently staged changes. Committed snapshots can be thought of as “safe” versions of a project—Git will never change them unless you explicitly ask it to.

While they share the same name, `git commit` is nothing like `svn commit`. In SVN, a commit pushes changes from the local SVN client, to a remote centralized shared SVN repository. In Git, repositories are distributed, Snapshots are committed to the local repository, and this requires absolutely no interaction with other Git repositories. Git commits can later be pushed to arbitrary remote repositories.

At a high-level, Git can be thought of as a timeline management utility. Commits can be thought of as snapshots or milestones along the timeline of a Git project. Snapshots, not differences. A SVN commit consists of a diff compared to the original file added to the repository. Git, on the other hand, records the entire contents of each file in every commit. This makes many Git operations much faster than SVN.

Commit the staged snapshot. This will launch a text editor prompting you for a commit message. 

```shell
git commit
```

A shortcut command that immediately creates a commit with a passed commit message. 

```shell
git commit -m "commit message"
```

Modify the last commit message.

```shell
git commit --amend
```

#### git diff

Diffing is a function that takes two input data sets and outputs the changes between them. These data sources can be commits, branches, files and more. A diff only displays the sections of the file that have changes. 

The remaining diff output is a list of diff 'chunks'. The first line is the chunk header. Each chunk is prepended by a header inclosed within `@@` symbols. `@@ -34,6 +34,8 @@` means 6 lines have been extracted starting from line number 34, 8 lines have been added starting at line number 34. The remaining content of the diff chunk displays the recent changes. `-` indicates changes from the input and `+` indicates changes from output.

Compare changes across the entire repository.

```shell
git diff
```

Compare file with local repository, showing the changes that are not staged yet.

```shell
git diff <file>
```

Compare the staged file with repository, showing the changes that has been staged.

```shell
git diff --cached <file>
git diff --staged <file>
```

Compare files between towo different commmit/branch.

```shell
git diff <commit-ID1/branch1> <commit-ID2/branch2>
```

Comparing files from two branches

```shell
git diff <commit-ID1/branch1> <commit-ID2/branch2> <file>
```

Diff the current master branch against 4 commit before master.

```
git diff master@{0} master@{4}
```

Every reflog entry has a timestamp attached to it. These timestamps can be leveraged as the `qualifier` token of Git ref pointer syntax. This enables filtering Git reflogs by time. eg. 

```
1.hour.ago		1.day.ago	yesterday	1.week.ago	1.month.ago
2011-05-17.09:00:00
```

Diff the current master branch against master 1 day ago.

```shell
git diff master@{0} master@{1.day.ago}
```

#### git stash

Git has an additional saving mechanism called 'the stash'. The stash is an ephemeral storage area for changes that are not ready to be committed. `git stash` temporarily shelves (or *stashes*) changes you've made to your working copy so you can work on something else, and then come back and re-apply them later on. 

The `git stash` command takes your uncommitted changes (both staged and unstaged), saves them away for later use, and then reverts them from your working copy.

```shell
git stash
```

Reapply previously stashed changes. Popping your stash removes the changes from your stash and reapplies them to your working copy.

```shell
git stash pop
```

Alternatively, you can reapply the changes to your working copy *and* keep them in your stash.

```shell
git stash apply
```

By default Git *won't* stash changes made to untracked or ignored files. It will stash changes that have been added to your index (staged changes), and changes made to files that are currently tracked by Git (unstaged changes).

To stash untracked files.

```shell
git stash -u 
```

To stash untracked or ignored files.

```shell
git stash -all
```

You can run `git stash` several times to create multiple stashes, and then use `git stash list` to view them.

```shell
git stash list
```

By default, stashes are identified simply as a "WIP" – work in progress – on top of the branch and commit that you created the stash from. 

After a while it can be difficult to remember what each stash contains. To provide a bit more context, it's good practice to annotate your stashes with a description.

```shell
git stash save "description help remember"
```

By default, `git stash pop` will re-apply the most recently created stash:  `stash@{0}`. You can choose which stash to re-apply by passing its identifier as the last argument.

```shell
git stash pop stash@{2}
```

View stash diffs. `git stash show` for a summary of a stash. Pass the `-p` option (or `--patch`) to view the full diff of a stash

```shell
git stash show -p
```

You can also choose to stash just a single file, a collection of files, or individual changes from within files. it will iterate through each changed "hunk" in your working copy and ask whether you wish to stash it.

```shell
git stash -p
```

`/`: search for a hunk by regex, `?`: help, `n`:  don't stash this hunk, `q`: quit (any hunks that have already been selected will be stashed), `s`: split this hunk into smaller hunks, `y`: stash this hunk. `CTRL-C` will abort the stash process.

Stashes are actually encoded in your repository as commit objects. A stash itself is a commit saving changes of tracked files, with 3 parents: the pre-existing commit, a commit saving staged changes, a commit saving changes of untracked files and ignored files.

#### .gitignore

Ignored files are usually build artifacts and machine generated files that can be derived from your repository source or should otherwise not be committed.

Ignored files are tracked in a special file named `.gitignore` that is checked in at the root of your repository. It contain patterns that are matched against file names in your repository to determine whether or not they should be ignored.

```shell
**/logs				# 匹配所有目录下名为logs的目录，忽略logs目录及其内部所有文件
**/logs/debug.log	# 匹配所有目录下名为logs的目录，忽略期内debug.log文件
*.log				# 匹配并忽略所有后缀为.log的文件
!important.log		# 不匹配所有目录下的important.log文件
/debug.log			# 仅匹配根目录下的debug.log文件
debug.log			# 匹配并忽略所有目录下的debug.log文件
debug?.log			# ？指代任意一个字母，匹配并忽略所有目录下匹配的文件
debug[0-9].log		# [0-9]指代0-9内任意一个数字，匹配并忽略所有目录下匹配的文件
debug[01].log		# [01]指代字符0或1，匹配并忽略所有目录下匹配的文件
debug[!01].log		# [!01]指代一个非0和1的字符，匹配并忽略所有目录下匹配的文件
debug[a-z].log		# [a-z]指代a-z内任意一个字母，匹配并忽略所有目录下匹配的文件
logs				# 匹配并忽略所有目录下名为logs的目录或文件，若为目录则同样忽略其内部所有文件
logs/				# 匹配并忽略所有目录下名为logs的目录，忽略其内部所有文件
logs/**/debug.log	# **可指代0个或1个目录，匹配并忽略所有目录下匹配的文件
logs/*day/debug.log	# *指代0或多个字符，匹配并忽略所有目录下匹配的文件
logs/debug.log		# 仅匹配根目录的logs/debug.log文件
```

You can use \ to escape `.gitignore` pattern characters if you have files or directories containing them.

you can define global Git ignore patterns for all repositories on your local system.

```shell
git config --global core.excludesFile ~/.gitignore
```

If you want to ignore a file that you've committed in the past, you'll need to delete the file from your repository and then add a `.gitignore` rule for it. Using the `--cached` option with `git rm`means that the file will be deleted from your repository, but will remain in your working directory as an ignored file.

```shell
echo debug.log >> .gitignore
git rm --cached debug.log
rm 'debug.log'
git commit -m "Start ignoring debug.log"
```

It is possible to force an ignored file to be committed to the repository using the `-f` (or `--force`) option with `git add`.

```shell
git add -f debug.log
```

### Inspecting a repository

####git status

The `git status` command displays the state of the working directory and the staging area. t lets you see which changes have been staged, which haven’t, and which files aren’t being tracked by Git.

#### git log

The `git log` command displays committed snapshots. 

Display the entire commit history using the default formatting.

```shell
git log
```

Limit the number of commits by `<limit>`. 

```shell
git log -n <limit>
```

Only display commits that include the specified file.

```shell
git log <file>
```

Display the patch representing each commit. 

```shell
git log -p
```

Display the commits that contain or remove pattern.

```shell
git log -S "pattern"
```

Search for commits with a commit message that matches `<pattern>`

```shell
git log --grep="<pattern>"
```

A few useful options to consider.  

```shell
git log --graph --decorate --oneline
```

View all commits across all branches.

```shell
git log --branches=*
```

建议安装qgit看commit历史。

#### git tag

Tags are ref's that point to specific points in Git history. Tagging is generally used to capture a point in history that is used for a marked version release.

Git supports two different types of tags, annotated and lightweight tags.

Lightweight tags are essentially 'bookmarks' to a commit, they are just a name and a pointer to a commit, useful for creating quick links to relevant commits.

To create a new lightweight  tag execute the following command

```shell
git tag <tagname>
```

Annotated tags store extra meta data such as: the tagger name, email, and date. Similar to commits and commit messages , annotated tags have a tagging message. 

```shell
git tag -a v1.4
git tag -a v1.4 -m "my version 1.4"
```

To list stored tags in a repo.

```shell
git tag
```

To refine the list of tags the `-l` option can be passed with a wild card expression.

```shell
git tag -l *-rc*
```

Tagging old commits.

```shell
git tag -a v1.2 15027957951b64cf874c3557a0f3547bd83b3ff6
```

Create a tag with the same identifier as an existing tag. It will override old tag.

```shell
git tag -a -f v1.4 15027957951b64cf874c3557a0f3547bd83b3ff6
```

Sharing tags is similar to pushing branches. By default, `git push`will not push tags. Tags have to be explicitly passed to `git push`.

```shell
git push origin v1.4
```

Checking out tags.

```shell
git checkout v1.4
```

The above command will checkout the `v1.4` tag. This puts the repo in a detached `HEAD` state. This means any changes made will not update the tag. They will create a new detached commit. This new detached commit will not be part of any branch and will only be reachable directly by the commits SHA hash. Therefore it is a best practice to create a new branch anytime you're making changes in a detached `HEAD` state.

Deleting tags.

```shell
git tag -d v1
```

#### git blame

The high-level function of `git blame` is the display of author metadata attached to specific committed lines in a file. This is used to examine specific points of a file's history and get context as to who the last author was that modified the line. `Git blame` is often used with a GUI display.

`git blame` only operates on individual files.

```shell
git blame <file>
```

`git blame`列出文件的内容，并指出每一行最后是由谁什么时间在哪次提交中修改的。

The `-L` option will restrict the output to the requested line range. 

```shell
git blame -L 1,5 README.md
```

The `-w` option ignores whitespace changes.

```shell
git blame -w README.md
```

### Undoing Commits & Changes

When 'undoing' in Git, you are usually moving back in time, or to another timeline where mistakes didn't happen.

To properly understand `changes, we must first understand Git's internal state management systems. Sometimes these mechanisms are called Git's "three trees".

The first tree we will examine is "The Working Directory". This tree is in sync with the local filesystem and is representative of the immediate changes made to content in files and directories.

Next up is the 'Staging Index' tree. This tree is tracking Working Directory changes, that have been promoted with `git add`, to be stored in the next commit.

 The final tree is the Commit History. The `git commit` command adds changes to a permanent snapshot that lives in the Commit History. This snapshot also includes the state of the Staging Index at the time of commit.

#### git checkout

Review a commit or a branch.

```shell
git checkout <branch/commitID>
```

Checking out a specific commit will put the repo in a "detached HEAD" state. This means you are no longer working on any branch. In a detached state, any new commits you make will be orphaned when you change branches back to an established branch. Orphaned commits are up for deletion by Git's garbage collector. The garbage collector runs on a configured interval and permanently destroys orphaned commits. To prevent orphaned commits from being garbage collected, we need to ensure we are on a branch.

Create a branch at this point.

```shell
git checkout -b <new_branch>
```

`git checkout` can also be used to drop changes.

```shell
git checkout -- <file>
```

`-f` option will drop all changes of working directory and staged index. It has the same performance with `git reset --hard HEAD`.

```shell
git checkout -f
```

#### git clean

`Git clean` can be considered complementary to other commands like `git reset` and `git checkout`. Whereas these other commands operate on files previously added to the Git tracking index, the `git clean` command operates on untracked files.

By default, Git is globally configured to require that `git clean` be passed a "force" option to initiate. This is an important safety mechanism. When finally executed `git clean` is not undo-able. 

The `-n` option will perform a “dry run” of `git clean`. This will show you which files are going to be removed without actually removing them.

```shell
git clean -n
```

The `-f` option initiates the actual deletion of untracked files from the current directory, not iteratively. Additionally, a <path> value can be passed with the `-f` option that will remove a specific file.

```shell
git clean -f
git clean -f <path>
```

The `-d` option tells `git clean` that you also want to remove any untracked directories, by default it will ignore directories. 'Dry run' first is a best practice.

```shell
git clean -dn
git clean -df
```

The `-x` option tells `git clean` to also include any ignored files. 

```shell
git clean -xn
git clean -xf
```

The `-X` option tells `git clean` to only include any ignored files. 

```shell
git clean -Xn
git clean -Xf
```

the `-i` option tells  `git clean` to behave in "interactive" mode.

```shell
git clean -di
```

#### git revert

The `git revert` command can be considered an 'undo' type command, however, it is not a traditional undo operation. Instead of removing the commit from the project history, it figures out how to invert the changes introduced by the commit and appends a new commit with the resulting inverse content. This prevents Git from losing history, which is important for the integrity of your revision history and for reliable collaboration.

It's **important** to understand that `git revert` undoes a **single** commit—it does not "revert" back to the previous state of a project by removing all subsequent commits. 

`git revert` is able to target an individual commit at an arbitrary point in the history, whereas `git reset` can only work backward from the current commit. For example, if you wanted to undo an old commit with `git reset`, you would have to remove all of the commits that occurred after the target commit, remove it, then re-commit all of the subsequent commits. Needless to say, this is not an elegant undo solution.

To revert the latest change.

```shell
git revert HEAD
```

To revert the change of a specfied commit.

```shell
git revert <commitID>
```

若两次提交在相同位置添加或修改，revert到第一次提交时会产生conflict。相同位置修改会产生冲突已理解，连续添加的情况还不能理解。

If revert make conflict, modify the both modified file, then add it and continue reverting.

```shell
git revert <commitID>
git add <conflicted_file>
git revert --continue
```

The revert will not open the editor.

```shell
git revert -e <commitID>
```

Passing `-n` will prevent `git revert` from creating a new commit that inverses the target commit. Instead of creating the new commit this option will add the inverse changes to the Staging Index and Working Directory. 

```shell
git revert -n <commitID>
```

#### git reset

The `git reset` command is a complex and versatile tool for undoing changes. It has three primary forms of invocation. These forms correspond to command line arguments `--soft, --mixed, --hard`, which direct how to modify the Staging Index, and Working Directory trees.

`--hard`  is the most direct, DANGEROUS, and frequently used option. When passed `--hard` The Commit History ref pointers are updated to the specified commit. Then, the Staging Index and Working Directory are reset to match that of the specified commit. All pending work in Staging Index and Working Directory will lost.

`--mixed` is the default operating mode. The ref pointers are updated. The Staging Index is reset to the state of the specified commit. Any changes that have been undone from the Staging Index are moved to the Working Directory.

`--soft` is the weakest operating mode. The ref pointers are updated and the reset stops there. The Staging Index and the Working Directory are left untouched. However, as a reminder, `git status` does not show the state of 'the three trees', it essentially shows a diff between them. In this case, it is displaying that the Staging Index is ahead of the changes in the Commit History as if we have already staged them.

The default invocation of `git reset` has implicit arguments of `--mixed` and `HEAD`. 

```shell
git reset
```

More general

```shell
git reset --<option> <commitID>
```

Doing a reset is great for local changes however it adds complications when working with a shared remote repository. If we have a shared remote repository that has the `872fa7e` commit pushed to it, and we try to `git push` a branch where we have reset the history, Git will catch this and throw an error. Git will assume that the branch being pushed is not up to date because of it's missing commits. In these scenarios, `git revert` should be the preferred undo method.

Whereas reverting is designed to safely undo a public commit, `git reset` is designed to undo local changes to the Staging Index and Working Directory. Because of their distinct goals, the two commands are implemented differently: resetting completely removes a changeset, whereas reverting maintains the original changeset and uses a new commit to apply the undo.

#### git rm

The `git rm`command is used to remove files from a Git repository. It can be thought of as the inverse of the `git add` command.  It tells Git not to track a file (or files) any more.

The `git rm` command operates on the current branch only. The file removal is not persisted to the repository history until a new commit is created.

Like `git clean`, `git rm` also have a "dry run" mode.

```shell
git rm -n <files>...
```

The `-r` option is shorthand for 'recursive'.

```shell
git -r <files>...
```

The `-f `option is used to override the safety check.

````shell
git -f <files>...
````

The cached option specifies that the removal should happen only on the staging index. Working directory files will be left alone.

```shell
git --cached <files>...
```

Executing `git rm` is not a permanent update. The command will update the staging index and the working directory. These changes will not be persisted until a new commit is created and the changes are added to the commit history. This means that the changes here can be "undone" using common Git commands.

A reset will revert the current staging index and working directory back to the `HEAD` commit.

```shell
git reset HEAD
```

A checkout will have the same effect and restore the latest version of a file from `HEAD`.

```shell
git checkout .
```

### Rewinding history

Git has several mechanisms for storing history and saving changes. These mechanisms include: Commit `--amend`, `git rebase` and `git reflog`.

#### git commit --amend

The `git commit --amend` command is a convenient way to modify the most recent commit. It can be used to simply edit the previous commit message without changing its snapshot. It also lets you combine staged changes with the previous commit instead of creating an entirely new commit. But, amending does not just alter the most recent commit, it replaces it entirely, meaning the amended commit will be a new entity with its own ref. 

Let's say you just committed and you made a mistake in your commit log message. Running this command when there is nothing staged lets you edit the previous commit’s message without altering its snapshot.

```shell
git add a.file
git commit -m "add x.file"
git commit --amend -m "add a.file"
```

Let's say we've edited a few files that we would like to commit in a single snapshot, but then we forget to add one of the files the first time around. Fixing the error is simply a matter of staging the other file and committing with the `--amend` flag.

```shell
git add a.file
git commit -m "add a.file b.file"
git add b.file
git commit --amend --no-edit
```

Amended commits are actually entirely new commits and the previous commit will no longer be on your current branch. This has the same consequences as resetting a public snapshot. Don’t amend public commits.

#### git rebase

Rebasing is the process of moving or combining a sequence of commits to a new base commit. From a content perspective, rebasing is changing the base of your branch from one commit to another making it appear as if you'd created your branch from a different commit.

Internally, Git accomplishes this by creating new commits and applying them to the specified base. It's very important to understand that even though the branch looks the same, it's composed of entirely new commits.

The primary reason for rebasing is to maintain a linear project history. For example, consider a situation where the master branch has progressed since you started working on a feature branch. You want to get the latest updates to the master branch in your feature branch, but you want to keep your branch's history clean so it appears as if you've been working off the latest master branch. This gives the later benefit of a clean merge of your feature branch back into the master branch. 

![Git tutorial: Git rebase](https://wac-cdn.atlassian.com/dam/jcr:e4a40899-636b-4988-9774-eaa8a440575b/02.svg?cdnVersion=le)

Rebasing is a common way to integrate upstream changes into your local repository. Pulling in upstream changes with Git merge results in a superfluous merge commit every time you want to see how the project has progressed. On the other hand, rebasing is like saying, “I want to base my changes on what everybody has already done.”

You should never rebase commits once they've been pushed to a public repository. The rebase would replace the old commits with new ones and it would look like that part of your project history abruptly vanished.

Git rebase in standard mode will automatically take the commits in your current working branch and apply them to the head of the passed branch.

```shell
git rebase <base>
```

Git rebase in an interactive mode will gives you the opportunity to alter individual commits in the process.

```shell
git rebase -i <base>
```

During a rebase, you can run a few commands on commits to modify commit messages.

- Reword or 'r' will stop rebase playback and let you rewrite the individual commit message during.
- Squash or 's' during rebase playback, any commits marked `s`will be paused on and you will be prompted to edit the separate commit messages into a combined message. More on this in the squash commits section below.
- Fixup or 'f' has the same combining effect as squash. Unlike squash, fixup commits will not interrupt rebase playback to open an editor to combine commit messages. The commits marked 'f' will have their messages discarded in-favor of the previous commit's message.

Most developers like to use an interactive rebase to polish a feature branch before merging it into the main code base. This gives them the opportunity to squash insignificant commits, delete obsolete ones, and make sure everything else is in order before committing to the “official” project history. To everybody else, it will look like the entire feature was developed in a single series of well-planned commits.

`git rebase --onto` can change the base of a branch.

```shell
git rebase --onto <new_base> <old_base> <branch>
```

One caveat to consider when working with Git Rebase is merge **conflicts** may become more frequent during a rebase workflow. The `--continue` and `--abort` command line arguments can be passed to `git rebase` to advance or reset the the rebase when dealing with conflicts.

A more serious rebase caveat is lost commits from interactive history rewriting. Running rebase in interactive mode and executing subcommands like squash or drop will remove commits from your branche's immediate log. 

#### git reflog

Git keeps track of updates to the tip of branches using a mechanism called reference logs, or "reflogs." In addition to branch tip reflogs, a special reflog is maintained for the Git stash. 

The most basic Reflog use case is invoking `git reflog `, which  is essentially a short cut that's equivalent to

```shell
git reflog
git reflog show HEAD
```

By default, `git reflog` will output the reflog of the `HEAD` ref. `HEAD`is a symbolic reference to the currently active branch. 

Reflogs are available for other refs as well. The syntax to access a git ref is `name@{qualifier}`. In addition to `HEAD` refs, other branches, tags, remotes, and the Git stash can be referenced as well.

```shell
git reflog show <other_branch>
```

You can get a complete reflog of all refs by executing:

```shell
git reflog show -all
```

To output a reflog for the Git stash.

```shell
git reflog stash
```

## Collaborating

### Syncing

SVN uses a single centralized repository to serve as the communication hub for developers, and collaboration takes place by passing changesets between the developers’ working copies and the central repository.  Users commit a changeset from a working copy to the central repository.

This is different from Git's distributed collaboration model, which gives every developer their own copy of the repository, complete with its own local history and branch structure. Users typically need to share a series of commits rather than a single changeset. In addtion, Git lets you share entire branches between repositories.

#### git remote

The `git remote` command lets you create, view, and delete connections to other repositories. 

The `git remote` command is essentially an interface for managing a list of remote entries that are stored in the repository's `./.git/config` file.

List the remote connections you have to other repositories. Pass `-v` will include the URL of each connection.

```shell
git remote -v
```

Create a new connection to a remote repository. 

```shell
git remote add <name> <url>
```

Remove the connection to the remote repository called `<name>`.

```shell
git remote rm <name>
```

Rename a remote connection from <old-name> to <new-name>.

```shell
git remote rename <old-name> <new-name>
```

Modify a remote connection URL

```shell
git remote set-url <name> <new_url>
```

#### git fetch

The `git fetch` command downloads commits, files, and refs from a remote repository into your local repo. Fetching is what you do when you want to see what everybody else has been working on. 

It doesn’t force you to actually merge the changes into your repository. Git isolates fetched content as a from existing local content, it has absolutely no effect on your local development work. Fetched content has to be explicitly checked out using the `git checkout` command.

The refs for local branches are stored in the `./.git/refs/heads/`. Remote branch refs live in the `./.git/refs/remotes/` directory.

Fetch all of the branches from the repository. This also downloads all of the required commits and files from the other repository.

```shell
git fetch <remote>
```

Only fetch the specified branch.

```shell
git fetch <remote> <branch>
```

The `--dry-run` option will perform a demo run of the command. I will output examples of actions it will take during the fetch but not apply them.

```shell
git fetch --dry-run
```

Demo: fetch a branch and make a new branch

```shell
git fetch origin feature_branch
git checkout origin/feature_branch
git checkout -b <new_branch_name>
# or
git fetch origin feature_branch:<new_branch_name>
```

Demo: fetch a branch and merge to a local branch

```shell
git checkout <local_branch>
git fetch origin feature_branch
git log origin/feature_branch
git merge feature_branch
```

#### git push

The `git push` command is used to upload local repository content to a remote repository. Pushing is how you transfer commits from your local repository to a remote repo.

Push the specified branch to <remote>, along with all of the necessary commits and internal objects. 

```shell
git push <remote> <branch>
```

To prevent you from overwriting commits, Git won’t let you push when it results in a non-fast-forward merge in the destination repository. Pass `-f` will force the push even if it results in a non-fast-forward merge.

```shell
git push <remote> --force
```

Tags are not automatically pushed when you push a branch. The `--tags` flag sends all of your local tags to the remote repository.

```shell
git push <remote> <tag_name>
git push <remote> --tags
```

One of the standard methods for publishing local contributions to the central repository. 

```shell
git checkout master
git fetch origin master
git rebase -i origin/master
# Squash commits, fix up commit messages etc.
git push origin master
```

Modify the recent upload commit. But make sure none of your teammates have pulled the commit before using the `--force`option.

```shell
# make changes to a repo and git add
git commit --amend
# update the existing commit message
git push --force origin master
```

To delete a remote branch.

```shell
git push <remote> --delete <branch>
```

#### git pull

The `git pull` command is used to fetch and download content from a remote repository and immediately update the local repository to match that content.

The `git pull` command is actually a combination of two other commands, `git fetch` followed by `git merge`. 

Fetch the specified remote’s copy of the current branch and immediately merge it into the local copy.

```shell
git pull remote
```

Fetches the remote content and merge, but does not create a new commit at once.

```shell
git pull --no-commit <remote>
```

Fetches the remote content, and repeat all the changes and commit again on the local branch. NOTICE, these are totally new commit which GIT will serve them as the different commits with the remote commits.

```shell
git pull --rebase <remote>
```

### Using branches

Branching is a feature available in most modern version control systems. Branching in other VCS's can be an expensive operation in both time and disk space. Git branches are effectively a pointer to a snapshot of your changes.

#### git branch

When you want to add a new feature or fix a bug—no matter how big or how small—you spawn a new branch to encapsulate your changes. This makes it harder for unstable code to get merged into the main code base, and it gives you the chance to clean up your future's history before merging it into the main branch. By developing them in branches, it’s not only possible to work on both of them in parallel, but it also keeps the main `master` branch free from questionable code.

It's important to understand that branches are just pointers to commits. When you create a branch, all Git needs to do is create a new pointer.

Executing the `git branch` command will output a list of the local branch refs. 

```shell
git branch
```

Pass `-r` option will output a list of remote refs.

```shell
git branch -r
```

Create a new branch called `<branch>`. This does *not* check out the new branch.

```shell
git branch <branch_name>
```

Delete the specified branch. This is a “safe” operation in that Git prevents you from deleting the branch if it has unmerged changes.

```shell
git branch -d <branch_name>
```

Force delete the specified branch, even if it has unmerged changes.

```shell
git branch -D <branch_name>
```

Rename the current branch to `<new_branch_name>`.

```shell
git branch -m <new_branch_name
```

#### git checkout

In Git terms, a "checkout" is the act of switching between different versions of a target entity. The `git checkout` command operates upon three distinct entities: files, commits, and branches.

Checking out a branch updates the files in the working directory to match the version stored in that branch, and it tells Git to record all new commits on that branch. 

Switch to a specified branch.

```shell
git checkout <existing-branch>
```

Create the new branch and immediately switch to it. 

```shell
git checkout -b <new-branch>
```

By default `git checkout -b` will base the `new-branch` off the current `HEAD`. An optional additional branch parameter can be passed to `git checkout`.

```shell
git checkout <existing-branch> -b <new-branch>
```

Additionally you can checkout a new local branch and reset it to the remote branches last commit.

```shell
git checkout -b <branchname>
git reset --hard origin/<branchname>
```

`HEAD` is Git’s way of referring to the current snapshot. Internally, the `git checkout` command simply updates the `HEAD` to point to either the specified branch or commit. When it points to a branch, Git doesn't complain, but when you check out a commit, it switches into a `“detached HEAD”` state. All your work make on a `detached HEAD`, can not be get back if you check out another branch.

#### git merge

Merging is Git's way of putting a forked history back together again. The `git merge` command lets you take the independent lines of development created by `git branch` and integrate them into a single branch.

`git merge` takes two commit pointers, usually the branch tips, and will find a common base commit between them. Once Git finds a common base commit it will create a new "merge commit" that combines the changes of each queued merge commit sequence. 

A fast-forward merge can occur when there is a linear path from the current branch tip to the target branch. Instead of “actually” merging the branches, all Git has to do is move the current branch tip up to the target branch tip. 

However, a fast-forward merge is not possible if the branches have diverged. When there is not a linear path to the target branch, Git has no choice but to combine them via a 3-way merge. 3-way merges use three commits to generate the merge commit: the two branch tips and their common ancestor.

While you can use either of these merge strategies, many developers like to use fast-forward merges (facilitated through [rebasing](https://www.atlassian.com/git/tutorials/rewriting-history/git-rebase)) for small features or bug fixes, while reserving 3-way merges for the integration of longer-running features. In the latter case, the resulting merge commit serves as a symbolic joining of the two branches.

Demo: a fast-forward merge

```shell
# Start a new feature
git checkout -b new-feature master
# Edit some files
git add <file>
git commit -m "Start a feature"
# Edit some files
git add <file>
git commit -m "Finish a feature"
# Merge in the new-feature branch
git checkout master
git merge new-feature
git branch -d new-feature
```

Demo: 3-way merge

```shell
Start a new feature
git checkout -b new-feature master
# Edit some files
git add <file>
git commit -m "Start a feature"
# Edit some files
git add <file>
git commit -m "Finish a feature"
# Develop the master branch
git checkout master
# Edit some files
git add <file>
git commit -m "Make some super-stable changes to master"
# Merge in the new-feature branch
git merge new-feature
git branch -d new-feature
```

You can require a merge commit during a fast forward merge for record keeping purposes, by executing `git merge` with the `--no-ff`option.

```shell
git merge --no-ff <branch>
```

If the two branches you're trying to merge both changed the same part of the same file, Git won't be able to figure out which version to use. When such a situation occurs, it stops right before the merge commit so that you can resolve the conflicts manually.

Once you've identified conflicting sections, you can go in and fix up the merge to your liking. When you're ready to finish the merge, all you have to do is run `git add` on the conflicted file(s) to tell Git they're resolved. Then, you run a normal `git commit` to generate the merge commit.

### Comparing workflows

A Git Workflow is a recipe or recommendation for how to use Git to accomplish work in a consistent and productive manner. 

#### Centralized Workflow

The Centralized Workflow is a great Git workflow for teams transitioning from SVN.

The default development branch is called `master` and all changes are committed into this branch. This workflow doesn’t require any other branches besides `master`.

```shell
# John make some work
John:  git add <file>
John:  git commit -m "John make a commit"
# John push his work to central repo
John:  git push origin master
# Mary make some work
Mary:  git add <file>
Mary:  git commit -m "Mary make a commit"
# Mary pull other's work from central repo
Mary:  git pull --rebase origin master
# Maybe there's conflict, fix it
Mary:  git add <conflict-file>
Mary:  git rebase --continue
# Mary push his work to central repo
Mary:  git push origin master
```

#### Feature Branch Workflow

The core idea behind the Feature Branch Workflow is that all feature development should take place in a dedicated branch instead of the `master` branch.

This encapsulation makes it easy for multiple developers to work on a particular feature without disturbing the main codebase. It also means the `master` branch will never contain broken code, which is a huge advantage for continuous integration environments.

The Feature Branch Workflow assumes a central repository, and `master` represents the official project history. Instead of committing directly on their local `master` branch, developers create a new branch every time they start work on a new feature. Feature branches should have descriptive names, like animated-menu-items or issue-#1061. Feature branches can (and should) be pushed to the central repository. This makes it possible to share a feature with other developers without touching any official code.

```shell
# set up local repo
git checkout master
git fetch origin
git reset --hard origin/master
# create a branch for new feature
git checkout -b new-feature
git push -u origin new-feature
# make some work
git add <files>
git commit -m "make some work"
git push [origin] [new-feature]
# pull request or other method, code review
# modify work
git add <files>
git commit -m "modify work"
git push [origin] [new-feature]
# publish new feature
git checkout master
git pull [origin] [master]
git pull origin new-feature
git push [origin] [master]
```

#### Gitflow Workflow

The Gitflow Workflow defines a strict branching model designed around the project release. This provides a robust framework for managing larger projects. 

Gitflow is ideally suited for projects that have a scheduled release cycle. It assigns very specific roles to different branches and defines how and when they should interact. In addition to `feature` branches, it uses individual branches for preparing, maintaining, and recording releases. 

To make user use Gitflow easily, it provide a git-flow toolset, which is an actual command line tool that has an installation process.  For Debian9:

```shell
sudo apt install git-flow
```

Git-flow is a wrapper around Git.

Instead of a single `master` branch, this workflow uses two branches to record the history of the project. The `master` branch stores the official release history, and the `develop` branch serves as an integration branch for features. It's also convenient to tag all commits in the `master` branch with a version number.

![Git flow workflow - Historical Branches](https://wac-cdn.atlassian.com/dam/jcr:2bef0bef-22bc-4485-94b9-a9422f70f11c/02%20(2).svg?cdnVersion=le)

Each new feature should reside in its own branch, which can be pushed to the central repository for backup/collaboration. But, instead of branching off of `master`, `feature` branches use `develop` as their parent branch. When a feature is complete, it gets merged back into develop. Features should never interact directly with `master`. `Feature` branches are generally created off to the latest `develop` branch.

![Git flow workflow - Feature Branches](https://wac-cdn.atlassian.com/dam/jcr:b5259cce-6245-49f2-b89b-9871f9ee3fa4/03%20(2).svg?cdnVersion=le)

Once `develop` has acquired enough features for a release (or a predetermined release date is approaching), you fork a `release`branch off of `develop`. Creating this branch starts the next release cycle, so no new features can be added after this point—only bug fixes, documentation generation, and other release-oriented tasks should go in this branch. Once it's ready to ship, the `release`branch gets merged into `master` and tagged with a version number. In addition, it should be merged back into `develop`, which may have progressed since the release was initiated.

![Git Flow Workflow - Release Branches](https://wac-cdn.atlassian.com/dam/jcr:a9cea7b7-23c3-41a7-a4e0-affa053d9ea7/04%20(1).svg?cdnVersion=le)

Maintenance or `“hotfix”` branches are used to quickly patch production releases. `Hotfix` branches are a lot like `release`branches and `feature` branches except they're based on `master`instead of `develop`. This is the only branch that should fork directly off of `master`. As soon as the fix is complete, it should be merged into both `master` and `develop` (or the current `release`branch), and `master` should be tagged with an updated version number.

![Git flow workflow - Hotfix Branches](https://wac-cdn.atlassian.com/dam/jcr:61ccc620-5249-4338-be66-94d563f2843c/05%20(2).svg?cdnVersion=le)

Demo : without git-flow extensions

```shell
# ------------------- setup ----------------------
git branch develop
# ------------ develop a new feature -------------
# create a feature branch
git checkout develop -b feature_branch
# make some work
git add <file>
git commit -m "make some work"
# finish feature branch
git checkout develop
git merge feature_branch
# --------------- make a release -----------------
# create a release branch
git checkout develop -b release/0.1.0
# make some work
git add <file>
git commit -m "make some work"
# finish release branch
git checkout master
git merge release/0.1.0
# make tag
git tag v0.1.0 -m "v0.1.0"
# ---------------- make a hotfix -----------------
# create a hotfix branch
git checkout develop -b hotfix_branch
# make some work
git add <file>
git commit -m "make some work"
# finish hotfix branch
git checkout master
git merge hotfix_branch
git checkout develop
git merge hotfix_branch
git branch -D hotfix_branch
```

Demo: with git-flow extensions

```shell
# ------------------- setup ----------------------
git flow init
# ------------ develop a new feature -------------
# create a feature branch
git flow feature start feature_branch
# make some work
git add <file>
git commit -m "make some work"
# finish feature branch
git flow feature finish feature_branch
# --------------- make a release -----------------
# create a release branch
git flow release start 0.1.0
# make some work
git add <file>
git commit -m "make some work"
# finish release branch
git flow release finish '0.1.0'
# make tag
git checkout master
git tag v0.1.0 -m "v0.1.0"
# --------------- make a release -----------------
# create a hotfix branch
git flow hotfix start hotfix_branch
# make some work
git add <file>
git commit -m "make some work"
# finish hotfix branch
git flow hotfix finish hotfix_branch
```

## 参考文献

1. [Git Tutorals](https://www.atlassian.com/git/tutorials/what-is-version-control)
2. [GIT团队合作探讨之二--Pull Request](https://www.cnblogs.com/kidsitcn/p/5319282.html)
3. [Git 内部原理 - Git References](https://git-scm.com/book/zh/v1/Git-%E5%86%85%E9%83%A8%E5%8E%9F%E7%90%86-Git-References)
4. [Git快照(snapshot)到底该如何理解？或者说如何从文件系统的角度理解快照(snapshot)?](https://segmentfault.com/q/1010000008914409)
5. [为什么你的 Git 仓库变得如此臃肿](https://www.jianshu.com/p/7231b509c279)
6. [git revert: Why do I get conflicts?](https://stackoverflow.com/questions/46275070/git-revert-why-do-i-get-conflicts)
7. [3-way(git merge) V.S 2-way(diff-patch)](http://blog.chinaunix.net/uid-26816751-id-4114947.html)