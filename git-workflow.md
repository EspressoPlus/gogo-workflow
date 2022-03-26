
# [Git basics - a general workflow](https://gist.github.com/blackfalcon/8428401)
* good guide, but goes beyond what we will (probably) need

# [Git and GitHub for Beginners - Crash Course - YouTube](https://www.youtube.com/watch?v=RGOj5yH7evk)
Branching and merging starts [here](https://youtu.be/RGOj5yH7evk?t=1956).
notes:
* long video, but does a great job .. worth the extra time
* skip first half if you know git basics already
* uses git integrated with VS Code, so you'll need to adapt to your IDE/system
* uses "master" rather than "main" branch

## GitHub Workflow

edit / add files via website
    |
    v
commit changes
    |
    v
make pull request
(if code review required)


## Local git Workflow

edit / add files
    |
    v
stage changes: git add
    |
    v
commit changes: git commit
    |
    v
push changes: git push
    |
    v
make a pull request
(if code review required)

# [Git Branching](https://youtu.be/RGOj5yH7evk?t=1963)

## Merging a Branch
go into the repo's dirctory
```
ck@mycomputer:zz-repo$ cd demo-repo
```

switch into git/bash CLI (or another flavor)

list branches
```
ck@mycomputer zz-repo (main)]$ git branch
```

create a new branch
```
ck@mycomputer zz-repo (feature-readme-instructions)]$ git checkout -b feature-readme-instructions
```

add lines to README.md with your preferred editor
```
ck@mycomputer zz-repo (feature-readme-instructions)]$ vim README.md
```

check for changes to branch .. should show that README.md was modified
```
ck@mycomputer zz-repo (feature-readme-instructions)]$ git status
```

add the file, and commit the change
```
ck@mycomputer zz-repo (feature-readme-instructions)]$ git add README.md
ck@mycomputer zz-repo (feature-readme-instructions)]$ git commit -m "updated readme"
```

go back to main branch and look at README.md .. it won't show changes made in feature-readme-instructions branch
```
ck@mycomputer zz-repo (feature-readme-instructions)]$ git checkout main
ck@mycomputer zz-repo (main)]$ cat README.md
```

*** you should just before you make your pull request ***
*pull* the repo's main branch so you have the most up to date version
```
 ck@mycomputer zz-repo (main)]$ git pull origin main
```

While still in main branch, look at the differences in the code between branches
this will show text that hasn't been changed in white
red text is not yet in the current (main) branch

```
 ck@mycomputer zz-repo (main)]$ git diff feature-readme-instructions 
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

here, you could merge, but this would only merge locally
```
*** DON'T DO THIS !!!!!!!!!!!!!!! ***
 ck@mycomputer zz-repo (main)]$ git merge feature-readme-instructions 
```

It's better to push the changes on the branch back to GitHub and then make a pull request
check status just be be sure.

```
 ck@mycomputer zz-repo (main)]$ git checkout feature-readme-instructions
 ck@mycomputer zz-repo (feature-readme-instructions)]$ git status
 ck@mycomputer zz-repo (feature-readme-instructions)]$ git push
fatal: The current branch feature-readme-instructions has no upstream branch.
To push the current branch and set the remote as upstream, use

    git push --set-upstream origin feature-readme-instructions

 ck@mycomputer zz-repo (feature-readme-instructions)]$ 
```
note:
```-u``` is short for ```--set-upstream```  

```
 ck@mycomputer zz-repo (feature-readme-instructions)]$ git push -u origin feature-readme-instructions
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

In the example above, the request is for the branch feature-readme-instructions to be pulled into branch main.

Once there is a PR, anyone with access to the repo on GitHub can review/comment/ask for changes to the code that is from the branch that made the PR.

You can copy the URL from the command-line output above, or you can just go to the GitHub repo and you'll see a notification about the recent pull request (green button: 'Compare & pull request')

Give the PR a title and provide bullets to describe the changes, the click the green 'Create pull request' button.

GitHub will let you know if there are/aren't conflicts. Before you click the green 'Merge pull request' button, you can add more comments (Conversation tab), or use the Commits or Files changed tabs. Under the 'Files changed' you can add comments for specific lines directly ('Add a single comment' button) in the code.

Once all the comments and conversations are "complete", clicking the 'Merge pull request' button will merge the working branch into the main branch.

After the PR is merged you can check the main branch to see that the repo was updated properly.

Back to your local computer to clean up .. pull to get the latest repo ... 

```
 ck@mycomputer zz-repo (feature-readme-instructions)]$ git checkout main 
Switched to branch 'main'
Your branch is up to date with 'origin/main'.
 ck@mycomputer zz-repo (main)]$ git pull 
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
 ck@mycomputer zz-repo (main)]$ git branch
  feature-readme-instructions
  front-controller
* main
```

... and delete the local branch ...

```
 ck@mycomputer zz-repo (main)]$ git branch -d feature-readme-instructions 
Deleted branch feature-readme-instructions (was 9e1369f).
 ck@mycomputer zz-repo (main)]$ git branch
  front-controller
* main
 ck@mycomputer zz-repo (main)]$ 
```

