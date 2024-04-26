# Intro

This is a total mess of a repo and you can break everything to learn how to use git. 

There is no perfect way to use this repo, in fact a lot of it won't be useful but might just be an idea for how to proceed. I'll also include some resources to learn git and it might behoove you to make a similar repo of your own and try to do things like you can find in the commit history: 


## Tutorial

We're going to learn how to merge first, then rebase. 
Open up two terminals side-by-side and run these commands (ask ChatGPT what they do if needed). I'm assuming we're starting with only one branch, master. 
Terminology 
- __repository__ in Git is a directory where Git has been initialized to start version tracking. It is essentially your project's folder which contains all of the project files and the metadata about the project history stored in a subdirectory named .git. Each Git repository is standalone and contains the full history of the project. This means that if you have a copy of a Git repository, you have the entire project history on your local machine, making it robust against network failures or server crashes.
  - __Local repository:__ This is the repository on your local machine where you make changes to your files. It's created using the git init command or cloned from a remote repository using git clone.
  - __Remote repository:__ This is the repository that is hosted on a server on the internet or in a network. This is where developers push their changes for collaboration with others. Popular hosting services for remote Git repositories include GitHub, GitLab, and Bitbucket.
  - __cloning__ creates a local copy of a repository, while __forking__ creates a server-side copy of the repository under your own account.
    - __upstream__ : is used to refer to the main branch or the original repository from which you cloned or forked. More specifically, it often refers to the branch that you're tracking in the original repository.
    - __Fork:__ Forking, on the other hand, is a feature provided by hosting services like GitHub and GitLab that lets you create a personal copy of someone else's repository under your own account. This is used when you want to contribute to a project that you don't have write access to. After forking, you can clone the forked repository to your local machine, make changes, and then__propose those changes back to the original repository by creating a pull request.__The original repository owners can then review your changes and decide whether to merge them into the original repository.
    - __Clone:__ Cloning is a Git operation that__creates a copy of a repository on your local machine.__When you clone a repository, you get a new directory on your computer with all the files and history of the repository. You can make changes to these files, commit those changes to your local repository, and push your commits back to the remote repository__if you have write access.__Cloning is typically used when you're starting to work on a project that you have write access to, or when you want to work on a project locally and don't need to publish your changes.
-a __branch__ is essentially a unique set of code changes with a unique name. Each repository can have one or more branches, allowing you to work on multiple features simultaneously without them interfering with each other. The main branch (the one where all changes eventually get merged into) is usually called master or main.
  - Each branch in Git is a pointer to a specific commit, marking the 'tip' of a series of commits (i.e., the history of work done). New commits are added to the end of this series and pointed to by the branch.
  - When you create a new branch, Git creates a new pointer for you to move around. This means you can switch branches quickly and easily, as Git simply needs to move the__HEAD pointer__to a different commit. Creating a new branch doesn't change the repository; it simply adds a new pointer to the existing commits.
    - __HEAD__ which is the latest commit of the currently checked out branch. When running `git log`, __HEAD__ will be pointing to a branch. 
      - Detached HEAD: This is the state when HEAD points to a specific commit, instead of a branch. This can be risky because any changes made in this state won't belong to any branch and will be lost when you check out another branch. This situation usually occurs when checking out commits or tags instead of branches.
        - You can reattach HEAD to a branch by checking a branch out again with `git checkout branchname`
      - Attached HEAD: This is the usual state of HEAD when it points to the tip (the most recent commit) of the current branch.
- __commit__ is a snapshot of your work that you've saved to your repository.__Every commit is uniquely identified by a SHA-1 hash__which represents a specific set of changes. Common SHAs mean a common history between branches. When SHAs change due to a command, that means the history has changed. 
  - __history__ : refers to the sequence of commits made in a repository over time. Each commit represents a set of changes made to the project and is linked to the commit that came before it. This linking forms a chain of commits, which we call the commit history or simply __history__.
    - __diverge__ : when Git tells you that histories have diverged, it means that there are commits in your current branch that aren't in the branch you're trying to merge with, or pull from, and vice versa. Divergent histories can be rectified with either a rebase or a merge.
      - [git-rebase](https://git-scm.com/docs/git-rebase) - Reapply commits on top of another base tip
        - Base: The base, in the context of a rebase, is the commit on which you want to base your work on. When you run a rebase operation, Git finds the *common ancestor* of the current branch and the one you're rebasing onto, then applies each of the changes from your branch onto the head of the branch you're rebasing onto. This base commit is effectively the starting point of your changes.
        - Tip: The tip refers to the most recent commit of the branch, also known as the__ HEAD __. In the context of a rebase, it means the latest commit in the branch that you're trying to rebase.
      ![rebase](/assets/tutorial/rebase.png) 
      - [git-merge](https://git-scm.com/docs/git-merge) - Join two or more development histories together
        -__after a merge, do you have to add a commit?__
          - In Git, when you perform a merge, a new commit is automatically created if the merge involves divergent paths from the base commit (the common ancestor commit). This new commit is called a __merge commit,__ and it has multiple parent commits.
          - When you run git merge branchname, Git attempts to automatically merge the changes from the specified branch into the current branch. If the changes don't conflict, a new commit (the merge commit) is automatically created, and you don't need to do anything else.
          - If there are conflicts between the branches that Git can't resolve on its own, Git will pause the merge and tell you which files have conflicts. You'll have to manually edit those files to resolve the conflicts, and then stage the resolved files with git add. After resolving all conflicts and staging the changes, you run git commit to complete the merge with a new commit. This commit is also a merge commit, but its creation was not automatic, because manual conflict resolution was involved.
          - So, after a merge, you don't usually have to add a new commit yourself, because Git does it for you. The exception is when there are merge conflicts that need to be resolved manually. After resolving these conflicts, you will have to complete the merge commit yourself.
        -__what does it mean to 'fast-forward' in git?__
          - __Fast-forward__ is a term used in Git when you are merging one branch that is ahead of the current branch, and there are no new changes on the current branch since it diverged.
            - Let's consider an example. You're working on a project and you have a master branch. You decide to create a new branch called feature from master and make some commits. During this time, no other changes were made to the master branch. If you checkout to master and merge feature, Git doesn't have to create a new merge commit. Instead, it can simply __fast-forward__ the master branch pointer to point to the same commit feature is pointing to, as this will bring master up to date with feature.
            - This operation is called a __fast-forward__ because you're moving the branch pointer forward along the commit history, making it point to the most recent commit.
      ![rebase](/assets/tutorial/merge.png) 
    - __conflict__ : Conflicts in Git occur when two or more changes clash with each other, and Git is unable to determine which change should take precedence. This typically happens when multiple developers are working on the same project simultaneously, and their changes overlap. 
      - The `<<<<<<< HEAD` line marks the beginning of the conflicting section.
      - The `=======` line separates the conflicting changes.
      - The `>>>>>>>` branch-being-merged line marks the end of the conflicting section.
    - To resolve the conflict, you need to manually edit the file to choose one change or the other and delete the added symbols. After you've resolved the conflict, you use git add filename to mark the file as resolved, and then git commit to finish the merge.    
    
Here's an example of what a conflict might look like:

```
<<<<<<< HEAD
This is some text from the current branch.
=======
This is some different text from the branch being merged.
>>>>>>> branch-being-merged

```
### Coding part start  - please read the instructions

#### Left terminal - Command prompt
The left terminal is meant to only show graphs of history to become accustomed to how it looks.
- `git log --pretty=oneline --graph --decorate --max-count=5 --all --abbrev-commit` -> only run this in the left terminal, one per time between all the right terminal commands
  - The latest commits across all branches will appear first, so if HEAD is not on the top line, there are commits that have occured more recently than the currently chec
  ked out branch. 
  - You can simply press up to rerun the command, instead of having to type it out every time. 

#### Right terminal - VS Code with terminal open and readme open
The right terminal is for running the majority of commands. Mark off the commands as you run them by placing an X inside the `- [ ]` so it looks like `- [X]`. This will trigger 'changes' that you can commit so you can view the history. The only required commands are in the top level of this bullet list (marked with -[ ]). Nested commands are just explainations. Also, [Read the docs](https://git-scm.com/docs). Nested commands depend on the context of parent commands in this tree. If you try running the nested commands, you might get stuck in a state and have to run `git checkout master` then `git fetch origin` and `git reset --hard origin/master` to start over.



- [ ] `git status` -> good to run anytime, shows status. 
    - `git commit -am "commit message"` is a shortcut combination to stage and commit your changes. (`git add .` and `git commit -m "commit message"`)
      - `git add --all` is a way to stage your changes. 
        - `git commit --amend` is a way to change the commit message of the previous commit, but this will create a new SHA (changes history)
    - To throw away 'Changes not staged for commit' run `git checkout .`
    - To throw away changes that *have* been staged (i.e. after using `git add .` shortcut or `git add --all` for all files) run `git reset` (optional `--soft` `--hard`)
  
- [ ] `git checkout master`
    - delete all other branches with `git branch -d other-branch-name` passing `-f` if needed. 
  
- [ ] `git commit -m "tutorial start"`
  
- [ ] `git checkout -b merge-branch`
    - make sure tocheck the checkboxs up to this point and save the file
  
- [ ] `git commit -am "changes made in merge-branch"`
    - remember to run the left terminal between every command so you can see what the repository is doing. Right now *** HEAD *** should be pointed at `merge-branch`. Also, the latest commit "changes made in merge-branch" should be on top, while the master branch is pointed to the second commit "tutorial start". This means `merge-branch` is one commit ahead of master. This can be verified by running `git rev-list --count master..HEAD`. To see how many commits `master` is ahead of `merge-branch` try running `git rev-list --count HEAD..master`. The result should be 1 and 0 respectively. 
  
- [ ] `git checkout master`
    - remember to check the checkboxes as you go (remember to save the file too), and keep producing new graphs to see what changes.
  
- [ ] `git commit -am "changes on master"`
    - This should make it so master is back in the first position and __HEAD__ should be pointed at master, because it's the currently checked out branch. Both __merge-branch__ and __master__ can't fit on the same line, so __merge-branch__ is indented. However if you run `git rev-list --count merge-branch..master` again, it should show 1, which means __master__ has one commit that __merge-branch__ does not. Comparitively, if you reverse the command like `git rev-list --count master..merge-branch`, it should show that __merge-branch__ also has one commit that master does not. This means that "histories have diverged" and we need to rectify it with either a rebase or a merge. 
    - Since we're working on the __merge-branch__, we'll perform a merge. 
  
- [ ] `git merge merge-branch` from master
    - This command will replay changes made on __merge-branch__ since it diverged from __master__(one commit ago) until the current commit of __merge-branch__. It does this on top of master. 
    - This should result in a conflict, where the changes for HEAD (master) are listed on top, even though we added them second. This means we need to move them down, below the merge branch and remove the symbols. 
    - Notice the conflicts appear in a special file, where the title is marked with an exlamation point and the terminal mentions 'Merging'. Since we're currently resolving conflicts, we'll need to close this file and add this merge of both files as a new commit.
    - What happens if you start on __merge-branch__ and run `git merge master`? 
      - When you issue the command git merge, you are saying *** "merge the specified branch into the current branch." *** In other words, you are bringing changes from the specified branch into the one currently checked out.
  
- [ ] `git commit -am "merged merge-branch into master"`
    - When you run the graph, you should see HEAD pointed at master as the most recent commit and __merge-branch__ one commit behind. We'll fix this, but first...
    - `git rev-list --count master..merge-branch` will give you the number of commits that are in the__merge-branch__but not in __master__. 
      - Should be 0, because we merged the changes of __merge-branch__ into master.
    - `git rev-list --count merge-branch..master` will give you the number of commits that are in the __master__ but not in __merge-branch__. 
      - Should be 2, because there was the original commit we made on __master__("changes on master") and the subsequent merge commit ("merged merge-branch into master")
    - `git log --pretty=oneline --max-count=5 --abbrev-commit` to see the history of the currently checked out branch. In this case __master__ which shows the "changes made in merge-branch" commit and the associated __merge-branch__ just below. 
      - The line that reconnects __merge-branch__ to master, indicating the changes were included back into master. 
      - The stars indicate which branch the commit lives on. 
      - *** Comparing this to the same graph in the below rebase is key to understanding the difference between a merge and rebase ***
    - Now if you wanted __merge-branch__ to be at the same commit, you would want to merge changes from __master__ into __merge-branch__, which would require checking out __merge-branch__ and running `git merge master`. Then look at the graph and you'll see both branches on the same commit.

- [ ] `git checkout master`

- [ ] `git commit -am "rebase start"`
    - Remember to check the box to trigger a change to the file. 

- [ ] `git checkout -b rebase-branch`
    - One of the things to notice is that if you make changes while on one branch, you can move to a *new* branch without needing to check them in. This is not the case if you're moving to an *existing* branch. You'll have to manage your changes by either 
      - Commiting them
      - Throwing them out with something like `git checkout .` or `git reset`
      - Stashing them with `git stash save "Your descriptive message here"` and `git stash pop`

- [ ] `git commit -am "changes made on rebase branch"`
    - Check the graph, HEAD should be pointing at rebase-branch and "changes made on rebase branch should be on top"

- [ ] `git checkout master`

- [ ] `git commit -am "changes on master before rebase"`
    - need to add some changes to __master__ branch that is not on __rebase-branch__.

- [ ] `git checkout rebase-branch`
    - changes are alreadyhere from before and we just need to run a rebase.

- [ ] `git commit -am "more changes on rebase-branch before rebase"`
    - Mark this complete before rebase to avoid common changes bug. 

- [ ] `git rebase master`
    - When you run the command `git rebase`, you are saying **"reapply the commits from the current branch onto the branch I specify."** In this case, we're applying the changes "changes made on rebase branch" onto __ master__, since we specified master.
    - The special file with the conflicts may appear. Once you resolve the conflicts, *close this file* and proceed to the next command.

- [ ] `git add .`

- [ ] `git rebase --continue`
    - Now you'll see "changes made on rebase branch" on top, with master one commit behind. HEAD is pointed at __rebase-branch__ of the latest commit. 
    - *** Compare this graph to the graph mentioned above to understand the difference between rebase and merge ***
    - To bring __master__ to the current state of __rebase-branch__ (which now has "changes on master before rebase") continue with the following commands

- [ ] `git checkout master`

- [ ] `git rebase rebase-branch`
    - Remember rebase means "reapply the commits from the current branch onto the branch I specify." Since there are no new commits to move into __rebase-branch__, it has nothing to 'pick up and rebase' kinda like a fat snowman picking up his body and putting on another branch, so it'll just move the pointer from the commit "changes on master before rebase" to "changes made on rebase branch".
    - As a reminder, merge means "merge the specified branch into the current branch."
    - Some final notes, the way git determines if the how many commits ahead/behind a branch is from another is by comparing the SHAs, so if the SHAs are different, it'll think the history is different, even if the changes are the same. This means you'll have to account for this if you ammend commits, which changes the SHAs. 

### What's the difference between a merge and rebase?
![rebase](/assets/tutorial/merge_rebase.png) 

Both `merge` and `rebase` in Git are designed to integrate changes from one branch into another, but they do it in different ways and the resulting history will look different.

#### Here's how they work:

Merge: git merge takes the contents of a source branch and integrates it with the target branch. When you merge a branch, it takes the contents of that branch and merges it with your current branch all at once. This creates a new "merge commit" in the history that has two parents, maintaining the historical context of the branch.

Rebase: git rebase moves or combines a sequence of commits to a new base commit. Essentially, it's like saying "I want to base my changes on what everybody else has already done." When you rebase, Git takes the changes made in each commit of your current branch that are not in the upstream branch and saves them away temporarily. It then applies the changes of the upstream branch to your base commit, and re-applies your changes on top of that, one by one. This results in a linear history.

#### Here are the key differences:

History: merge preserves the history of your commits exactly as they were, while rebase rewrites the commit history in order to produce a more linear project history.

Merge Conflicts: In case of overlapping changes, with merge, you'll only need to resolve conflicts once. With rebase, conflicts need to be resolved for each commit separately, as changes are applied one by one.

Traceability: Merge keeps all the past history of commits, making it easy to see when and how changes were made. Rebase provides a more simplified and linear project history, without the noise of non-significant commits.

Safety and Collaboration: merge is a safe operation that won't alter existing history, making it a good choice for public or collaborative branches. rebase alters commit history, which can be problematic for anyone else who's already using the existing branches, so it's generally recommended for cleaning up local branches.

In a nutshell, if you want to combine your changes with another branch while preserving chronological commit history, use merge. If you want to make your feature branch up to date with the latest code from the target branch, while maintaining a clean, linear history, use rebase.

## Additional resources
### Total Beginner
- [ ] [Git School](https://www.youtube.com/channel/UCshmCws1MijkZLMkPmOmzbQ) specifically, [start here](https://www.youtube.com/watch?v=OZEGnam2M9s&list=PLu-nSsOS6FRIg52MWrd7C_qSnQp3ZoHwW)
- [ ] [Intro to Git in 16 mins](https://vickyikechukwu.hashnode.dev/introduction-to-git-in-16-minutes?utm_source=tldrnewsletter)
- [ ] [9 Beginner Friendly Tutorials](https://www.deployhq.com/git)
- [ ] [Writing better commit messages](https://www.freecodecamp.org/news/how-to-write-better-git-commit-messages/)
- [ ] [Github Docs](https://docs.github.com/en)
- [ ] [git scm](https://git-scm.com/docs)
- [ ] [Github Community](https://github.community/)
- [ ] [Git Explorer](gitexplorer.com)
#### Markdown 
- [ ] [Basic writing and formatting syntax](https://guides.github.com/features/mastering-markdown/)
- [ ] [The Markdown Guide](https://www.markdownguide.org/cheat-sheet/)
- [ ] [Create Awesome Git readMe Profile](https://medium.com/swlh/create-awesome-git-readme-profile-84efa0bcda3b)
- [ ] [10 Standout GitHub Profile READMEs](https://dev.to/github/10-standout-github-profile-readmes-h2o)
- [ ] [Publishing sources for GitHub Pages sites](https://docs.github.com/en/github/working-with-github-pages/about-github-pages#publishing-sources-for-github-pages-sites)
- [ ] [Awesome Developer Profile](https://github.com/coderjojo/creative-profile-readme)

### Intermediate 
- [ ] [GitPals](https://www.gitpals.com)
- [ ] [Take advantage of Git Rebase](https://about.gitlab.com/blog/2022/10/06/take-advantage-of-git-rebase/)
- [ ] [How to rebase in Git: Explained Step by Step](https://www.becomebetterprogrammer.com/git-rebase)
- [ ] [Effective Git for Solo Developer](https://mikkel.ca/blog/git-is-my-buddy-effective-solo-developer/?utm_source=tldrnewsletter)
- [ ] [Github 1s](https://github.com/conwnet/github1s)
- [ ] [Git ignore templates](https://github.com/github/gitignore)

### Advanced
- [ ] [Conquering Git: Advanced Training Guide](https://www.udemy.com/course/conquering-git-advanced-training-guide/) 
- [ ] [Atlassian Advanced Git Tutorial](https://www.atlassian.com/git/tutorials/advanced-overview)
- [ ] [Extend GitHub](https://github.com/marketplace?type=) 

#### Devops
- [ ] [Gitlab](https://docs.gitlab.com/ee/README.html) 
- [ ] [About Gitlab](https://about.gitlab.com/)
- [ ] https://channel9.msdn.com/Shows/Azure-Friday/Learn-how-to-deploy-NET-Core-apps-to-Azure-with-GitHub-Actions 
- [ ] [GitHub Actions](https://docs.github.com/en/actions)
- [ ] [DevSec Ops](https://github.com/sottlmarek/DevSecOps?utm_source=tldrnewsletter)

### Other resources
- [ ] [Gist](https://gist.github.com/)
- [ ] [Pluralsight Course on DevOps with Github and Azure: Implementing CI/CD with GitHub Actions](https://app.pluralsight.com/id/signin/?redirectTo=https%3A%2F%2Fapp.pluralsight.com%2Flibrary%2Fcourses%2F7d044527-6919-4968-8c0a-53ac4881968a%2Ftable-of-contents)
- [ ] [Git Guardian](https://www.gitguardian.com/)
- [ ] [Code Scanning](https://github.blog/2020-09-30-code-scanning-is-now-available/)
- [ ] [Github Cli 1.0](https://github.blog/2020-09-17-github-cli-1-0-is-now-available/)
- [ ] [GitKraken Client](https://www.gitkraken.com/)
- [ ] [Lazy Git Client](https://github.com/jesseduffield/lazygit)



***

# Merging vs Rebasing
- Merging preserves history exactly as it happened (same SHAs) and merges it into one single timeline
- rebasing creates new commit (SHAs for changes in history)
- `git log --all --decorate --oneline --graph --max-count=5` shows all branchs graph history, limiting to last 5 commits; 

##### This is what the setup looks like:
- The process was create two subsequent commits on branch f1, then 2 commits on branch f2, then a third commit on f1 and run either a merge or rebase.
![prepRebase](/assets/prepRebase.png) 

##### In the below image, on top you can see the history after a rebase. On the bottom the history after a merge:
- The original f2 branch for the rebase is not shown, but it wouldn't have the same SHAs as what is shown. 
![afterBoth](/assets/afterBoth.png) 

# [Merging](https://git-scm.com/docs/git-merge)
- move to branch you want to move changes into then run `git merge branchWhereChangesAreComingFrom`

### Before Merge
![prepRebase](/assets/prepRebase.png) 
### After Merge
- Note: had to reconcile conflicts to produce result
  - ![afterMerge](/assets/afterMerge.png) 

# [Rebasing](https://git-scm.com/docs/git-rebase)
### Before rebase on branch f1:
- ![beforeRebasef1](/assets/beforeRebasef1.png) 
  - Note: Sometimes the graph command can flip things:
  - ![beforeRebasef1b](/assets/beforeRebasef1b.png) 

### After rebase see above red line (below red line is example of merge)
- ![afterBoth](/assets/afterBoth.png) 

## Rebase Operation
- another difference is which branch you start the operation on. During a rebase you start on the branch you would like to detatch from the commit that is the common origin (origin commit that other branch you want to move the commits onto has in common) and write the branch you're moving the commmits onto. For instance if I'm trying to move f2 commits onto f1, I would start on f2 and write `git rebase f1`
- when you rebase with `git rebase master` when on a featureBranch based on older commit, HEAD is pointed at the master branch, while the changes you're rebasing onto master are the incoming changes. Further, the incoming changes, in the resolve conflicts view, come second, even if the work precedes what is already in master.
- Also, have to run `git add .` then `git rebase --continue` after resolving conflicts 
- When conflicts have been resolved, you'll want to run `git push origin <featureBranch> --force-with-lease` without pulling. [article on --force-with-lease](https://itnext.io/git-force-vs-force-with-lease-9d0e753e8c41)
- If it drops into an interactive rebase, update the commit message and maybe add another commit with additional changes

***

# Tagging 

- [Here is a great article on git tagging](https://devconnected.com/how-to-create-git-tags/)
- [Another article on deleting tags](https://devconnected.com/how-to-delete-local-and-remote-tags-on-git/)

## Basic tagging
- `git tag -a v1.2 -m "learning how to tag things"` - make tag with message
- `git tag -n` show tags and message
- `git push --tags` push tags

## Adding tag to last commit
- `git tag <tag_name> HEAD`   (for the last commit)
- `git tag <tag_name> HEAD~1`  (for the commit before HEAD)
- `git tag -a <tag_name> HEAD -m "message"`

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

# Exploring the repo
![mostRecentCommit](/assets/mostRecentCommit.png)
![parentCommit](/assets/parentCommit.png)
"change" 
"third change" 
"second change" 

