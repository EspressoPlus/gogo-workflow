# git-workflow for gogoMoney
Many of these notes come from this [Git and GitHub for Beginners](https://youtu.be/RGOj5yH7evk?t=1956) video tutorial.

[git-crash-course.md](need link) has notves with times form important sections of the tutorial


## Local | CLI | first time only: getting the repo to local computer
* make a directory to hold the repo/project
* clone repo to your local computer into the directory
* commands depend on whether you do http, ssh, or GitHub CLI
* ssh approach:
```bash
git clone git@github.com:EspressoPlus/gogoMoney.git
```
* add/import the project to Eclipse EE workspace and open it
* in Eclipse you should see it named gogoMoney ```[gogoMoney main]```

![gogoMoney_main.png](https://github.com/EspressoPlus/gogo-workflow/blob/main/gogoMoney_main.png)


## Local | CLI | make local branch
* create a new branch on your computer
* name the branch something descriptive like "back-dao" or "dao-updates"
```bash
git checkout -b test-back-dao
```
* ensure that you are working in your new branch
```bash
git branch
```

## Local | Eclipse | how branch appears in GUI
* if you open the project in Eclipse you should see that it has switched to the local branch that you are working on: ```[gogoMoney test-back-dao]```

![gogoMoney_test-back-dao.png](https://github.com/EspressoPlus/gogo-workflow/blob/main/gogoMoney_test-back-dao.png)

* you may have to close/open/refresh the Eclipse project if it doesn't show like this
* DO NOT WORK ON YOUR CODE UNTIL **ECLIPSE** SHOWS THAT YOU ARE IN THE CORRECT BRANCH

## Local | Eclipse | edit, update, add code
* in Eclipse, edit your code and save it
* you could test by editing a line (e.g. add a comment) or adding a dummy package
* **note**: Eclipse puts a **>** in front of packages and files that have been changed

![gogoMoney_Eclipse-w-changes.png](https://github.com/EspressoPlus/gogo-workflow/blob/main/gogoMoney_Eclipse-w-changes.png)


## Local | CLI | check status
* check which files have been updated
```bash
 ck@lemuree gogoMoney (test-back-dao)]$ git status

On branch test-back-dao

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   src/main/java/com/gogo/dao/MoneyDAO.java
        modified:   target/m2e-wtp/web-resources/META-INF/maven/com.gogo/gogoMoney/pom.properties

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        src/main/java/com/gogo/zzbort/
        target/classes/com/gogo/zzbort/

no changes added to commit (use "git add" and/or "git commit -a")

 ck@lemuree gogoMoney (test-back-dao)]$ 

```



## Local | CLI | add and commit changes
* it's probably good practice to close the Eclipse **project** (shouldn't need to close Eclipse) at this point


## Local | CLI | pull main
* this is **CRITICAL** because you need to have the most up-to-date version of **main** from GitHub
```bash
git checkout main
git pull origin main
```
* check how your branch differs from main .. you should see all the differences in your code
```bash
git diff test-back-dao
```


## Local | CLI | push changes
* switch back to your branch and confirm that everything is in order: check status, add your files, check status again
```bash
git checkout test-back-dao
git status
git add .
git commit -m "test back dao branch experiment"
git status
```
* **PUSH** upstream 
```bash
 ck@lemuree gogoMoney (test-back-dao)]$ git push

fatal: The current branch test-back-dao has no upstream branch.
To push the current branch and set the remote as upstream, use

    git push --set-upstream origin test-back-dao

 ck@lemuree gogoMoney (test-back-dao)]$ git push -u origin test-back-dao 

Enumerating objects: 43, done.
Counting objects: 100% (43/43), done.
Delta compression using up to 8 threads
Compressing objects: 100% (16/16), done.
Writing objects: 100% (24/24), 1.90 KiB | 1.90 MiB/s, done.
Total 24 (delta 4), reused 0 (delta 0)
remote: Resolving deltas: 100% (4/4), completed with 4 local objects.
To github.com:EspressoPlus/gogoMoney.git
   0172900..b1ba737  test-back-dao -> test-back-dao
Branch 'test-back-dao' set up to track remote branch 'test-back-dao' from 'origin'.
```

## GitHub | Web Ui | Pull Request & Merge
* watch [this section](https://youtu.be/RGOj5yH7evk?t=2675) of the video tutorial for a demonstration
* Clayton can demo this too
* afterwards, check that changes are in **main**


## Local | CLI | pull from main and delete local branch
* pull so you get latest main branch
* now, locally, you'll see the changes that have been merged into main
```bash
git checkout main
git pull
```
* no need to keep the branch (if you don't want to) because changes are now incorporated into main branch
```bash
 ck@lemuree gogoMoney (main)]$ git branch -d test-back-dao
Deleted branch test-back-dao (was b1ba737).
 ck@lemuree gogoMoney (main)]$ git branch 
* main
```
* now only the main branch remains




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
