# testrepo

I am trying to figure out git subtree like this http://www.kitware.com/blog/home/post/899
Also this: https://www.kernel.org/pub/software/scm/git/docs/howto/using-merge-subtree.html

    git remote add -f Bproject /path/to/B
    git merge -s ours --no-commit Bproject/master
    git read-tree --prefix=dir-B/ -u Bproject/master
    git commit -m "Merge B project as our subdirectory"
    git pull -s subtree Bproject master
