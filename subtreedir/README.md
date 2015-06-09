# testrepoprivate

If the base repo is public, and this subrepo is private and does contain 'secret' stuff, we should not use Subtree Merge.

We should instead use a Git Submodule to keep it safe, private, and separate

If the base repo was also private, we could use a Subtree Merge strategy to add the code into the private base repo.
