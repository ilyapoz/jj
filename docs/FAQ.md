# Frequently asked questions

### Why does my branch not move to the new commit after `jj new/commit`?

Jujutsu's branches are akin to Git Tags, they always point to a single commit.
To move them, use `jj branch set`. 

### Where is my commit, why is it not visible in `jj log`? 

If you don't find it with `jj log -r 'all()'`, it may be time to set the config
`revsets.log` to something more matching.

See [revsets], [templates] and [config] for guidance.

### Is there something like `git rebase`? 

For now its recommended to rebase the commit individually with 
`jj rebase -s $changeid -d $new-parent`.

In the future there may be a `histedit` command, which alleviates that.


### How do I partially add changes from a file? 

With Jujutsu you never partially add hunks, as your always amending the 
`@` commit. You need to split it, as the `@` may already be complete.

This is easy doable with `jj split your-file`


### How can I keep my scratch files in the repository?

You can keep your notes and other scratch files in the repository, if you add 
a wildcard pattern to the `gitignore`. Something like `*.scratch` or 
`*.scratchpad` should do, after that rename the files you want to keep around
to match the pattern.

### How can I keep my Git-like workflow?

In contrast to Git, we suggest keeping the branch pointing at the first commit.
This is so you can keep adding child commits to the branch, to create a new commit, 
use `jj checkout/new heads(:your-branch)`.

To see your current work, use `jj log -r your-branch:` which means children of
`your branch`.


### How can I keep local changes around, but not use them for Pull Requests? 

In general you can create a local commit, which incorporates your changes and 
then rebase all your open work on it. Before creating a PR, remove the 
change from the branches history with e.g `jj rebase -s $change-id -d main`. 



[config]: ./config.md
[revsets]: ./revsets.md
[templates]: ./templates.md
