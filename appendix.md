`ls` - List directory contents
> *Optional flags:*  
> &nbsp;&nbsp;Long listing (with details)... `ls -l`  
> &nbsp;&nbsp;List all files... `ls -a`


`cd` - Change directory
> *Special characters:*  
> &nbsp;&nbsp;Root of filesystem... `cd /`  
> &nbsp;&nbsp;Your home directory... `cd ~`  
> &nbsp;&nbsp;Go up a directory... `cd ..`  
> &nbsp;&nbsp;Return to last directory... `cd -`

> *Optional flags:*  
> &nbsp;&nbsp;Create intermediate directories as required. ... `mkdir -p`  


> *Optional flags:*  
> &nbsp;&nbsp;Remove recursively (directories)... `rm -r`  

> *Optional flags:*  
> &nbsp;&nbsp;Copy recursively (directories)... `rm -r`  

`nano` - Edit text files  
## Introduce Yourself

First, let's personalize Git by setting some configuration values...

    $ git config --global user.name "Your Name"
    $ git config --global user.email "your_email@whatever.com"

Now when we add new files (and folders) we can use Git to keep track of everything.

Let's clone a repository from Github to learn a little more about how Git works...
      Cloning into 'intro-to-git-starter-kit'...
      remote: Counting objects: 17, done.
      remote: Compressing objects: 100% (10/10), done.
      remote: Total 17 (delta 3), reused 17 (delta 3), pack-reused 0
      Unpacking objects: 100% (17/17), done.
      Checking connectivity... done.

Git just created a new directory called `intro-to-git-starter-kit` containing all the project files. Let's inspect...

    $ cd intro-to-git-starter-kit/
    $ ls -la
      total 24
      drwxr-xr-x   7 tcmacdonald  staff   238 Sep 24 23:00 .
      drwxr-xr-x  36 tcmacdonald  staff  1224 Sep 24 23:00 ..
      drwxr-xr-x  13 tcmacdonald  staff   442 Sep 24 23:00 .git
      -rw-r--r--   1 tcmacdonald  staff    10 Sep 24 23:00 .gitignore
      -rw-r--r--   1 tcmacdonald  staff   583 Sep 24 23:00 about.html
      drwxr-xr-x   3 tcmacdonald  staff   102 Sep 24 23:00 images
      -rw-r--r--   1 tcmacdonald  staff    13 Sep 24 23:00 index.html
The status tells you what changed since the last commit.
      Your branch is up-to-date with 'origin/master'.
      nothing to commit, working directory clean
Say you made some changes...
    $ git status
      On branch master
      Your branch is up-to-date with 'origin/master'.
      Changes not staged for commit:
        (use "git add <file>..." to update what will be committed)
        (use "git checkout -- <file>..." to discard changes in working directory)

        modified:   index.html

      no changes added to commit (use "git add" and/or "git commit -a")
You can change the format of the command's output by passing the `-s` flag...
    $ git status -s
      M index.html
## Uncommitted Changes
You can use `git diff` to see what changed ...

    $ git diff
      diff --git a/index.html b/index.html
      index cd08755..e4a5346 100644
      --- a/index.html
      +++ b/index.html
      @@ -1 +1,2 @@
      Hello world!
      +Is anybody out there?
      (END)
## Committing Changes
Commiting a revision is a 2-step process...
    $ git commit -m "Update index.html"
      [master 80c520c] Update index.html
      1 file changed, 1 insertion(+)

## The Stage

With the `git add` command, you are "staging" files in preparation for commit. This is a convention designed to help you *organize your commits*.

Imagine you've edited the copy in a couple files and added something new...

      Your branch is ahead of 'origin/master' by 1 commit.
        (use "git push" to publish your local commits)
      Changes not staged for commit:
        (use "git add <file>..." to update what will be committed)
        (use "git checkout -- <file>..." to discard changes in working directory)

        modified:   about.html
        modified:   index.html

      Untracked files:
        (use "git add <file>..." to include in what will be committed)

        news.html

Lets split these changes into a couple commits. First, lets add `news.html` to the stage...

    $ git add news.html
Now we can see that file is ready to be committed...
    $ git status
      On branch master
      Your branch is ahead of 'origin/master' by 1 commit.
        (use "git push" to publish your local commits)
        (use "git reset HEAD <file>..." to unstage)
        new file:   news.html
      Changes not staged for commit:
        (use "git add <file>..." to update what will be committed)
        (use "git checkout -- <file>..." to discard changes in working directory)
        modified:   about.html
        modified:   index.html
## Undoing a Commit
Made a mistake? You can undo your last commit with the `git reset` command, like so...
    $ git reset HEAD~1
      Unstaged changes after reset:
      M   about.html
      M   index.html
Git responds by telling you all the unstaged commits in the current directory. You can see that our last commit was indeed reverted by looking at status...
    $ git status -s
       M about.html
       M index.html
      ?? news.html
## Staging Everything
Sometimes you want to commit all the latest changes and staging individual files one by one can be a pain.
You can add everything to the stage by passing the `-A` flag...
    $ git add -A
      M  about.html
      M  index.html
      A  news.html
Let's say you changed your mind and want to unstage a particular file.
You can do this by passing a file to the `git reset` command...
      Your branch is up-to-date with 'origin/master'.
      Changes to be committed:
        (use "git reset HEAD <file>..." to unstage)

        modified:   about.html
        new file:   news.html

Want to unstage everything? Just call `git reset` with no arguments...

    $ git reset
    Unstaged changes after reset:
    M	about.html
    M	index.html

Check the status to ensure nothing is left on the stage...

    $ git status
      On branch master
      Your branch is up-to-date with 'origin/master'.
      Changes not staged for commit:
        (use "git add <file>..." to update what will be committed)
        (use "git checkout -- <file>..." to discard changes in working directory)

        modified:   about.html
        modified:   index.html

        news.html

      no changes added to commit (use "git add" and/or "git commit -a")
Now you can discard all your local changes with `git checkout`...
      Your branch is up-to-date with 'origin/master'.
      Changes not staged for commit:
        (use "git add <file>..." to update what will be committed)
        (use "git checkout -- <file>..." to discard changes in working directory)

        modified:   about.html

        news.html

      no changes added to commit (use "git add" and/or "git commit -a")
      Your branch is up-to-date with 'origin/master'.
        modified:   about.html
        new file:   news.html
    $ git commit -m "Add uncommitted files."
      [master 0b2b1f9] Add uncommitted files.
      2 files changed, 7 insertions(+), 1 deletion(-)
      create mode 100644 news.html
You can view all the commits with `git log`...


      commit 0b2b1f9a8fe2e836d300ac9e711429d01cbca0e7
      Date:   Sun Sep 27 21:58:59 2015 -0400
          Add uncommitted files.
      commit 5466ecf3271990817904e3f48dea166bf0af4605
      Date:   Tue Sep 22 08:57:59 2015 -0400
          Cleanup punctuation.
      commit 61e70075e6d77bf3e6513c07253dabb9d8c1239b
      Author: Taylor C. MacDonald <tcmacdonald@gmail.com>
      Date:   Mon Sep 21 23:19:33 2015 -0400
          Remove hidden .DS_Store files. :boom:
      commit a1f9b3e92585015c9ee6a4e2bc59205554438325
      Date:   Mon Sep 21 23:12:26 2015 -0400
          Add about page.
      commit 7b16c0cbad5caa44f62de31a51ec03cf6bb3ce44
      Author: Taylor C. MacDonald <tcmacdonald@gmail.com>
      Date:   Mon Sep 21 23:06:35 2015 -0400

          Initial commit.
      (END) 

Each commit has a unique, 40-digit identifier called a SHA.

You can view the details of an individual commit by passing the commit SHA to the `git show` command...

    $ git show 5466ecf3271990817904e3f48dea166bf0af4605
      commit 5466ecf3271990817904e3f48dea166bf0af4605
      Author: Taylor C. MacDonald <tcmacdonald@gmail.com>
      Date:   Tue Sep 22 08:57:59 2015 -0400

          Cleanup punctuation.

      diff --git a/about.html b/about.html
      index 2e5af6b..006caec 100644
      --- a/about.html
      +++ b/about.html
      @@ -1,5 +1,5 @@
      <h1>Sollicitudin Pharetra Nullam</h1>
      -<img src="images/gdi.png" alt="Girl, Develop It" />
      +<img src="images/gdi.png" alt="Girl Develop It" />
Conveniently, you can abbreviate the SHA value and get the same output...
    $ git show 5466ecf
So far, we've done everything locally but Git is a powerful remote collaboration tool by allowing us to "push" and "pull" updates to/from remote endpoints.
Since we cloned this repository from Github, we already have a remote endpoint that points to Github.
    $ git remote -v
      origin	https://github.com/tcmacdonald/intro-to-git-starter-kit.git (fetch)
      origin	https://github.com/tcmacdonald/intro-to-git-starter-kit.git (push)

Adding a remote server your repository is easy too. In the example below, you'd replace &lt;name&gt; with the name of your remote (eg. "origin") and &lt;server&gt; with the address of your remote.
    $ git remote add <name> <server>
Then "pushing" all your files and your commit history to a remote is as easy as executing the following (where "master" is your branch name)...

    $ git push origin master
      Counting objects: 4, done.
      Delta compression using up to 8 threads.
      Compressing objects: 100% (4/4), done.
      Writing objects: 100% (4/4), 430 bytes | 0 bytes/s, done.
      Total 4 (delta 2), reused 0 (delta 0)
      To git@github.com:tcmacdonald/intro-to-git-starter-kit.git
        5466ecf..0b2b1f9  master -> master

"Pulling" updates from your remote endpoint is also easy...
      From github.com:tcmacdonald/intro-to-git-starter-kit
      * branch            master     -> FETCH_HEAD
      Already up-to-date.
    $ git branch some-branch