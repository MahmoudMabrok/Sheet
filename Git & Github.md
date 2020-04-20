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
