# git-test-space
A public repo used to mess around with git


To simpify, consider that you will always update your feature branch before a merge. If your feature branch does not have the latest from master, feature -> master will always lead to a non-fast-foward merge commit

# Merge vs rebase

* Rebase saves you the (non fast-forward) merge commit when you merge the latest master into your feature branch

* Either way, you use merge to go from feature -> master, because master is most certainly public and rebase deletes commits from the base (recipient) branch

* If you updated your feature branch before feature -> master, this will be a fast forward merge, and the merge commit is option, at the discretion of you / GitHub

* "Rewrite history"

  * merge won't preserve the **order** of commits
  
  * rebase won't preserve the bass / recipient branch (typically feature when used properly) commits **AT ALL**
  
* *Fast forward merge*: the recipient branch's HEAD COMMIT (current position, not to be mistaken with the "head" / donor branch) must be in the commit history of the donor / head branch.

  * master -> feature (update): never a fast forward, feature is the one with new stuff
  
  * feature -> master (PR): only a fast forward if you've updated your feature branch with the latest commits via merge / rebase.
  
* *Three way merge*: when your feature branch and master branch both have progessed, a new commit is necessary.

### Questions

What happens when you open / merge a GitHub PR in a 3 way merge scenario?

* Nothing special, you're good to go. It works the same way, if there are conflicts you get the editor. Just know that accepting the PR will always 100% give you a new commit in the recipient / base branch.

What happens when you open / merge a fast forward PR in GitHub?

* You still get a merge commit in GitHub, even though it's optional. I'm not sure if this functionality can be toggled for GitHub, but here are the relevant commands for ```git merge```:

  * ```--ff```: do NOT create a merge commit when fast forwarding. This is the defalut behavior of ```git```
  
  * ```--no-ff```: always create a merge commit, even if it's a fast forward. This is the default behavior of GitHub.
  
  * ```--ff-only```: refuse to merge and exit if no a fast forward scenario
  
  **CAUTON** when specifying both ```--no-ff``` and ```--ff-only```, ```--ff-only``` takes precedence and will ignore ```--no-ff```, so it will either merge with no commit in a fast forward scenario, or it will abort the merge and exit in any other scenario.


### Merge terminology

* feature -> master

* master -> feature

* head -> base

* donor -> recipient
