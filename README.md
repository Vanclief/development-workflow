# development-workflow
A General Development workflow based on Github and OpenProject. Special thanks to 
[Thoughtbot](https://thoughtbot.com/), [Rhomeister](https://github.com/rhomeister), and
[Atlasian](https://www.atlassian.com/git/tutorials/).

TODO:
- [x] Rebase Guidelines
- [ ] Branch Workflow Guidelines
- [ ] Commit Guidelines
- [ ] Pull Request Review Guidelines
- [ ] Report Issue Guidelines
- [ ] Pull Request Guidelines

## Setup

1. Go to [Estudio I Open Project](https://www.shapeandcode.com/admin), and check if there is any Work Item assigned to you for the current iteration. If there is no Work Item assigned to you, and you have not fulfilled your hours, then talk to your Project Product Owner.

2. Plan what you are going to do. This involves any kind of Software Engineering that is required before your start coding.

3. Go to the project folder, make sure your repository is up to date with the remote one. To do this run the following commands:

```
git fetch --all
```
_This command will update the local copies of the remote branch_

```
git pull --all
```
_WARNING: This command will update local branches with the remote branch_

4. Create a new branch from either `develop` or an specific branch if you need
work realized on it. Use our naming conventions:

* For User Story 21: US-21/Login

* For Feature Database Upgrade: Feature/Database-Upgrade

* For Bug #21 with Login: Bug-21/Login

* For a Hotfix: Hotfix/Database


## Work in Progress

1. While working on your branch, make commits often, and craft good commit
descriptions.

_Examples:_

* "Created a new Controller for purchases" - Good

* "Finished controller" - Bad (What controller?)

* "Fix" - Bad

* "Fix bug with Navigation in Product View" - Good

_You can create temporary commits like "WIP" as long as they are squashed latter
before merging the branch._


2. Keep pushing your commits to the remote repository, never work on a stale
branch.

3. If work is required from another branch that is being worked on, perform a
Rebase of it (Check the Rebase Section).

4. At the end of each day, log the amount of hours worked on the task in
OpenProject.

## Finishing a task

Once you have finished working on the task, perform the following steps to make
sure your work is ready to be merged.

1. Run tests in your **local environment**.

2. Test in your **local environment** that the task that you worked in is completely functional and
fulfills the requirements for "Finished" that the Task required.

3. Check that your branch has passed on the continuous integration and delivery platform.

4. Perform a rebase on the branch that you will be merging to. Check the Rebase
Guideline for step by step instructions.

5. Create a Pull Request following the _Pull Request Guidelines_

## Approving a Pull Request

TODO

## Merging a Pull Request

Once a pull request has been approved, perform the following steps from the
command line. *Do NOT merge though the Github interface*. In this example we
will be merging the `feature` branch into `master`.

1. _Make sure the branch we are merging to is up to date_

`git checkout master`

`git fetch && git pull`

2. _Merge the branch_

`git merge feature`

3. _Since we are using rebase, and likelly recrafting the history, we need to
   use force_

`git push --force`

4. _Thats it!_

## Branch Workflow Guidelines
TODO

## Pull Request Guidelines
TODO

## Rebase Guidelines


*Why Rebasing?*

Rebasing allows crafting a much cleaner project history.

*What is Rebasing?*

[Explanation](https://www.atlassian.com/git/tutorials/merging-vs-rebasing)

*TL;DR*

![Rebase Image](https://i.stack.imgur.com/5yRg3.png)

*How do I rebase?*

For this example, we will be assuming we will be rebasing `feature` into
`master`.

1. _Lets first make sure the branch we want to rebase from is up to date_

`git checkout master`

`git fetch && git pull`

2. 2. _Lets go back to our branch_

`git checkout -`

3. _Now, lets start the rebase:_

`git rebase -i develop`

Now a text editor will show up with a list of all the commits the rebase will be
working with:

![Rebase -i](http://fusionpbx-docs.readthedocs.io/en/latest/_images/github_rebase_3.png)

We have a couple of commands:

```
# Commands:
# p, pick = use commit
# r, reword = use commit, but edit the commit message
# e, edit = use commit, but stop for amending
# s, squash = use commit, but meld into previous commit
# f, fixup = like "squash", but discard this commit's log message
# x, exec = run command (the rest of the line) using shell
# d, drop = remove commit*
```

What we want to do is to craft the best commit history we can, so we will
`squash` all the commits that are not useful to have in the commit history. (Fro
example: WIP). And we pick the rest.

4. _Solving conflits_

Sooner or latter you will experience Conflicts during a rebase.

```
error: could not apply fa39187... something to add to patch A

When you have resolved this problem, run "git rebase --continue".
If you prefer to skip this patch, run "git rebase --skip" instead.
To check out the original branch and stop rebasing, run "git rebase --abort".
Could not apply fa39187f3c3dfd2ab5faa38ac01cf3de7ce2e841... Change fake file
```

You have three choises:

a) Run `git rebase --abort` to completely undo the rebase. Git will return you to your branch's state as it was before git rebase was called.

b) Run `git rebase --skip` to completely skip the commit. That means that none of the changes introduced by the problematic commit will be included. *Unless you are absolutelly sure about what you are doing, you should NOT choose this option.* 

c) Fix the conflict, and run `git rebase --continue`. Git will continue
processing the rest of the rebase.


`git push --force`

5. _Finishing up_

Since Rebase is Destructive by nature, you should make sure you performed your
rebase properly before pushing. Double check, run tests again and make sure
everything its on its place.

`git push --force`

_This command will overwrite the remote repository_

## Pull Request Guidelines
TODO
