# Use cases, examples and other useful things of git

## ProGit book notes:

#### There are three stages that the files can reside in:
1. Commited: the data is safely store in your local database
2. Modified: it means that you have chenged the file but have not commited it to the databasse yet
3. Staged: It means that you have marked  a modified file in its current version to go into your next commit snapshot

#### Three main sections of a Git project:
1. The .git directory: is where Git stores the metadata and object database for your project.
2. The working directory: is a checkout of one version of your project, the files are pulled out of the compressed database in the Gt directory and placed on disk for you to use or modifiy
3. The staging area: it is a file, generally contained in your Git directory, that
stores information about what will go into your next commit. It’s sometimes re-
ferred to as the “index”, but it’s also common to refer to it as the staging area.

#### The basic Git workflow goes something like this:
1. You modify files in your working directory.
2. You stage the files, adding snapshots of them to your staging area.
3. You do a commit, which takes the files as they are in the staging area and
stores that snapshot permanently to your Git directory.

If a particular version of a file is in the Git directory, it’s considered commit-
ted. If it has been modified and was added to the staging area, it is staged. And
if it was changed since it was checked out but has not been staged, it is modi-
fied.In Chapter 2, you’ll learn more about these states and how you can either
take advantage of them or skip the staged part entirely.

Each file in your working directory can be in one of two
states: tracked or untracked. 

Tracked files are files that were in the last snap-shot;
they can be unmodified, modified, or staged. Untracked files are every-
thing else – any files in your working directory that were not in your last snap-
shot and are not in your staging area. When you first clone a repository, all of
your files will be tracked and unmodified because Git just checked them out
and you haven’t edited anything.

#### .gitignore file

Here is another example .gitignore file:
```
# no .a files
*.a
# but do track lib.a, even though you're ignoring .a files above
!lib.a
# only ignore the TODO file in the current directory, not subdir/TODO
/TODO
# ignore all files in the build/ directory
build/
# ignore doc/notes.txt, but not doc/server/arch.txt
doc/*.txt
# ignore all .pdf files in the doc/ directory
doc/**/*.pdf
```
- GitHub maintains a fairly comprehensive list of good .gitignore file ex-
amples for dozens of projects and languages at https://github.com/github/
gitignore if you want a starting point for your project.

- Viewing Your Staged and Unstaged Changes

`git status
`
- To see what you’ve changed but not yet staged:

` git diff
`
- If you want to see what you’ve staged that will go into your next commit

`git diff --staged
`
- To remove a file from Git you have to remove it from your tracked files (more
accurately, remove it from your staging area) and then commit.

`git rm file`

and also removes the file from your working directory so
you don’t see it as an untracked file the next time around.

- Another useful thing you may want to do is to keep the file in your working
tree but remove it from your staging area. In other words, you may want to
keep the file on your hard drive but not have Git track it anymore. This is partic-
ularly useful if you forgot to add something to your .gitignore file and acci-
dentally staged it, like a large log file or a bunch of .a compiled files. To do this,
use the --cached option:

`git rm --cached file`

- You can pass files, directories, and file-glob patterns to the git rm com-
mand. That means you can do things such as:

`git rm log/\*.log`  

- If you want to rename a
file in Git, you can run something like:

`git mv file_from file_to`

and then do a commit. 

- To see the commit history
 
` git log`

git log --help

- The --stat option prints below each commit entry a list of
modified files, how many files were changed, and how many lines in those files
were added and removed. It also puts a summary of the information at the end. It is the more useful for me.

 `git log --stat`
 
 - Another really useful option is --pretty
 
 `git log --pretty=oneline --> print in one line every commit`  
 
 - To print in a custom format
 `git log --pretty=format:"%h - %an, %ar : %s"`
 
 - To se the difference in each commit
 
 `git log -p`
 
 - To see the commits in a especific time there are --since and --until
 
 ` git log --since=2.hours` 
 
 - To see logs in a pretty format 
 
 `git log --oneline --abbrev-commit --all --graph --decorate --color`
 
 -The above line could have an alias:
 
 `alias gg='git log --oneline --abbrev-commit --all --graph --decorate --color `
 
 #### Undoing Things
 
 - If you want
to try that commit again, you can run commit with the --amend option:

 `git commit --amend`
 
 
 - As an example, if you commit and then realize you forgot to stage the
changes in a file you wanted to add to this commit, you can do something like
this:

``` 
git commit -m 'initial commit'
git add forgotten_file
git commit --amend
```
You end up with a single commit – the second commit replaces the results of
the first

If you only want to modify your last commit message, it’s very simple:

 `git commit --amend`
 
That drops you into your text editor, which has your last commit message in
it, ready for you to modify the message.

It's useful for example if you staged and commited the wrong file:

```
git commit -m 'initial commit'
git rm file
git commit --amend

```

To remove entirely the last commit:

`git reset HEAD^`

#### Unstaging a Staged File

- To undo a file that you staged for error:

`git reset HEAD file`
 
#### Unmodifying a Modified File

- To discard changes in a working directory.It means that if you do not want to keep changes in a file in working directory. 

`git checkout -- file`

#### Remotes

- To see which remote servers you have configured, you can run

`git remote`
 
 command.
 
 - Origin is the dedault name Git gives to the server you  cloned from, so when you run the above command, the most probably output would be `origin`
 
 - And with the -v flag, git shows you the URLs that Git has stored for the shortname to be used when reading and writing to that remote:
 
`git remote -v`

#### Adding remote repositories

- We know how to clone a remote repo:
  
  ` git clone <url>`

-But a more fancy way to do it. To add a new remote Git repository as a shortname you can reference easily:

`run git add <shortname> <url>`


#### Fetching and Pulling from Your Remotes

- To get the data that has been pushed to that sever since you cloned (or last fetched) of this repo:

`git fetch <shortname> `

That command only downloads data to local repository -

- To do a pull of this repo:
   
 ` git pull <shortname> <branch> `
 
 automaticaly fetch an d then merge a remote branch into your current branch. 

### Tags

-There are two main types of tags: lightweight and annotated. The first is like a branch that points to a specific commit and annotated are full objects in the Git database (contain the tagger name, email, and date; have a tagging message).

- To create a tag: 

`git tag -a <tagName> -m "my version<tagName>"` --> This creates a tag in the last commit you made. 

- To list tags: 

`git tag`

- You can see the tag data along with the commit that was tagged by using the git show command:

`git show <tagName>`

- To create a tag in a specific commit:

`git tag -a <tagName> commit_hash `

- When you create a tag with a version in a specifi commit, just the commits until that tag are part of the version. 

-If you want to put a version of your repository in your working directory that looks
like a specific tag, you can create a new branch at a specific tag with git
checkout -b [branchname] [tagname] :

`git checkout -b version2 v2.0.0` --> This command create the branch version2 and switch you to it. 
 
   - Then You can verify it:

` git log --oneline`

- To delete a tag:

`git tag -d tagName`

- To push tags to remote repositories after you have created them, for example:

`git push origin tagName` --This is the only way a colaborator could fetch the tag into his local repo.  

### Merge examples

## Technical Notes from [a visual git reference](http://marklodato.github.io/visual-git-guide/index-en.html):

The contents of files are not actually stored in the index (.git/index) or in commit objects. Rather, each file is stored in the object database (.git/objects) as a blob, identified by its SHA-1 hash. The index file lists the filenames along with the identifier of the associated blob, as well as some other data. For commits, there is an additional data type, a tree, also identified by its hash. Trees correspond to directories in the working directory, and contain a list of trees and blobs corresponding to each filename within that directory. Each commit stores the identifier of its top-level tree, which in turn contains all of the blobs and other trees associated with that commit.
 
#### Walkthrough: Watching the effect of commands

Start by creating some repository:
```
$ git init foo
$ cd foo
$ echo 1 > myfile
$ git add myfile
$ git commit -m "version 1"
```
Now, define the following functions to help us show information in a file show_status.sh:
```
show_status() {
  echo "HEAD:     $(git cat-file -p HEAD:myfile)"
  echo "Stage:    $(git cat-file -p :myfile)"
  echo "Worktree: $(cat myfile)"
}

initial_setup() {
  echo 3 > myfile
  git add myfile
  echo 4 > myfile
  show_status
}
```
Initially, everything is at version 1.
```
$ show_status
HEAD:     1
Stage:    1
Worktree: 1
```

We can watch the state change as we add and commit.
```
$ echo 2 > myfile
$ show_status
HEAD:     1
Stage:    1
Worktree: 2
$ git add myfile
$ show_status
HEAD:     1
Stage:    2
Worktree: 2
$ git commit -m "version 2"
[master 4156116] version 2
 1 file changed, 1 insertion(+), 1 deletion(-)
$ show_status
HEAD:     2
Stage:    2
Worktree: 2
```

Now, let's create an initial state where the three are all different.
```
$ initial_setup
HEAD:     2
Stage:    3
Worktree: 4
```
Let's watch what each command does. You will see that they match the diagrams above.

git reset -- myfile copies from HEAD to stage:

```
$ initial_setup
HEAD:     2
Stage:    3
Worktree: 4
$ git reset -- myfile
Unstaged changes after reset:
M   myfile
$ show_status
HEAD:     2
Stage:    2
Worktree: 4
```
git checkout -- myfile copies from stage to worktree:
```
$ initial_setup
HEAD:     2
Stage:    3
Worktree: 4
$ git checkout -- myfile
$ show_status
HEAD:     2
Stage:    3
Worktree: 3
```


git checkout HEAD -- myfile copies from HEAD to both stage and worktree:
```
$ initial_setup
HEAD:     2
Stage:    3
Worktree: 4
$ git checkout HEAD -- myfile
$ show_status
HEAD:     2
Stage:    2
Worktree: 2
```
git commit myfile copies from worktree to both stage and HEAD:
```
$ initial_setup
HEAD:     2
Stage:    3
Worktree: 4
$ git commit myfile -m "version 4"
[master 679ff51] version 4
 1 file changed, 1 insertion(+), 1 deletion(-)
$ show_status
HEAD:     4
Stage:    4
Worktree: 4

```
To resume, the important part is:

`git reset -- myfile` COPIES from HEAD to stage:

`git checkout -- myfile` COPIES from stage to worktree:

`git checkout HEAD -- myfile` COPIES from HEAD to both stage and worktree:

`git commit myfile` COPIES from worktree to both stage and HEAD: 



## Tutorial to do a PR

https://github.com/karwinski/QA/blob/Confluence/PR.md



## Don’t type your password every time


Don’t type your password every time


If you don’t want to type it every single time you push, you can set up a “credential cache”. The simplest is just to keep it in memory for a few minutes, which you can easily set up by running:

`git config --global credential.helper cache` 


## How to work with multiple accounts

 This is important if you have one GitHub personal account and other for your company, for instance.

- Generate a unique SSH key for your company GitHub account:

`ssh-keygen -t rsa -C "your-company-github-account-email-address`


- Do not over-write your existing keys for your personal account. 
when prompted, save the file generated as :

id_rsa_company, for example `~/.ssh/id_rsa_datio`

- Attach the new key
login to your second GitHub account, browse to "Account Overview," and attach the new key, within the "SSH Public Keys" section. To retrieve the value of the key that you just created, return to the Terminal, and type: `vim ~/.ssh/id_rsa_COMPANY.pub` Copy the entire string that is displayed, and paste this into the GitHub text area.

Next, because we saved our key with a unique name, we need to tell SSH about it. Within the Terminal, type: `ssh-add ~/.ssh/id_rsa_COMPANY` If successful, you'll see a response of "Identity Added."

- Create a config file

Now we need a way to specify when we wish to push to our personal account, 
and when we should instead push to our company account. To do so, let's create a `config` file.

```
touch ~/.ssh/config
vim config
```

Paste the following: 

```
#Default GitHub
Host github.com
  HostName github.com
  User git
  IdentityFile ~/.ssh/id_rsa

```

This is the default setup for pushing to our personal GitHub account. Notice that we're able to attach an identity file to the host. Let's add another one for the company account. Directly below the code above, add:

```
Host github-COMPANY
  HostName github.com
  User git
  IdentityFile ~/.ssh/id_rsa_COMPANY
```
Save the page and exit!


- Try it out

Create a test directory, initialize git, and create your first commit.

```
git init
echo "hello " > hello 
git add hello
git commit -m "first commit"
```
- Login to your company account, create a new repository, give it a name of "Test"
 and then return to the Terminal and push your git repo to GitHub.

`git remote add origin git@github-COMPANY:Company/testing.git` # Here we named origin to the github repo we created before. 

Now, we need to push the first commit to origin, in the master branch for example. 

`git push origin master`


Note that, this time, rather than pushing to git@github.com, we're using the custom host that we create in the
config file: `git@github-COMPANY`


- Return to GitHub, and you should now see your repository.
Remember:

When pushing to your personal account, proceed as you always have.
For your company account, make sure that you use `git@github-COMPANY` as the host.


- If you want to push commits using the user of your company github account you need to set up your name and e-mail address:

Located in the git directory after you initialized git and type:
For more info about [git configuration](https://git-scm.com/book/tr/v2/Customizing-Git-Git-Configuration)

```
git config --local user.name <name> # User name you use in your company github account
git config --local user.email <email> # Email you registered in your company github account
```

Note that the `--local` flag is because we want the scope of this user available only to this directory

To confirm your changes have been done:

`git config --local --list`

You should see the name and email address you wrote before and probably other info.  

And If your personal github account is global, you should type:

`git config --global --list`

And see the name and email address of your personal github account. 



References:

[Link to think like a git](http://think-like-a-git.net)

[Link to a visual git reference](http://marklodato.github.io/visual-git-guide/index-en.html)

[Link to tutorial of how to work with multiple accounts](https://code.tutsplus.com/tutorials/quick-tip-how-to-work-with-github-and-multiple-accounts--net-22574)

[Link to youtube Git For Ages 4 And Up tutorial](https://www.youtube.com/watch?v=1ffBJ4sVUb4)


