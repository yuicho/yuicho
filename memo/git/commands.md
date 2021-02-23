# よく使うコマンド
## 実ファイルはそのまま `Untracked files` にする
commitした後に `.gitignore` に追加したときとか
```console
git rm --cached want_ignore
```
## `submodule` があるリポジトリをcloneするときに `--recursive` し忘れた
`submodule add` で `--recursive` し忘れた時も同じ
```console
git submodule update --init --recursive
```
