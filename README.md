# testrepo

## Discussion

If this base repo is public (as it is in this case), and the subrepo is private and does contain 'secret' stuff (also true), we should not use Git Subtree Merge.
We should instead use a Git Submodule to keep it safe, private, and separate.

Instead, if the base repo was also private, we could use the Git Subtree Merge strategy to add the code into the base repo.

If both repos were public, there may be advantages of each strategy: Git Subtree Merge allows easy inclusion, while Git Submodule might be better for optional stuff.

Both strategies are used in this repo as a demonstration of the right and wrong way to keep one's secret stuff private. 
The Git Subtree Merge exposes our private subrepo secret stuff in public in the subtreedir directory!
The Git Submodule method keeps our secret stuff safe in the private directory.

## Code

Create the original structure of the base repo:

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
    cd subtreedir/  
    git pull -s subtree subproj master  
    cd ..  
    # Pull Submodule changes  
    git submodule status
    cd private  
    git pull origin master  
    cd ..  
    # add the submodule changes  
    git add .  
    git commit -m 'push submodule update'  
    git push  

Clone repo and submodules:

    git clone --recursive git@bitbucket.org:davidbradway/testrepo.git
      
    # that does these for you:  
    git submodule init  
    git submodule update  

Information about the Submodules are contained in:
- .gitmodules
- .git/config

Information about the Subproj Remotes are contained in:
- .git/config

## References
1. First saw git subtree here: http://www.kitware.com/blog/home/post/899
2. Trying this: https://www.kernel.org/pub/software/scm/git/docs/howto/using-merge-subtree.html
3. This explanation is very good: http://blog.joncairns.com/2011/10/how-to-use-git-submodules/
