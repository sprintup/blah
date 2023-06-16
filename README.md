# Intro

This is a total mess of a repo and you can break everything to learn how to use git. 

There is no perfect way to use this repo, in fact a lot of it won't be useful but might just be an idea for how to proceed. I'll also include some resources to learn git and it might behoove you to make a similar repo of your own and try to do things like you can find in the commit history: 


## Tutorial

We're going to learn how to merge first, then rebase. 
Open up two terminals side-by-side and run these commands (ask ChatGPT what they do if needed). I'm assuming we're starting with only one branch, master. 
Terminology 
- "repository" in Git is a directory where Git has been initialized to start version tracking. It is essentially your project's folder which contains all of the project files and the metadata about the project history stored in a subdirectory named .git. Each Git repository is standalone and contains the full history of the project. This means that if you have a copy of a Git repository, you have the entire project history on your local machine, making it robust against network failures or server crashes.
  - "Local repository:" This is the repository on your local machine where you make changes to your files. It's created using the git init command or cloned from a remote repository using git clone.
  - "Remote repository:" This is the repository that is hosted on a server on the internet or in a network. This is where developers push their changes for collaboration with others. Popular hosting services for remote Git repositories include GitHub, GitLab, and Bitbucket.
  - "cloning" creates a local copy of a repository, while "forking" creates a server-side copy of the repository under your own account.
    - "upstream" : is used to refer to the main branch or the original repository from which you cloned or forked. More specifically, it often refers to the branch that you're tracking in the original repository.
    - "Fork:" Forking, on the other hand, is a feature provided by hosting services like GitHub and GitLab that lets you create a personal copy of someone else's repository under your own account. This is used when you want to contribute to a project that you don't have write access to. After forking, you can clone the forked repository to your local machine, make changes, and then *** propose those changes back to the original repository by creating a pull request.*** The original repository owners can then review your changes and decide whether to merge them into the original repository.
    - "Clone:" Cloning is a Git operation that *** creates a copy of a repository on your local machine.*** When you clone a repository, you get a new directory on your computer with all the files and history of the repository. You can make changes to these files, commit those changes to your local repository, and push your commits back to the remote repository *** if you have write access.*** Cloning is typically used when you're starting to work on a project that you have write access to, or when you want to work on a project locally and don't need to publish your changes.
-a "branch" is essentially a unique set of code changes with a unique name. Each repository can have one or more branches, allowing you to work on multiple features simultaneously without them interfering with each other. The main branch (the one where all changes eventually get merged into) is usually called master or main.
  - Each branch in Git is a pointer to a specific commit, marking the 'tip' of a series of commits (i.e., the history of work done). New commits are added to the end of this series and pointed to by the branch.
  - When you create a new branch, Git creates a new pointer for you to move around. This means you can switch branches quickly and easily, as Git simply needs to move the *** HEAD pointer *** to a different commit. Creating a new branch doesn't change the repository; it simply adds a new pointer to the existing commits.
    - "HEAD" which is the latest commit of the currently checked out branch. When running `git log`, "HEAD" will be pointing to a branch. 
      - Detached HEAD: This is the state when HEAD points to a specific commit, instead of a branch. This can be risky because any changes made in this state won't belong to any branch and will be lost when you check out another branch. This situation usually occurs when checking out commits or tags instead of branches.
        - You can reattach HEAD to a branch by checking a branch out again with `git checkout branchname`
      - Attached HEAD: This is the usual state of HEAD when it points to the tip (the most recent commit) of the current branch.
- "commit" is a snapshot of your work that you've saved to your repository. *** Every commit is uniquely identified by a SHA-1 hash *** which represents a specific set of changes. Common SHAs mean a common history between branches. When SHAs change due to a command, that means the history has changed. 
  - "history" : refers to the sequence of commits made in a repository over time. Each commit represents a set of changes made to the project and is linked to the commit that came before it. This linking forms a chain of commits, which we call the commit history or simply "history".


- [git-rebase](https://git-scm.com/docs/git-rebase) - Reapply commits on top of another base tip
  - Base: The base, in the context of a rebase, is the commit on which you want to base your work on. When you run a rebase operation, Git finds the *common ancestor* of the current branch and the one you're rebasing onto, then applies each of the changes from your branch onto the head of the branch you're rebasing onto. This base commit is effectively the starting point of your changes.
  - Tip: The tip refers to the most recent commit of the branch, also known as the *** "HEAD" ***. In the context of a rebase, it means the latest commit in the branch that you're trying to rebase.
![mostRecentCommit](/assets/mostRecentCommit.png) 


- [git-merge](https://git-scm.com/docs/git-merge) - Join two or more development histories together


#### Left terminal
The left terminal is meant to only show graphs of history to become accustomed to how it looks.
- `git checkout master`
    - To simplify things, make sure 'HEAD' is always pointed at master in the left terminal. This means *** run `git checkout master` in the right terminal before running the next command in the left terminal. *** 
- `git log --pretty=oneline --graph --decorate --max-count=5 --all` -> only run this in the left terminal, one per time between all the right terminal commands
  - The latest commits across all branches will appear first, so if HEAD is not on the top line, there are commits that have occured more recently than the currently checked out branch. 
  - You can simply press up to rerun the command, instead of having to type it out every time. 

#### Right terminal
The right terminal is for running the majority of commands. 
*** Run only the commands in the top level of this bullet list. Nested commands are just explainations. Also, [Read the docs](https://git-scm.com/docs)*** Nested commands depend on the context of parent commands in this tree. 
- `git status` -> good to run anytime, shows status. 
  - `git commit -am "commit message"` is a shortcut combination to stage and commit your changes. (`git add .` and `git commit -m "commit message"`)
    - `git add --all` is a way to stage your changes. 
      - `git commit --amend` is a way to change the commit message of the previous commit, but this will create a new SHA (changes history)
  - To throw away 'Changes not staged for commit' run `git checkout .`
  - To throw away changes that *have* been staged (i.e. after using `git add .` shortcut or `git add --all` for all files) run `git reset` (optional `--soft` `--hard`)
- `git checkout master`
- `git checkout -b merge-branch`



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
