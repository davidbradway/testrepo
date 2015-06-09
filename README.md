# testrepo

1. First saw git subtree here: http://www.kitware.com/blog/home/post/899
2. Trying this: https://www.kernel.org/pub/software/scm/git/docs/howto/using-merge-subtree.html


If this base repo is public (as it is in this case), and this subrepo is private and does contain 'secret' stuff, (also true) we should not use Subtree Merge.

We should instead use a Git Submodule to keep it safe, private, and separate

If the base repo was also private, we could use a Subtree Merge strategy to add the code into the private base repo.

If both repos are public, there may be advantages of each strategy: Subtree Merge allows easy inclusion while Submodule might be better for optional stuff.

Both strategies are demonstrated in this repo as a demonstration. Below is the code to create the structure of the repo:

    # SUBTREE - merges subtree into repo  
    # Merge subtree to subdir  
    git remote add -f subproj git@bitbucket.org:davidbradway/testrepoprivate.git  
    git merge -s ours --no-commit subproj/master  
    git read-tree --prefix=subtreedir/ -u subproj/master  
    git commit -m "Merge subproject repo as our subdir called subtreedir"  
    # Pull subtree changes  
    git pull -s subtree subproj master  
  
    # SUBMODULE - links subrepo as submodule  
    git submodule add git@bitbucket.org:davidbradway/testrepoprivate.git private  

Update code:

    # Pull subtree changes  
    git pull -s subtree subproj master  
  
    git pull  