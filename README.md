subtree-patterns
================

My notepad for [git-subtree] patterns for drupal sysop.
[git-subtree]: https://github.com/apenwarr/git-subtree

Links:
* [git-subtree] repo by apenwarr
* [manpage](https://github.com/apenwarr/git-subtree/blob/master/git-subtree.txt)
* Examples:
  * [Having Fun With Git Subtree | h2ik](http://h2ik.co/2011/03/having-fun-with-git-subtree/) has some nice examples
  * [Using Git subtrees for repository separation – Making Software](http://makingsoftware.wordpress.com/2013/02/16/using-git-subtrees-for-repository-separation/)
* [Deploying a Git repository to a remote server | Wildly Inaccurate](http://wildlyinaccurate.com/deploying-a-git-repository-to-a-remote-server)
* [A few git tips you didn't know about](http://mislav.uniqpath.com/2010/07/git-tips/)
* [hub · the command-line wrapper for git](http://hub.github.com/)

# General objectives
* Patches to all components are tracked in the repository
* Patches can be re-applied after updates
* On updates patches should be rebased to easily re-upstream them

# Research topics
* Rebasing subtrees?
* Checkout a tag and have detached head?
* Slim subtree with only relevant commits to reduce repo weight? This will give for every use case a different solution.
* Can we drush-download from git directly into a subtree? Maybe with a suitable git pull versiontag:foo-upstream?
* Can we drush-download from git a single commit? 
 * See `git fetch --depth 1`, `git checkout --orphan new-branch`, `git checkout tree-ish -- .`
 * See [git - Why can't I push from a shallow clone? - Stack Overflow](http://stackoverflow.com/questions/6900103/why-cant-i-push-from-a-shallow-clone)
 * 

# Comparison to submodules
* (+) Has more drive, better toolbase and less clutter
* (+) Everything in repo, so does not rely on network connection
* (-) Not supported yet by drush and git_deploy.module
* (-) Large repository weight

# Slim subtree use cases

## Make component a subtree
* Subtree add foo-patched (checked out)
* Add branch foo-upstream = foo-patched
* (none of tha foo patches has a origin yet)

## Update component
* In workspace fork
* checkout foo-upstream
* dl foo & commit
* checkout foo-patched
* rebase

## Push patches
* Add foo fork repo branch mysite-patches as remote of foo-patched
* push
* cherry-pick them

# Complete subtree use cases - TODO
## Get new component as subtree
## Make existing unpatched component a subtree
## Make existing patched component a subtree
## Add or swap remote repository

# Appendix: Rebasing merge commits
* [How to rebase after git-subtree add? - Stack Overflow](http://stackoverflow.com/questions/12858199/how-to-rebase-after-git-subtree-add) - one answer suggests: `git rebase --preserve-merges --preserve-committer --onto new_place start end`, also see 
  * [What exactly does git's "rebase --preserve-merges" do (and why?) - Stack Overflow](http://stackoverflow.com/questions/15915430/what-exactly-does-gits-rebase-preserve-merges-do-and-why)
  * [Rebasing Merge Commits in Git | Envato Notes](http://notes.envato.com/developers/rebasing-merge-commits-in-git/)
  * [Alex's Corner: Git: Rebasing Merge Commits](http://apasca.blogspot.de/2012/02/git-rebasing-merge-commits.html)
