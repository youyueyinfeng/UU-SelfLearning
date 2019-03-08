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









Git has an additional saving mechanism called 'the stash'. The stash is an ephemeral storage area for changes that are not ready to be committed. 



## 参考文献

1. 
2. [GIT团队合作探讨之二--Pull Request](https://www.cnblogs.com/kidsitcn/p/5319282.html)
3. [Git 内部原理 - Git References](https://git-scm.com/book/zh/v1/Git-%E5%86%85%E9%83%A8%E5%8E%9F%E7%90%86-Git-References)
4. 