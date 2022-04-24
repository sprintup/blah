# Rebasing 

feature  
feature 2  

pushed feature 2 to master first, then pulled master, then rebased feature onto master
feature 2, reordering initial features
making changes to featureBranch1, based on ca29fb6


- when you rebase with `git rebase master` when on a featureBranch based on older commit, HEAD is pointed at the master branch, while the changes you're rebasing onto master are the incoming changes. Further, the incoming changes, in the resolve conflicts view, come second, even if the work preceeds what is already in master.
- Also, have to run `git add .` then `git rebase --continue` after resolving conflicts 
- When conflicts have been resolved, you'll want to run `git push origin <featureBranch> --force-with-lease` without pulling. [article on --force-with-lease](https://itnext.io/git-force-vs-force-with-lease-9d0e753e8c41)
- If it drops into an interactive rebase, update the commit message and maybe add another commit with additional changes

- this is a [good article for rebasing](https://www.becomebetterprogrammer.com/git-rebase/#10_Once_you_finish_rebasing_DO_NOT_pull_but_push_immediately_to_remote)

***
# Combining commits
`git reset --soft HEAD~3` combines this many commits -> includes 3 commits total starting with HEAD
![before](/assets/reset.png)
![after](/assets/after.png)

***
# Deleting commits
[good article on deleting commits](https://www.w3docs.com/snippets/git/deleting-commits-from-a-branch-in-git.html)
 - `git reset --hard HEAD~N` where N is the number of commits to remove
 
 # Git Reflog
 - `git reflog` will show you even deleted commits that can be checked out with a `git reset --hard <sha>`

 # Amending commit 
 - `git commit --amend`
