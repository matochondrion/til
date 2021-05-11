Diff All Files From Two Branches and Cherry Pick
================================================================================

*created: 2021-05-10*


Using Difftool With Fugitive
--------------------------------------------------------------------------------

Vim Fugitive comes with a number of niceties that make using git with vim
easier.  While you can use vim as the default `git difftool`, using vim this
way may not load many the user settings or use Fugitive during the process.

To make diff'ing two branches more convenient, it's easier to use fugitive from
inside vim by entering the following in command mode:

```
# To compare master to the current branch:
# (replace `master` with the name of any branch to be compared)
:G difftool -y master..

```

The `-y` flag instructs Fugitive, via git difftool, to open and compare all
files between the two branches.

There is minimal
[documentation](https://github.com/tpope/vim-fugitive/blob/master/doc/fugitive.txt#L80)
for the `-y` flag in `doc/fugitive.txt`.
