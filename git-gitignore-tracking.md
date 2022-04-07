
### bunch of disorganized notes ...
Trying to merge a branch caused a bunch of conflicts that were all files from Eclipse, Maven, Spring, etc. That is, they were all tied to the local development environment and not relevant to the project code base.

* Chris submitted a pull request that Clayton accepted
* now, Chris' local settings are part of the main branch
* Clayton submitted a pull request for another branch and was notified that it couldn't be automatically merged because of conflicts
* all the conflicts were in places like ```targets/``` and ```.settings/```
* went to  https://www.gitignore.io/ and generated .gitignore for Eclipse, Java, Maven and put that file in the repo root


* each local user has their own IDE setup (paths, settings) and each time a pull request is merged conflicts appear because no two users will have the exact same local settings.
* implementing ```.gitignore``` after the repo has been created is doesn't help with files that git is already tracking .. so these files have to be handled somehow

Working this out was a nightmare, but it seems like the latest merge worked without messing up previous merges.

### links

[git still shows files as modified after adding to .gitignore](https://stackoverflow.com/questions/9750606/git-still-shows-files-as-modified-after-adding-to-gitignore)

[Apply .gitignore on an existing repository already tracking large number of files](https://stackoverflow.com/questions/19663093/apply-gitignore-on-an-existing-repository-already-tracking-large-number-of-file)

[How can I make Git "forget" about a file that was tracked, but is now in .gitignore?](https://stackoverflow.com/questions/1274057/how-can-i-make-git-forget-about-a-file-that-was-tracked-but-is-now-in-gitign)

https://stackoverflow.com/questions/936249/how-to-stop-tracking-and-ignore-changes-to-a-file-in-git/40272289#40272289

[How to stop tracking and ignore changes to a file in Git?](https://stackoverflow.com/questions/936249/how-to-stop-tracking-and-ignore-changes-to-a-file-in-git)

[specific answer](https://stackoverflow.com/questions/936249/how-to-stop-tracking-and-ignore-changes-to-a-file-in-git/40272289#40272289)

[UNTRACK FILES IN GIT](http://source.kohlerville.com/2009/02/untrack-files-in-git/)

[Git merge errors](https://stackoverflow.com/questions/6006737/git-merge-errors)


