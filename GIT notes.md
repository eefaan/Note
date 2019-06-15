##GIT notes

### 1. Install 

####Installing git on linux

- apt-get安装：`sudo apt-get install git`

- 源码安装：```./config```，```make```，`sudo make install`

#### Installing git on osx

- [homebrew](http://brew.sh/)安装
- Xcode内集成：菜单“Xcode”->“Preferences”->“Downloads”->“Command Line Tools”，“Install”

### 2. Repository/版本库/仓库

####Creating an empty repository

```shell
$ mkdir learngit
$ cd learngit
$ git init
```

​	the directory '.git' is used for tracking/managing the repository. (Using command `ls -ah` to see it)

#### Adding file to the repository

​	Creating a file named 'readme.txt':

```
Git is a version control system.
Git is free software
```

​	Using the command `git add`:

```shell
$ git add readme.txt
```

​	Using the command `git commit`:

```shell
$ git commit -m "wrote a readme file"
```

​	The output in terminal will look like:

```shell
➜  gitlearn git:(master) ✗ git add file1.txt
➜  gitlearn git:(master) ✗ git commit -m "no changing"
[master 57b2a60] no changing
 1 file changed, 2 insertions(+)
 create mode 100644 file1.txt
```

###3. Going back!

#### Reset the repository

​	Using the command `git status` to see the status of the repository.

​	Using the command `git diff filename` to see the difference about the file.

​	Using the command `git log` to see all the distributions about the repository. (Or have a try with `git log --pretty=oneline`)

​	Going back with `git reset --hard HEAD^`. (`Head^` meant the last commit. `Head^^` meant the commit before the last one.)

​	Undoing the  GoBack step? `git reset --hart id_of_the_commit`. (Make sure that the terminal has not been closed. Or command `git reflog` will be needed to see the history of your command.)

#### The Working Directory and the Repository 

​	**Working Directory:** the visable directory in your computer. 

​	**Repository:** contain stage(or named index), the first branch named 'master', and the pointer to the branch named 'HEAD'.

​	![image-20190122193033941](/Users/yifanliu/Library/Application Support/typora-user-images/image-20190122193033941.png)

​	`git add` will only add the modification of files.

​	`git checkout -- file` will reset the file to the status when you type `git add` or `git commit` last time.

​	`git reset HEAD file` will undo `git add`.

#### Remove file

```shell
$ rm file1.txt
$ git rm file1.txt
# when you need to remove the file in repository
$ git commit -m "remove file1.txt"
# or you need to undo the rm in your terminal
$ git checkout -- file1.txt
```

### 4. Remoting repository: GitHub

####SSH Key

1. If there are no `id_rsa` and `id_rsa.pub` in the directory `YourUserDic/.ssh`, typing: 

```shell
$ ssh-keygen -t rsa -C "youremail@example.com"
```

2. Logining in GitHub->"Account setting"->"SSH Keys", adding the content in file `id_rsa.pub` to the web.

#### Creating a new repo in GitHub

​	Logining in GitHub->"Create a new repo" named "gitlearn"->"Create repository".

​	Using command as follow to link your local repo to the remote one:

```shell
$ git remote add origin git@github.com:YourGitHubUsername/gitlearn.git
```

​	# origin is the name of the remote repo.

​	Using command `git push` to push your local repo:

```shell
$ git push -u origin master
```

​	# -u means link the local master with the remote one, which is only needed in your first push. Besides when you first use `git push` with ssh, you will get a warning to check if the rsa key is from the server of GitHub.

​	Some other command about pushing:

```shell
$ git push origin master
$ git push origin :master
$ git push origin
$ git push
```

#### Cloning from the remote repo

​	Using command `git clone` to clone repo from GitHub:

```shell
$ git clone git@github.com:eefaan/gitlearn.git
```

​	And the output in terminal will look like:

```shell
Cloning into 'gitlearn'...
remote: Enumerating objects: 9, done.
remote: Counting objects: 100% (9/9), done.
remote: Compressing objects: 100% (5/5), done.
remote: Total 9 (delta 0), reused 9 (delta 0), pack-reused 0
Receiving objects: 100% (9/9), done.
```

​	Besides, you can also use `https` protocol to push/clone. (But slower.)

### 5. Branches

#### Fast-forward

​	Creating a new branch named dev and switch to it:

```shell
$ git checkout -b dev
```

​	which is same as:

```shell
$ git branch dev
$ git checkout dev
```

​	To check the working branch:

```shell
$ git branch
```

​	To merge master branch with dev, and then remove the dev branch:

```shell
$ git checkout master
$ git merge dev
$ git branch -d dev
```

#### Merge conflict

​	If a file is modified by more than two branches, when you merge them you will see:

```shell
➜  gitlearn git:(master) git merge dev
Auto-merging file1.txt
CONFLICT (content): Merge conflict in file1.txt
Automatic merge failed; fix conflicts and then commit the result.
```

​	Git uses `<<<<<<<`,`=======` and `>>>>>>>` to mark the conflict text from different branches

​	Solving the conflict by yourself, then using `git add` and `git commit`, merging done!

​	Using command `git log --graph` will display the merging graph.

#### Banning the Fast-forward(ff) mode

​	The fast-forward mode looks like you finish your job always in the master branch but safer. (which will lose the information of merged branch)

​	To use `no-ff` mode will create a new commit and save "dev"s information:

```shell
$ git merge --no-ff -m "merge with no-ff" dev
```

​	Since we make a new commit, `-m` is nesserary to make a summary for the commit.

#### Strategy of managing branches

​	The `master` branch is usual a stable branch, which is used for publish the new edition.

​	The `dev` branch is usual what we edit with.

​	The branches usually look like:

![image-20190129150306468](/Users/yifanliu/Library/Application Support/typora-user-images/image-20190129150306468.png)

#### The branch used for bugging (Bug branch)

​	The wokring branch will be clean after saving the working directory:

```shell
$ git stash
```

​	then creating a new branch for debugging:

```shell
$ git checkout master
$ git checkout -b issue-101
...
$ git add .
$ git commit -m "fix bug 101"
```

​	The bug has been fixed! Using command (`git stash apply` + `git stash drop`) or `git stash pop` to go back to our working directory:

```shell
$ git checkout dev
# To check the stash
$ git stash list
$ git stash pop
```

####The branch used for adding new func (Feature branch)

​	A branch named `feature-vulcan` will be used for adding new func to our project:

```shell
$ git checkout -b feature-vulcan
```

​	However, before you merge it to the dev branch, you need to remove the new func:

```shell
# will now work cause the branch 'feature' is not fully merged
$ git branch -d feature-vulcan
# insted of '-d', using '-D'
$ git branch -D feature-vulcan
```

#### Working together!

​	When you clone a repo from GitHub, Git will connect the local branch 'master' to the remote one, and we name the remote repo 'origin' default. To check the information about your remote repo:

```shell
$ git remote
# Or '-v' will display the details
$ git remote -v
```

​	Pushing your branch:

```shell
# The branch 'master' should be same as your local one all the time.
$ git push origin master
# The branch 'dev' needs to be sync updated.
$ git push origin dev
# The branch 'bug' should be used locally.
# The branch 'feature' needs to be syne updated if it has muti developers.
```

​	Pulling remote branch:

​	Assuming that one of your friend did those:

```shell
# clone your project from github
$ git clone git@github.com:xxx/gitlearn.git
# the only branch he could see is master
$ git branch
* master
# he have to create a branch 'dev' to develop himself
$ git checkout -b dev origin/dev
# he will commit sth and push them to branch 'dev'
$ git commit -m "add sth"
$ git push origin dev
```

​	Now fortunately you also have some changes on the branch 'dev', when you try to commit them, and Git will give you hint such as `Updates were rejected, merge the remote changes before pushing again`. So what you should do is:

```shell
# Using 'git pull' to get the newest commit from the remote repo
$ git pull
# Pulling failed since the local branch 'dev' has not been linked to the remote one
# Using 'git branch' to link them
$ git branch --set-upstream dev origin/dev
# Then pulling again
$ git pull
# merge those conflicts by yourself, then try to commit & push
$ git commit -m "merge & fix new file"
$ git push origin dev
```

###6. Tag management

​	Tag is actually a pointer point to a commit. (Tag is static, compared to the branch)

#### Creating a tag

```shell
# Move to the branch needed tags
$ git branch
* dev
  master
$ git checkout master
# To make a new tag
$ git tag v1.0
# To check your tag
$ git tag
```

 	Defaultly, the tag will be attached to the newest commit. If you need to attach a tag to older commit, try:

```shell
$ git log --pretty=oneline --abbrev-commit
...
$ git tag v0.9 6224937
```

​	`git tag` could display all the tags alphabetically, `git show` could display the detail you set with `$ git tag -a v0.1 -m "version 0.1 released" 3628164`. (`-a` could set the name of tag, `-m` could set the detail of commit)

​	Besides, you could sign a tag with parameter `-s`, such as: `$ git tag -s v0.2 -m "signed version 0.2 released" fec145a`

#### Deleting a tag

```shell
$ git tag -d v0.1
```

​	Pusing and deleting a tag to the remote repo:

```shell
$ git push origin v1.0
# Or you need to push all the tags
$ git push prigin --tags
# Deleting a tag in the remote repo, first deleting locally
$ git tag -d v0.9
# Then deleting remote
$ git push origin :refs/tags/v0.9
```

### Using GitHub

​	Fork a project firstly from others' account, then clone it to local repo from your account.

![image-20190131140435190](/Users/yifanliu/Library/Application Support/typora-user-images/image-20190131140435190.png)

### Making your Git

​	Making your git colorful:

```shell
$ git config --global color.ui true
```

​	Ignoring some special files with file `.gitignore`.

​	Naming your command `git status` as `git st`:

```shell
$ git config --global alias.st status
```

