# blah

feature
feature 2


pushed feature 2 to master first, then pulled master, then rebased feature onto master
feature 2, reordering initial features
making changes to featureBranch1, based on ca29fb6


- when you rebase with `git rebase master` when on a featureBranch based on older commit, HEAD is pointed at the master branch, while the changes you're rebasing onto master are the incoming changes. Further, the incoming changes, in the resolve conflicts view, come second, even if the work proceeds what is already in master.
- Also, have to run `git rebase --continue` after resolving conflicts and adding them with `git add .`
- If it drops into an interactive rebase

- this is a [good article for rebasing](https://www.becomebetterprogrammer.com/git-rebase/#10_Once_you_finish_rebasing_DO_NOT_pull_but_push_immediately_to_remote)