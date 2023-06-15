# Intro
f2 changes
This is a total mess of a repo and you can break everything to learn how to use git. 

There is no perfect way to use this repo, in fact a lot of it won't be useful but might just be an idea for how to proceed. I'll also include some resources to learn git and it might behoove you to make a similar repo of your own and try to do things like you can find in the commit history: 

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
