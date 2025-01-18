---
layout: post
title: Accidentally commit large files or sensitive data
date: 2024-11-03 11:12:00-0400
description: 
tags: 
categories:
related_posts: false
---

### What if I accidentally commit something？

Commit in Git is just like taking a snapshot of some of your data and save it in a folder called <code>.git</code>. Imagine you take snapshots of your room everyday. But one day you realize a sticky note with your bank password is on the wall! Although, you can tear off or avoid including it in the snapshots in the future. But anyone with your snapshot history will see it! In a nutshell, what you add/modify/delete in the working directory and what you commit in the future will not affect your commit history. They are just quietly lying there. 


### Where are them?

Sometimes, you even don't know where is your large files. So it is good to check them first. 


```
$ git rev-list --objects --all |
  git cat-file --batch-check='%(objecttype) %(objectname) %(objectsize) %(rest)' |
  sed -n 's/^blob //p' |
  sort --numeric-sort --key=2 |
  cut -c 1-12,41- |
```

This will give you human-readable output like this:
```
...
0d99bb931299  530KiB path/to/some-image.jpg
2ba44098e28f   12MiB path/to/hires-image.png
bd1741ddce0d   63MiB path/to/some-video-1080p.mp4
```
- [https://stackoverflow.com/questions/10622179/how-to-find-identify-large-commits-in-git-history](https://stackoverflow.com/questions/10622179/how-to-find-identify-large-commits-in-git-history)


### Rewrite history

Changing/deleting the history is highly risky, so make sure you really need to do it! There are also other ways you can share your repo without sharing the history or sharing part of the history. If you really think certain files should be deleted in the history in your repo, carefully follows tutorials:

- [https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/removing-sensitive-data-from-a-repository](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/removing-sensitive-data-from-a-repository)
- [https://www.geeksforgeeks.org/how-to-remove-a-large-file-from-commit-history-in-git/](https://www.geeksforgeeks.org/how-to-remove-a-large-file-from-commit-history-in-git/)
- [https://rtyley.github.io/bfg-repo-cleaner/](https://rtyley.github.io/bfg-repo-cleaner/)


At the end, don't forget to force push to the server because you have already rewritten the history. 

```
$ git push --force
```

### Good practice 

Next time, add the sticker note with your password into  <code>.gitignore</code> so that it will not be included in the snapshot.

- [https://git-scm.com/docs/gitignore](https://git-scm.com/docs/gitignore)