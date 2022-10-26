# Intro

This is a total mess of a repo and you can break everything to learn how to use git. 

There is no perfect way to use this repo, in fact a lot of it won't be useful but might just be an idea for how to proceed. I'll also include some resources to learn git and it might behoove you to make a similar repo of your own and try to do things like you can find in the commit history: 

![mostRecentCommit](/assets/mostRecentCommit.png)
![parentCommit](/assets/parentCommit.png)

### Total Beginner
- [ ] [Git School](https://www.youtube.com/channel/UCshmCws1MijkZLMkPmOmzbQ) specifically, [start here](https://www.youtube.com/watch?v=OZEGnam2M9s&list=PLu-nSsOS6FRIg52MWrd7C_qSnQp3ZoHwW)
- [ ] [Github Docs](https://docs.github.com/en)
- [ ] [git scm](https://git-scm.com/docs)
- [ ] https://github.community/ 
- [ ] [Git Explorer](gitexplorer.com)
#### Markdown 
- [ ] https://guides.github.com/features/mastering-markdown/
- [ ] Www.markdownguide.org
- [ ] https://medium.com/swlh/create-awesome-git-readme-profile-84efa0bcda3b
- [ ] https://dev.to/github/10-standout-github-profile-readmes-h2o 
- [ ] https://docs.github.com/en/github/working-with-github-pages/about-github-pages#publishing-sources-for-github-pages-sites 

### Intermediate 
- [ ] [GitPals](https://www.gitpals.com)
- [ ] https://www.becomebetterprogrammer.com/git-rebase

### Advanced
- [ ] [Conquering Git: Advanced Training Guide](https://www.udemy.com/course/conquering-git-advanced-training-guide/) 
- [ ] [Extend GitHub](https://github.com/marketplace?type=) 

#### Devops
- [ ] [Gitlab](https://docs.gitlab.com/ee/README.html) 
- [ ] [About Gitlab](https://about.gitlab.com/)
- [ ] https://channel9.msdn.com/Shows/Azure-Friday/Learn-how-to-deploy-NET-Core-apps-to-Azure-with-GitHub-Actions 
- [ ] [GitHub Actions](https://docs.github.com/en/actions)

### Other resources
- [ ] https://gist.github.com/
- [ ] [Pluralsight Course on DevOps with Github and Azure: Implementing CI/CD with GitHub Actions](https://app.pluralsight.com/id/signin/?redirectTo=https%3A%2F%2Fapp.pluralsight.com%2Flibrary%2Fcourses%2F7d044527-6919-4968-8c0a-53ac4881968a%2Ftable-of-contents)
- [ ] https://www.gitguardian.com/
- [ ] https://github.blog/2020-09-30-code-scanning-is-now-available/
- [ ] https://github.blog/2020-09-17-github-cli-1-0-is-now-available/
- [ ] https://www.gitkraken.com/ 



***
Below are all my stupid notes as I did something. I would typically change this one readme to show a change as I worked through different problems locally and on the remote repo. 


# Tagging 
Here is a change to tag
- [Here is a great article on git tagging](https://devconnected.com/how-to-create-git-tags/)

- `git tag -a v1.2 -m "learning how to tag things"` - make tag with message
- `git tag -n` show tags and message
- `git push --tags` push tags
# Rebasing 
Removing text


- when you rebase with `git rebase master` when on a featureBranch based on older commit, HEAD is pointed at the master branch, while the changes you're rebasing onto master are the incoming changes. Further, the incoming changes, in the resolve conflicts view, come second, even if the work precedes what is already in master.
- Also, have to run `git add .` then `git rebase --continue` after resolving conflicts 
- When conflicts have been resolved, you'll want to run `git push origin <featureBranch> --force-with-lease` without pulling. [article on --force-with-lease](https://itnext.io/git-force-vs-force-with-lease-9d0e753e8c41)
- If it drops into an interactive rebase, update the commit message and maybe add another commit with additional changes

- this is a [good article for rebasing](https://www.becomgitebetterprogrammer.com/git-rebase/#10_Once_you_finish_rebasing_DO_NOT_pull_but_push_immediately_to_remote)

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
