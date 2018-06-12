---
title: Removing large files from you git version control
author: Thomas Goossens
date: '2018-06-12'
categories:
  - how-to
  - git
tags:
  - git
---

While working with geodata, you might often end up downloading large raw-data files likes `.shp` that you will need in your data process chain. 

As you don't want to keep this static files under version control, you must tell git to ignore these files. Usually, you do it by adding a rule to your `.gitignore` file. But what if those files were created before there were added to the `.gitignore` ? 

This problem happened to me this morning. My usual R specific `.gitignore` file was not setup to ignore large `.shp` files and I inadvertently added my `.shp` files to git. After some local commits, I pushed my work to my online repo and as it took a longer time than usual to upload, I suspected that large files were polluting my git index. 

So the first thing I did, is to add a "ignore the folder containing my geodata" rule to my `.gitignore` file : `geodata/`. To learn more about ignore folders, check [this](https://stackoverflow.com/questions/14700835/gitignore-a-folder-content?noredirect=1&lq=1) SO thread.

Then, because the ignoring rule was setup after those files were already added to my git index, I had to remove them from the cache :

```bash
$ git rm --cached <FOLDER_NAME_OR_FILE_NAME>
```

This command was found on [this](https://stackoverflow.com/questions/2047465/how-can-i-delete-a-file-from-git-repo) SO thread

If you want to inspect which files of your project are ignored by git, run this command from [this](https://stackoverflow.com/questions/15931238/unable-to-remove-file-that-really-exists-fatal-pathspec-did-not-match-any#15931542) SO thread :

```bash
$ git ls-files --others -i --exclude-standard
```

Finally, after adding the rule, and removing the files from my repository, I pushed again and ended up with the exact same problem : large files were being uploaded to my online repo. How could this be possible ? The problem, as mentioned in [this](https://stackoverflow.com/questions/19573031/cant-push-to-github-because-of-large-file-which-i-already-deleted#23657759) SO thread, was that the file was still in my history. So I simply executed this command to solve my problem : 

```bash
$ git filter-branch --index-filter 'git rm -r --cached --ignore-unmatch <file/dir>' HEAD
```