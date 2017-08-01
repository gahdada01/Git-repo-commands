Git Repository Commands

Pull git

first pull :
$ git clone http://sample

second pull:
go to project folder.
$ cd foldername
$ git init
	- to initialise git

#### project version.
```ruby
$ git add .
$ git status
 - git status to compare your  updated version to the master 
$ git commit -m “message”
$ git remote add origin https://github.com/gahdada01/meanauth_local.git
$ git push -u origin master
```

…or push an existing repository from the command line

$ git remote add origin https://github.com/gahdada01/meanauth_deploy.git
$ git push -u origin master


To add remote repositories
$ git remote set-url origin git://new.url.here
or
$ git remote set-url --add --push origin https://sampleRemote.git

git remote -v
### View current remotes
origin  https://github.com/OWNER/REPOSITORY.git (fetch)
origin  https://github.com/OWNER/REPOSITORY.git (push)
destination  https://github.com/FORKER/REPOSITORY.git (fetch)
destination  https://github.com/FORKER/REPOSITORY.git (push)

git remote rm destination
### Remove remote
git remote -v
### Verify it's gone
origin  https://github.com/OWNER/REPOSITORY.git (fetch)
origin  https://github.com/OWNER/REPOSITORY.git (push)



To reset git
$ git reset

To pull
$ git pull origin master or $ git pull

To stash local folder
$ git stash —keep-index

To drop stash
$ git stash drop 

To get repository name
$ git config --get remote.origin.url

To merge
$ git stash apply

To get git origin
git remote -v


Git Branch

First, you create your branch locally:
$ git checkout -b <branch-name>

The remote branch is automatically created when you push it to the remote server. So when you feel ready for it, you can just do:
$ git push <remote-name> <branch-name>

Where <remote-name> is typically origin, the name which git gives to the remote you cloned from. Your colleagues would then just pull that branch, and it's automatically created locally.
Note however that formally, the format is:
$ git push <remote-name> <local-branch-name>:<remote-branch-name>

But when you omit one, it assumes both branch names are the same. Having said this, as a word of caution, do not make the critical mistake of specifying only :<remote-branch-name> (with the colon), or the remote branch will be deleted!
So that a subsequent git pull will know what to do, you might instead want to use:
$ git push -u <remote-name> <local-branch-name>

As described below, the -u option sets up an upstream branch:
For every branch that is up to date or successfully pushed, add upstream (tracking) reference, used by argument-less $ git-pull(1) and other commands.


To merge branch

git checkout testBranch
git pull origin testBranch
git checkout master
git pull
git merge --no-ff --no-commit test

Test merge before commit, avoid a fast-forward commit by --no-ff,
If conflict is encountered, we can run git status to check details about the conflicts and try to solve

git status

Once we solve the conflicts, or if there is no conflict, we commit and push them

git commit -m 'merge test branch'
git push

But this way will lose the changes history logged in test branch, and it would make master branch to be hard for other developers to understand the history of the project.
So the best method is we have to use rebase instead of merge (suppose, when in this time, we have solved the branch conflicts).
Following is one simple sample, for advanced operations, please refer to http://git-scm.com/book/en/v2/Git-Branching-Rebasing

git checkout master
git pull
git checkout test
git pull
git rebase -i master
git checkout master
git merge test

Yep, when you have uppers done, all the Test branch's commits will be moved onto the head of Master branch. The major benefit of rebasing is that you get a linear and much cleaner project history.
The only thing you need to avoid is: never use rebase on public branch, like master branch.
like following operation:

git checkout master
git rebase -i test

never do these operations.
Details for https://www.atlassian.com/git/tutorials/merging-vs-rebasing/the-golden-rule-of-rebasing
appendix:
* if you are not sure about rebasing operations, please refer to: https://git-scm.com/book/en/v2/Git-Branching-Rebasing


