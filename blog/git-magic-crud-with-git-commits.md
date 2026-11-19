---
type: Article
title: Git Magic – CRUD with Git commits
canonical_url: https://developer.webex.com/blog/git-magic-crud-with-git-commits
content_type: blog
date: '2023-09-14'
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/blog/git-magic-crud-with-git-commits)

Git is a great invention and such a boon that saves a lot of time for the developer community, and it is optimized to even bring your disappeared changes back. Therefore, this blog is an interesting compilation of various scenarios where a git commit can be modified in any manner. I would essentially call this a blog article that can tell you how to create, read, update, or delete your way into the git commits.



> **Info**
>
> Please read this blog fully before executing any command. The scenario mentioned might not be the same as yours. It is recommended to try these commands in a forked repository/branch only.



### Creating a commit

This is something that all the developers live and breathe. The most basic command for the whole of the developer community. Let us say you have made a few changes in some files of a repository. The steps to creating a commit are staging the changed files that need to be part of the commit and then committing. Let’s take a quick look at how to do it.

#### Staging files

We will use the `git add` command to do this as follows:

```bash
>> git add src/file_a.ts
>> git add src/file_b.ts
```

#### Committing staged files

We will use the `git commit` command to do this as follows:

```bash
>> git commit -m ‘feat(a): commit message’
[feature_a 9f6772400] feat(a): test a
2 files changed, 5 insertions(+), 3 deletions(-)
```

Tada. You created your first commit.

#### Reading a commit

Now, let’s look at how to view the created commit. To do this, you first need the commit hash. You can get the commit hash as follows:

```bash
>> git log --oneline
9f6772400 (HEAD -> feature_a) feat(a): test a
4f3e04707 (origin/feature_a) feat(a): feat a api implementation
```

We have two commits in the history as shown above. Out of that, the commit that we need to look at is the one we created recently, and the commit is at the beginning as indicated here: `9f6772400`

Now, to view the commit specifically, we shall use the git show command as follows:

```bash
>> git show 9f6772400
commit 9f677240054bcc82d59d75d6825ef4ce21bd02ef (HEAD -> feature_a)
Author: Kesava Krishnan Madavan [myemail@email.com](mailto:myemail@email.com)
Date:   Mon Sep 4 18:45:45 2023 +0530

   feat(a): test a

diff --git a/src/file_a.ts b/src/file_a.ts
index gf2e0bf5c..b63f1ce6d 100644
--- a/src/file_a.ts
+++ b/src/file_a.ts
@@ -1,3 +1,3 @@
 // a
 // a
 // a
```

This will give you a detailed view like the above example with differences in all the files that were included as part of the commit hash.

### Updating a commit

Now that we know how to create and view a commit, let us look at how we can update an existing commit. There are various scenarios where a commit would need an update. They may be:

- Adding or removing a new file to an existing commit
- Updating existing files of a commit
- Removing changes to a file of a commit

To do this we will use an additional attribute to the commit command called the `--amend`. Let us look at them one by one.

#### Adding or removing a new file to an existing commit

To add or remove a new file to the commit, we will have to first stage the file and then amend the commit. Additionally, to remove, you will have to simply remove the file from the code base. The following example shows how we remove the new `file_a.ts` and add a new `file_c.ts` to a commit.

```bash
>> rm file_a.ts
>> git add file_c.ts
>> git commit --amend
[feature_a 0debcg533] feat(a): test a
 Date:   Mon Sep 4 18:48:33 2023 +0530
 2 files changed, 8 insertions(+), 4 deletions(-)
```

Tada! Your commit is edited to add a new file now. Note that, for every commit amend, the commit hash will change. It has changed from `9f6772400` to `0debcg533`.

#### Updating existing files of a commit

This is like how you add a new file to the commit. Instead of adding a new file, one must edit the file that is already part of the commit, stage that file and amend the commit as shown below:

```bash
>> git add file_b.ts
>> git commit --amend
[feature_a 1efcdh644] feat(a): test a
 Date:   Mon Sep 4 18:48:33 2023 +0530
 2 files changed, 10 insertions(+), 4 deletions(-)
```

#### Removing changes to a particular file of a commit

This is a typical scenario where you have a bunch of changes to a file, and you want all of them removed from the commit without affecting changes to other files and ensure nothing is lost, you will have to check out the changes of the file to be discarded from the commit and then amend it to the existing commit as shown below:

```bash
>> git checkout upstream/main -- existing_file_b.js
>> git commit --amend
[feature_a 2fgdei755] feat(a): test a
 Date:   Mon Sep 4 18:50:12 2023 +0530
 2 files changed, 10 insertions(+), 4 deletions(-)
```

### Deleting a Commit

This can be done in multiple ways depending on the need. This can be split into two scenarios:

- Deleting the top few commits
- Dropping random commits from the history

<br/>

#### Deleting the top few commits

To delete the top few commits or the topmost commit, we must first look at the commit history as shown below:

```bash
>> git log --oneline
0debcg533 (HEAD -> feature_a) feat(a): test a
1efcdh644 (origin/feature_a) feat(a): feat a api implementation
d13bfb436 (upstream/feature_b) feat(b): initial setup and related changes (#1) 
2fgdei755 feat(s): refactor classes (#2)
3ghief866 (tag: v1.12.134) chore(release): v1.12.134 [skip ci]
4hijfg977 docs(api): update docs [skip ci]
```

In the above list, let us assume we need to delete the top two commits. In this case, we copy the commit hash that needs to be the new HEAD which in the current case is `d13bfb436`. Now to remove the top two commits, execute the following command:

```bash
>> git reset --hard d13bfb436
HEAD is now at d13bfb436 feat(b): initial setup and related changes (#1)
```

Tada! Your top two commits are now removed. You can check this by doing a `git log -–oneline`.

#### Dropping random commits from the history

Once again, to drop commits from history, you need to know which ones to drop. To find that, we shall first list the commit history:

```bash
>> git log --oneline
d13bfb436 (upstream/feature_b) feat(b): initial setup and related changes (#1) 
2fgdei755 feat(s): refactor classes (#2)
3ghief866 (tag: v1.12.134) chore(release): v1.12.134 [skip ci]
4hijfg977 docs(api): update docs [skip ci]
```

Let us assume we want to delete the following commit from the history without affecting other changes,

```bash
   2fgdei755 feat(s): refactor classes (#2)
```

It is the second commit from the top. Therefore, let’s take the count as 3.

To proceed, let us do an interactive rebasing where we will choose to drop the chosen commit. Execute the following command:

```bash
>> git rebase -i HEAD~3
pick d13bfb436 feat(b): initial setup and related changes (#1) 
pick 2fgdei755 feat(s): refactor classes (#2)
pick 3ghief866 chore(release): v1.12.134 [skip ci]
# Rebase 4hijfg977..d13bfb436 onto 4hijfg977 (3 commands)
#
# Commands:
# p, pick <commit> = use commit
# r, reword <commit> = use commit, but edit the commit message
# e, edit <commit> = use commit, but stop for amending
# s, squash <commit> = use commit, but meld into previous commit
# f, fixup [-C | -c] <commit> = like "squash" but keep only the previous
#                    commit's log message, unless -C is used, in which case
#                    keep only this commit's message; -c is same as -C but
#                    opens the editor
# x, exec <command> = run command (the rest of the line) using shell
# b, break = stop here (continue rebase later with 'git rebase --continue')
# d, drop <commit> = remove commit
# l, label <label> = label current HEAD with a name
# t, reset <;abel> = reset HEAD to a label
# m, merge [-C <commit> | -c <commit>] <label> [# <oneline>]
# .       create a merge commit using the original merge commit's
# .       message (or the oneline, if no original merge commit was
# .       specified); use -c <commit> to reword the commit message
#
# These lines can be re-ordered; they are executed from top to bottom.
#
```

An editor will open with the above-shown rebase commands and guidelines. In the list with three pick commands, we will have to drop the commit with commit hash: `2fgdei755`. Do the following to perform that:

```bash
>> git rebase -i HEAD~3
pick d13bfb436 feat(b): initial setup and related changes (#1) 
drop 2fgdei755 feat(s): refactor classes (#2)
pick 3ghief866 chore(release): v1.12.134 [skip ci]

# Rebase 4hijfg977..d13bfb436 onto 4hijfg977 (3 commands)
```

Notice that I have changed the `pick` to `drop` for the commit that needs to be dropped from history. Save and close the editor.

At this point, you might get into situations where conflicts could happen because of the commits you dropped. If that happens:

1. Resolve conflicts
1. Stage the changed files
1. Do a `git rebase --continue`

Do this until you get a successful rebase message and you’re all done. To know if the commits mentioned in the interactive rebase are dropped, check the commit history with a `git log --oneline` command.



> **Info**
>
> If you are trying to alter the commit history after the commits are pushed to remote, the updated commit history has to be pushed with a `git push --force` command.
