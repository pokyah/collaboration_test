# collaboration_test
Repository to test collaborative git workflows

## 3 good git references online 

* https://www.miximum.fr/blog/enfin-comprendre-git/
* http://marklodato.github.io/visual-git-guide/index-en.html
* http://r-bio.github.io/intro-git-rstudio/


## what we have done so far 

1. pasting each member public SSH key in repository setting so that everyone can collaborate on the upstream repository without the need to ask for pull requests.
2. each collaborator `git clone` the online github repository on his own computer :

```bash
git@github.com:pokyah/collaboration_test.git
```

3. Frdvwn has made edits to the README.md in the master branch & commited and pushed to the github remote origin.
4. On purpose, Pokyah has made edits to the README.md without pulling. 

```bash
$ git status
On branch master
Your branch is up-to-date with 'origin/master'.
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

	modified:   README.md

no changes added to commit (use "git add" and/or "git commit -a")
```

So git status says that I'm up-to-date even if Frdvwn has made edits and pushed to the online repo. Strange ! Doing a git diff between my local master and the remote master does not provide anything neither : 

```bash
$ git diff master origin/master
```

How can this be possible ? Let's ask on [Stackoverflow](https://stackoverflow.com/questions/1800783/compare-local-git-branch-with-remote-branch)
The explanation is that you need to make your local git tree aware of the remote changes using the `git fetch` command : 

```bash
$ git fetch
$ git status
On branch master
Your branch is behind 'origin/master' by 1 commit, and can be fast-forwarded.
  (use "git pull" to update your local branch)
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

	modified:   README.md
$ git diff master origin/master
diff --git a/README.md b/README.md
index fd9533a..2816a7e 100644
--- a/README.md
+++ b/README.md
@@ -10,7 +10,8 @@ Repository to test collaborative git workflows
 
 ## what we have done so far 
 
-1. pasting each member public SSH key in repository setting so that everyone can collaborate on the upstream repository without the need to ask for pull requests.
+1. Adding all the team members as repository's collaborators (through Github interface via github username)
+
 2. each collaborator `git clone` the online github repository on his iwn computer :
```

So what will doing a `git pull` before commiting my local work lead to ? Let's try : 

```bash
$ git pull
Updating 7776b27..36f3d54
error: Your local changes to the following files would be overwritten by merge:
	README.md
Please, commit your changes or stash them before you can merge.
Aborting
```

Git is not happy. 




