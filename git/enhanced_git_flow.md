"Enhanced" Git Flow
================================================================================

_created: 2020-11-28_


Git flow works great but has some shortcomings:
--------------------------------------------------------------------------------

* **Mistakes** are likely to happen because of complex branch structure:
  Two long-lived branches, three types of temporary branches, and strict rules.
* **Release and hotfix branches require "double-merging"** - once into `main`
  and then into `develop`. You can forget to do both.
* In CI/CD workflows you usually end up with two final builds for a release:
  One from the latest commit to the `release` branch, and one from the merge
  commit to `main`.

Enhanced Git Flow Advantages
--------------------------------------------------------------------------------

It **simplifies** the more common maneuvers of the "Git Flow" workflow while
still reataining its advantages


Source
--------------------------------------------------------------------------------

* https://www.toptal.com/gitflow/enhanced-git-flow-explained
