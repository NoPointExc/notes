### git: undo all working dir changes including new files ###
git reset --hard # removes staged and working directory changes

    ## !! be very careful with these !!
    ## you may end up deleting what you don't want to
    ## read comments and manual.
    git clean -f -d # remove untracked AND ignored files
    git clean -f -x -d # CAUTION: as above but removes ignored files like config.
    git clean -fxd :/ # CAUTION: as above, but cleans untracked and ignored files through the entire repo (without :/, the operation affects only the current directory)
    
### cherry-pick ###
Apply the changes introduced by some existing commits  

Given one or more existing commits, apply the change each one introduces, recording a new commit for each. This requires your working tree to be clean (no modifications from the HEAD commit).

ref: [https://git-scm.com/docs/git-cherry-pick](https://git-scm.com/docs/git-cherry-pick)

### FETCH_HEAD ###
FETCH_HEAD is a short-lived ref, to keep track of what has just been fetched from the remote repository.  
  
git pull first invokes git fetch, in normal cases fetching a branch from the remote.  ```FETCH_HEAD``` points to the tip of this branch (it stores the SHA1 of the commit, just as branches do). git pull then invokes git merge, merging FETCH_HEAD into the current branch.  

This is a bit like doing git fetch without arguments (or git remote update), updating all your remote branches, then running git merge origin/<branch>, but using FETCH_HEAD internally instead to refer to whatever single ref was fetched, instead of needing to name things.

E.g
```git fetch ssh://jiayangs@android.intel.com:29418/a/bsp/vendor/intel/common refs/changes/35/476835/1 && git cherry-pick FETCH_HEAD```  

fetch and cherry-pick from remote.




