note: each of the heading (blue) are links to associated sections in the video


# [Git and GitHub for Beginners - Crash Course - YouTube](https://www.youtube.com/watch?v=RGOj5yH7evk)
Branching and merging starts [here](https://youtu.be/RGOj5yH7evk?t=1956).

* long video, but does a great job .. worth the extra time
* skip first half if you know git basics already
* uses git integrated with VS Code, so you'll need to adapt to your IDE/system
* the VS Code setup shows current local branch in the CLI .. probably uses something like [https://github.com/git/git/tree/master/contrib/completion], described [https://gist.github.com/ivanoats/1823034](here)
* uses "master" rather than "main" branch
* uses 

## [GitHub Workflow](https://www.youtube.com/watch?v=RGOj5yH7evk&t=1821s)
30:21
* summarizes video up to this point
* doing "simple" commits using GitHub UI
```
edit / add files via GitHub website interface
      |
      v
commit changes
      |
      v
make pull request
(if code review required)
```


## [Local git Workflow](https://youtu.be/RGOj5yH7evk?t=1900)
31:40

```
 edit/write/add code 
        |
        v
 git add: stage changes
        |
        v
 git commit: commit changes
        |
        v
 git push: push changes
        |
        v
 make a pull request
(if code review required)
```

## [Git Branching](https://youtu.be/RGOj5yH7evk?t=1963)
32:43

* "master" is "main"
* if there is only one branch, everything is in "main"
* make a new branch .. called "feature" .. at first, both master and feature will be the same
* if you change feature then switch back to master, you won't see any of the changes on feature
* branches only track their own changes
* branches can't see/know changes in other branches
* why branch? so you can work on code without affecting master

## [Merging a Branch](https://youtu.be/RGOj5yH7evk?t=2162)
36:02

Go into the repo's dirctory
```bash
ck@lemuree:zz-repo$ cd demo-repo
```

Switch into git/bash CLI (or another flavor)

list branches
```bash
ck@lemuree zz-repo (main)]$ git branch
```

Create a new branch
```bash
ck@lemuree zz-repo (main)]$ git checkout -b feature-readme-instructions
```

Add lines to README.md with your preferred editor
```bash
ck@lemuree zz-repo (feature-readme-instructions)]$ vim README.md
```

Check for changes to branch .. should show that README.md was modified
```bash
ck@lemuree zz-repo (feature-readme-instructions)]$ git status
```

Stage the file changes "add", then commit the change
```bash
ck@lemuree zz-repo (feature-readme-instructions)]$ git add README.md

ck@lemuree zz-repo (feature-readme-instructions)]$ git commit -m "updated readme"
```

Go back to main branch and look at README.md .. it won't show changes made in feature-readme-instructions branch
```bash
ck@lemuree zz-repo (feature-readme-instructions)]$ git checkout main

ck@lemuree zz-repo (main)]$ cat README.md
```

**PULL** the repo's main branch so you have the most up to date version
```bash
 ck@lemuree zz-repo (main)]$ git pull origin main
```

While still in the main branch, examine differences in code between branches.
Text that hasn't been changed will be white.
Lines starting with "-' and red text are not yet in the current (main) branch

```bash
 ck@lemuree zz-repo (main)]$ git diff feature-readme-instructions 

diff --git a/README.md b/README.md
index d13e4db..1f8597d 100644
--- a/README.md
+++ b/README.md
@@ -3,8 +3,3 @@
 repo for testing branches, pull, push, merge
 
 adding these lines for pull
-
-
-## Local Development
-
-1. Open index.html in your browser

```

At this point you could merge, but this would only merge locally ...

**DON'T DO THIS !!!!!!!!!!!!!!!**
```bash
 ck@lemuree zz-repo (main)]$ git merge feature-readme-instructions 
```

**DO DO THIS**
It's better to **push** the changes on the branch back to GitHub and then make a pull request and check status just be be sure.

```bash
 ck@lemuree zz-repo (main)]$ git checkout feature-readme-instructions

 ck@lemuree zz-repo (feature-readme-instructions)]$ git status

 ck@lemuree zz-repo (feature-readme-instructions)]$ git push

fatal: The current branch feature-readme-instructions has no upstream branch.
To push the current branch and set the remote as upstream, use

    git push --set-upstream origin feature-readme-instructions

 ck@lemuree zz-repo (feature-readme-instructions)]$ 
```
note:
```-u``` is short for ```--set-upstream```  

```bash
 ck@lemuree zz-repo (feature-readme-instructions)]$ git push -u origin feature-readme-instructions
Enumerating objects: 5, done.
Counting objects: 100% (5/5), done.
Delta compression using up to 8 threads
Compressing objects: 100% (3/3), done.
Writing objects: 100% (3/3), 404 bytes | 404.00 KiB/s, done.

Total 3 (delta 0), reused 0 (delta 0)
remote: 
remote: Create a pull request for 'feature-readme-instructions' on GitHub by visiting:
remote:      https://github.com/EspressoPlus/zz-repo/pull/new/feature-readme-instructions
remote: 
To github.com:EspressoPlus/zz-repo.git
 * [new branch]      feature-readme-instructions -> feature-readme-instructions
Branch 'feature-readme-instructions' set up to track remote branch 'feature-readme-instructions' from 'origin'.
```

## [What is a Pull Request (PR)](https://youtu.be/RGOj5yH7evk?t=2604)
43:24

It's a request to have your code pulled into another branch.

In the example above, the request is for the branch *feature-readme-instructions* to be pulled into branch *main* .. this is making a PR from the feature branch to the main branch.

Once there is a PR, anyone with access to the repo on GitHub can review/comment/ask for changes to the code in the branch that made the PR.

After you make a PR you can update the code by making additional commits and pushing them up to GitHub, as long as the commits are on the same branch where the PR is happening.

Once the PR is merged, it's standard practice to delete the feature branch and switch back to the main branch. When you want to make additional changes you follow the same order of operations: **create a new feature branch, commit, PR, merge to main**.

## [Handle PR via GitHub interface](https://youtu.be/RGOj5yH7evk?t=2675)
44:35
You can copy the URL from the command-line output above, or you can just go to the GitHub repo and you'll see a notification about the recent PR (green button: 'Compare & pull request')

Give the PR a title and provide bullets to describe the changes, the click the green 'Create pull request' button.

GitHub will let you know if there are/aren't conflicts. Before you click the green 'Merge pull request' button, you can add more comments (Conversation tab), or use the Commits or Files changed tabs. Under the 'Files changed' you can add comments for specific lines directly ('Add a single comment' button) in the code.

Once all the comments and conversations are "complete", clicking the 'Merge pull request' button will merge the working branch into the main branch.

After the PR is merged you can check the main branch to see that the repo was updated properly.

## [Back on local computer CLI](https://youtu.be/RGOj5yH7evk?t=2865)
47:45

Go back to your local computer CLI to clean up. Do a **pull** to get the latest repo ... 

```bash
 ck@lemuree zz-repo (feature-readme-instructions)]$ git checkout main 
Switched to branch 'main'
Your branch is up to date with 'origin/main'.

 ck@lemuree zz-repo (main)]$ git pull 
remote: Enumerating objects: 1, done.
remote: Counting objects: 100% (1/1), done.
remote: Total 1 (delta 0), reused 0 (delta 0), pack-reused 0
Unpacking objects: 100% (1/1), 643 bytes | 643.00 KiB/s, done.
From github.com:EspressoPlus/zz-repo
   74697f6..48a1ae0  main       -> origin/main
Updating 74697f6..48a1ae0
Fast-forward
 README.md | 5 +++++
 1 file changed, 5 insertions(+)
 ck@lemuree zz-repo (main)]$ git branch
  feature-readme-instructions
* main
```

Delete the local branch because, with this approach, you don't re-use branches .. you just make a new one. So, delete the branch ...

```bash
 ck@lemuree zz-repo (main)]$ git branch -d feature-readme-instructions 

Deleted branch feature-readme-instructions (was 9e1369f).

 ck@lemuree zz-repo (main)]$ git branch
* main

 ck@lemuree zz-repo (main)]$ 
```
Now, only the **main** branch remains.


## [What about conflicts?](https://youtu.be/RGOj5yH7evk?t=2946)
49:06

Merge conflicts happen when multiple users change the same files across multiple branches. This means that conflicts have to be dealt with manually.

To demonstrate, make a new branch called **quick-test** and add something to the index.html

```bash
 ck@lemuree gogo-workflow (main)]$ git checkout -b quick-test          
Switched to a new branch 'quick-test'                                  

 ck@lemuree gogo-workflow (quick-test)]$ v index.html

 ck@lemuree gogo-workflow (quick-test)]$ git status                    
On branch quick-test                                                   
Changes not staged for commit:                                         
  (use "git add <file>..." to update what will be committed)           
  (use "git restore <file>..." to discard changes in working directory)
        modified:   index.html                                         
                                                                       
no changes added to commit (use "git add" and/or "git commit -a")      

 ck@lemuree gogo-workflow (quick-test)]$ git diff
 
diff --git a/index.html b/index.html
index 0fd9beb..206cf8b 100644       
--- a/index.html                    
+++ b/index.html                    
@@ -1 +1,2 @@                       
 <div>Hello</div>                   
+<p>world</p>                       
```
Shortcut: ```-am``` on commit means add modified files .. so no need to do ```git add . ``` first

```bash
 ck@lemuree gogo-workflow (quick-test)]$ git commit -am "added world to index.html"
[quick-test 07654d1] added world to index.html                                     
 1 files changed, 1 insertions(+) 
 ck@lemuree gogo-workflow (quick-test)]$                                           
```

Go back to main branch .. check that edits **did not** happen in main by looking at index.html ...
```bash
 ck@lemuree gogo-workflow (quick-test)]$ git checkout main 
Switched to branch 'main'                                  
Your branch is up to date with 'origin/main'.

 ck@lemuree gogo-workflow (main)]$ cat index.html
<div>Hello</div>                                 
 ck@lemuree gogo-workflow (main)]$               
```
Now, what if you update the line in index.html that was already changed in the quick-update branch?
```bash
 ck@lemuree gogo-workflow (main)]$ vim index.html
 ck@lemuree gogo-workflow (main)]$ git branch
* main                                                                            
  quick-test                                 
                                       
 ck@lemuree gogo-workflow (main)]$ git checkout quick-test                        
 
error: Your local changes to the following files would be overwritten by checkout:
        index.html                                                                
Please commit your changes or stash them before you switch branches.              
Aborting

 ck@lemuree gogo-workflow (main)]$
```

You get an error and shouldn't checkout the quick-update branch because the index.html will overwritten if you do.

(Video doesn't demonstrate **stash**, which puts changes in a temp holding place so you can retrieve them later.)

So, **commit** the changes in **main**.
```bash
 ck@lemuree gogo-workflow (main)]$ git commit -am "added there"
[main d047e3c] added there                                     
 1 file changed, 1 insertion(+)                                
 ck@lemuree gogo-workflow (main)]$ git checkout quick-test     
Switched to branch 'quick-test'                                
 ck@lemuree gogo-workflow (quick-test)]$
```

Now, review the changes ...

```bash
 ck@lemuree gogo-workflow (quick-test)]$ git diff main
```

## [Merge quick-test branch into main branch](https://youtu.be/RGOj5yH7evk?t=3208)
53:28

```bash
ck@lemuree gogo-workflow (quick-test)]$ git merge main
```
Why **merge locally** now? Earlier there was a warning about **not** doing this. Because ...

Main gets updated as others are working on, and doing PRs, for their branches. You won't have those changes in your branch and you don't want to get too far behind **main** while you're working on your own branch because it will make it more difficult to merge changes later.

So, as changes are made to **main** in the GitHub repo, you need to pull those down to your local **main** branch, and then whatever feature branch you're working off of, you'll want to do ```git merge main``` to keep your branch up to date with **main**.

But .. now there's a conflict ...
```bash
 ck@lemuree gogo-workflow (quick-test)]$ git merge main

Auto-merging index.html

CONFLICT (content): Merge conflict in index.html
Automatic merge failed; fix conflicts and then commit the result.

 ck@lemuree gogo-workflow (quick-test|MERGING)]$
                
```
**note**: I'm using git-completion shell script, so my prompt shows ```branch|MERGING```.

You can fix it
* on GitHub through their interface
* on your computer by editing the code

Edit index.html:
```bash
<div>Hello</d
<<<<<<< HEAD 
<p>world</p> 
=======      
<p>there</p> 
>>>>>>> main 
```

Between ```<<<<<< HEAD``` and ```======``` is the code in the current branch (quick-edit). After ```======``` and before ```>>>>>> main``` is the code coming from the other branch (main) that we're trying to merge in.

Delete the git-added conflict markers, and change the code however you need to (delete lines, or keep it all).

```bash
 ck@lemuree gogo-workflow (quick-test|MERGING)]$ vim index.html
 
 ... [edited and saved the file here] ...
 
 ck@lemuree gogo-workflow (quick-test|MERGING)]$ git status      
On branch quick-test                                             
You have unmerged paths.                                         
  (fix conflicts and run "git commit")                           
  (use "git merge --abort" to abort the merge)                   
                                                                 
Unmerged paths:                                                  
  (use "git add <file>..." to mark resolution)                   
        both modified:   index.html                              
                                                                 
no changes added to commit (use "git add" and/or "git commit -a")

 ck@lemuree gogo-workflow (quick-test|MERGING)]$ git diff        
diff --cc index.html                                             
index 206cf8b,c2e10f3..0000000                                   
--- a/index.html                                                 
+++ b/index.html                                                 
@@@ -1,2 -1,2 +1,3 @@@                                           
  <div>Hello</div>                                               
 +<p>world</p>                                                   
+ <p>there</p>                                                   

 ck@lemuree gogo-workflow (quick-test|MERGING)]$ git commit -am "updated with main"
[quick-test 2905e1b] updated with main                                             

 ck@lemuree gogo-workflow (quick-test)]$                                           

```                                                                 
Now changes from **main** have been updated in the current **quick-test** branch, so you can continue doing work in the current branch knowing that you have the latest from **main** incorporated into your local branch.

## [Undoing in Git](https://youtu.be/RGOj5yH7evk?t=3389)
56:29
* notes on this as needed


 


                                                                                  
































