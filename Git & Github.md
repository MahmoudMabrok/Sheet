# Git & Github


# Branches 


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

- used to clean history
- `squash`: make multiple commits into single commit 
- Steps 
  - git all commits `git log --oneline`
  - git base commit `git merge-base source target`, `source`: current branch `target`:branch you want to be base i.e oldest base commit 
  - after prev command you will git an ID use it here: `git rebase -i lastCommitID`
