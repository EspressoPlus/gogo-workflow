# Overview:
This summarizes section of the **Git and GitHub for Beginners - Crash Course** where they work through the process of making a local branch, making a pull request, then merging with the main branch, starting at [35:55](https://youtu.be/RGOj5yH7evk?t=2155).

```
 git clone UrlToTheRepo             # clone the repo
 [ you're currently                 # necessary only if you don't have the repo locally
   in the *main* branch ]
        |
        v
 git checkout -b feature-branch     # make feature-branch (local) and switch to it
        |
        v
 Eclipse/IDE                        # edit/write/add code 
        |
        v
 git status                         # list changed/added files
        |
        v
 git add .                          # saves all changes to feature-branch
        |
        v
 git commit -m "your message"       # commit feature-branch changes
        |
        v
 git checkout main                  # back to main
        |
        v
 git pull origin main               # get latest main
        |
        v
 git diff feature-branch            # review differences: main vs feature-branch
        |
        v
 git checkout feature-branch        # back to feature-branch
        |
        v
 git push -u origin feature-branch  # push changes upstream
        |
        v
 GitHub: make a pull request        # 'Compare & pull request' green button
        |
        v
 GitHub: someone else reviews pull request and accepts/rejects/asks for changes
        |
        v
 git branch -d feature-branch       # delete local copy of feature-branch
```


# Feature Branching for gogoMoney
Many of these notes come from this [Git and GitHub for Beginners](https://youtu.be/RGOj5yH7evk?t=1956) video tutorial.

[git-crash-course.md](https://github.com/EspressoPlus/gogo-workflow/blob/main/git-crash-course.md) has notes with times form important sections of the tutorial


## Local | CLI | first time only: getting the repo to local computer
Make a directory to hold the repo/project.

Clone repo to your local computer into the directory.

Commands depend on whether you do http, ssh, or GitHub CLI.

ssh approach:
```bash
git clone git@github.com:EspressoPlus/gogoMoney.git
```
Add/import the project to Eclipse EE workspace and open it.

In Eclipse you should see it named gogoMoney ```[gogoMoney main]```.

![gogoMoney_main.png](https://github.com/EspressoPlus/gogo-workflow/blob/main/gogoMoney_main.png)


## Local | CLI | make local branch
Create a new branch on your computer. Name the branch something descriptive like "back-dao" or "dao-updates".
```bash
git checkout -b test-back-dao
```
Ensure that you are working in your new branch.
```bash
git branch
```

## Local | Eclipse | how branch appears in GUI
If you open the project in Eclipse you should see that it has switched to the local branch that you are working on: ```[gogoMoney test-back-dao]```.

![gogoMoney_test-back-dao.png](https://github.com/EspressoPlus/gogo-workflow/blob/main/gogoMoney_test-back-dao.png)

You may have to close/open/refresh the Eclipse project if it doesn't show like this.

DO NOT WORK ON YOUR CODE UNTIL **ECLIPSE** SHOWS THAT YOU ARE IN THE CORRECT BRANCH

## Local | Eclipse | edit, update, add code
In Eclipse, edit your code and save it. You could test by editing a line (e.g. add a comment) or adding a dummy package.

Eclipse puts a **```>```** in front of packages and files that have been changed

![gogoMoney_Eclipse-w-changes.png](https://github.com/EspressoPlus/gogo-workflow/blob/main/gogoMoney_Eclipse-w-changes.png)


## Local | CLI | check status
Check which files have been updated.
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
Switch back to your branch and confirm that everything is in order: check status, add your files, check status again.
```bash
git checkout test-back-dao
git status
git add .
git commit -m "test back dao branch experiment"
git status
```


## Local | CLI | pull main
This is **CRITICAL** because you need to have the most up-to-date version of **main** from GitHub
```bash
git checkout main
git pull origin main
```
Check how your branch differs from main. You should see all the differences in your code
```bash
git diff test-back-dao
```

---
>>## Push the feature branch, then make a Pull Request (PR)
>>The Crash Course video, [from 43:24 to 44:35](https://youtu.be/RGOj5yH7evk?t=2604), explains the process of **pushing** your branch then making a **pull request**.
>>
>>A pull request is a request to have your code pulled into another branch.
>>
>>In the example below, the feature branch *test-back-dao* will be **pushed** and then a **pull request** will be made for that branch to be **pulled** ( = fetch + merge) into the *main* branch.
>>
>>Once there is a PR, anyone with access to the repo on GitHub can review/comment/ask for changes to the code from the branch that made the PR.
>>
>>Note that even after there is a PR (but the branch is not yet merged) the branch's code can still be updated by making additional commits and pushing them up to GitHub. These commits will be reflected on GitHub as long as the commits are on the same branch where the PR is happening.
>>
---


## Local | CLI | push your branch upstream
Your branch now includes all of your code changes. Now **push** your branch upstream. This makes the branch available on github.
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
Watch the Crash Course video [from 44:35  to 45:45](https://youtu.be/RGOj5yH7evk?t=2675) for a demonstration.

Afterwards, check that the changes actually happened in the **main** branch.


## Make a Pull Request
After you push your branch successfully, there will be a notification at the top of the GitHub repo (on the website) that reads "Your recently pushed branches:", then your branch's name, and a green 🟢Compare & pull request🟢 button.

Click the 🟢green🟢 button and you'll be directed to a **Open a pull request** page. Go through the process of creating the request, described below.


## Local | CLI | pull from main and delete local branch
Locally, make sure you're in the main branch, then do a pull so you get latest version of the main branch.

Now you'll see the changes that have been merged into main.
```bash
git checkout main
git pull
```
There is no need to keep the feature branch that you made (unless you want to for .. reasons) because the feature branch's changes are now incorporated into main branch.
```bash
 ck@lemuree gogoMoney (main)]$ git branch -d test-back-dao
Deleted branch test-back-dao (was b1ba737).
 ck@lemuree gogoMoney (main)]$ git branch 
* main
```
Now only the main branch remains.









