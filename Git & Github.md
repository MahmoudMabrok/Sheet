# Git & Github


# Branches 
- flow of a certain flow of code 
- create a new one and switch to it by `git checkout -b branchname`
- `git branch -a` list brnaches 

# Merge 
- Get Updates from branch to another one 
- Fast Forward: occurs when there is Taget branch is just moved to end of Source branch 
- Steps 
  - checkout to Taget branch `git checkout target`
  - merge the source `git merge source`

# Compare branches
-  `git diff branch1 branch2`

# Rebase
- Not use it with public branch 
- Cause problems when working with teams and may lose work 
- Check guidelines of teams(some teams not prefere rebase )
- **used to clean history**
- `squash`: make multiple commits into single commit 
- Steps 
  - git all commits `git log --oneline`
  - git base commit `git merge-base source target`, `source`: current branch `target`:branch you want to be base i.e oldest base commit 
  - after prev command you will git an ID use it here: `git rebase -i lastCommitID`
  - it will show all commits, with options such as pick (commit will remain as it is ), squash (will be jonined with other)
  - choose one to pick and other to squash and choose a final message 

# Cherry Pick 
- **copy some commits** from branch to another 
- Use case is Hotfix, move **hotfix** commits to other branches 
- Steps 
  - get commit id you want to copy, you can use `git log --oneline` 
  - checkout to **target branch** (i.e where copy to).
  - `git cherry-pick commitID`


# Working with Teams 
## Remotes 
- references to project (Github, bitbucket, gitlab,..etc). 
- it is a url added to VCS 
- when you clone project git create a local master branche and names remote as `origin`
- you can add one by `git remote add name url`
- you can list all remotes by  `git remove -v`
- use fetch to get latest info from remotes  `git fetch` or use `git fetch origin branch4`
- then you switch and track it, `git checkout --track origin branch4`

## Diff 
- `git diff HEAD`:changes between current state and last commit 
- `git diff commitid`:changes between current state and this commit 
- `git diff commit commit`: changes between these commits 
- `git diff branch branch`: changes between these branches 
- `git diff feature..master`: what changed at master after feature offed from master
- `git diff feature master file.txt`: what changed to file.txt  bettween feature,master

## Convensions
- use **samller commits** rather than one big commit
- use same **.gitignore** file
- use branches make testing is easy, branch that is success with test being merged to master 

## Commits
- use commit with related changes 
- use a proper message name for commit 
- add body of it propriate 
- **Empty spaces** git count them as changes and may cause errors, so format code before submit it 
- **Line Ending** it differs from OS to another so prefer to enforce one for all team

## Pull Request
- when finish your work push to remote 
- make pull request to master for example 
- add reviewers 
- when he approve, it be ,erged to master 

## Merge Conflicts
- occurs when files changed at both branches, git can not determine how to combine them 
- it marks files, let you combine and commit them again and make **merge commit**
- **merge commit**: is a commit has two parent commits. 

## Merge tips 
- pull latest changes from remote before merge
- when solve conflict add it as seprate commit (to make it easy to return if want to abort merge).
- you will get this with conflict 
  ```
  <<<<HEAD
  1
  2
  ======
  4
  5
  >>>>> master
  ```
  `======` is serartor,
  `above` is current code ,
  `below` is master code, **then**
  `you should combine them as you want, save, and commit`
  
  

