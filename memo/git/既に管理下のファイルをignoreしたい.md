# Issue
ignoreしたいファイルをcommitしてしまったために、 `.gitignore` を書いても無視してもらえない。これは `.gitignore` が `Untracked files` にしか作用しないため。
```bash
$ echo "want_ignore" > .gitignore
$ git add .gitignore
$ git commit -m "Ignore"
[master e40c9d3] Ignore
 1 file changed, 1 insertion(+)
 create mode 100644 .gitignore
$ echo "hoge" > want_ignore
$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

        modified:   want_ignore

no changes added to commit (use "git add" and/or "git commit -a")
$
```

# Solution
`cached` だけ `git rm` してやることで、実ファイルを残したままgit上は削除したことにできる。本来は実ファイルが残っているのでまた `Untracked files` に出てきてしまうが、ここで `.gitignore` が生きるので以降無視される。
```bash
$ git rm --cached want_ignore
rm 'want_ignore'
$ git commit -m "Delete want_ignore"
[master 2ee8cb3] Delete want_ignore
 1 file changed, 0 insertions(+), 0 deletions(-)
 delete mode 100644 want_ignore
$ git status
On branch master
nothing to commit, working tree clean
$ echo "huga" > want_ignore
$ git status
On branch master
nothing to commit, working tree clean
$
```
