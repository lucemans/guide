---
setup: |
  import Layout from '../src/layouts/BlogPost.astro'
  import Person from '../src/components/person/Person.astro'
title: Git Merge vs Rebase vs Squash
description: Merging vs Rebasing vs Squashing, and why you should pick one
slug: merge-strategy
type: guide
date: 1646315950153
published: true
---

# Merge vs Rebase vs Squash

There are an abundant amount of ways in which branches can be updated these ways which to even the more experienced developers sometimes is still an untouched taboo topic. In this document, I will aim to clarify a few of the most common methods (and default), and attempt to break them down a little in an effort to make this a more mainstream topic.

## None at all

Some people, notably the most rushed or careless ones, tend to commit straight to master. Committing straight to master is the easiest and fastest way to go provided you are the only one working on the entire repository. In any other case, where the team is bigger then just you, you will want to utalize one of the following.

## Merge

The traditional merge is by far the most used and oldest method of merging branches. The idea with merge is that your commits to a feature branch are summed up and added back to the main branch under a `merge commit`, these commits usually have a commit message along the lines of:

```
Merge branch 'feature/login' into master
```

In most cases I have noticed that the git history tends to get "cluttered" with a bunch of merge commits especially if the average commit length of your feature branches is low.

Merge commits follow a strategy along the lines of this.

![](/assets/git/Merge.png)

In this approach you will notice that `after merge the feature branch commits are still visible` and that our lovely `Merge commit is visible.`

## Rebase

When we rebase a branch we essentially bring the branch up to speed. A common example of this is in the event your `feature branch` runs behind on master, and before you call your feature "done" you might want to check if it will still work well with the latest updates from your team. In this event you would perform a rebase. A rebase in general looks something like this.

![](/assets/git/Rebase2.png)

In the above we see our commits essentially being recreated, one by one, ontop of the lastest core branch.

This same would apply in cases where we want to merge a feature branch into our master branch.

![Rebase Strategy](/assets/git/Rebase.png)

When we `rebase` our feature branch into our target branch we essentially just move every commit over and bring the repository up to speed.
Using this method we are still capable of retaining our git history and see the exact commits that did certain things, and at the same time we have `no merge unnecessary commits`

For most use cases this merging strategy is the most suitable. It allows you to keep a maintained, organized overview of the git history aswell as maintaining a history of each and every commit.

In contrairy to the [merge method](#merge) described above rebasing does not leave any lingering side-branches, pointers, and does not introduce in my opinion bloaty merge commits.

## Rebase and Squash

This is by far my favourite method of merging. It is similar to the above [rebase method](#rebase) in the way that it coppies over the current state of the feature branch onto the target branch, and combines it into a single commit. This commit ussually has a commit message being a combination of the pull request name, and the pull request number. Something like

```
Introduce Login Mechanics (#72)
```

On most platforms (github, gitlab, etc), you can click the [#72](https://www.youtube.com/watch?v=dQw4w9WgXcQ) and it will take you directly to the pull request, where you can view the commits that make up that feature.

The commit structure with this method looks something along the lines of the following

![](/assets/git/RebaseAndSquash.png)

In this example our feature branch is removed from view after it is merged (on github archived, so you can still recover it, don't worry), and a clean "summarizing commit" is placed instead.

## How to keep your graph organized

The default merging method for PR's for some reason is still [merge](#merge) which... over the course of time tends to interfere a lot of with the git history, leave a mess, and tends to be a pain to manage when it comes to reverting commits or cherry-picking.

In my current opinion I think that the only two viable options are [rebase](#rebase) and [squashing](#rebase-and-squash).

Depending on how granular you like to make your commits, and thereby commit frequency you might want to opt for using [squashing](#rebase-and-squash) as opposed to [rebase](#rebase) when there are multiple commits per feature, or you do not prefix your commits with what feature they belong to.

<p>Oh and obviously a special thanks to <Person name="svemat"/> for being part of my examples ;)</p>

~ Luc
