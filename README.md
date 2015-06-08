# testrepo

1. First saw git subtree here: http://www.kitware.com/blog/home/post/899
2. Trying this: https://www.kernel.org/pub/software/scm/git/docs/howto/using-merge-subtree.html

    # Clean out old git and push to remote
    cd Documents/GitHub/testrepoprivate/
    rm .git/* -rf
    git init
    git remote add origin git@bitbucket.org:davidbradway/testrepoprivate.git
    git add .
    git commit -m 'first commit'
    git push -u origin --all # pushes up the repo and its refs for the first time
    git push -u origin --tags # pushes up any tags
    
    # Clean out old git and push to remote
    cd ../testrepo
    rm .git/* -rf
    git init
    git add .
    mkdir subtreedir/
    git commit -m 'first commit'
    git remote add origin git@bitbucket.org:davidbradway/testrepo.git
    git push -u origin --all # pushes up the repo and its refs for the first time
    git push -u origin --tags # pushes up any tags
        
    # Merge subtree to subdir
    git remote add -f subproj git@bitbucket.org:davidbradway/testrepoprivate.git
    git merge -s ours --no-commit subproj/master
    git read-tree --prefix=subtreedir/ -u subproj/master
    git commit -m "Merge subproject repo as our subdir called subtreedir"

    # Pull subtree changes
    git pull -s subtree subproj master
