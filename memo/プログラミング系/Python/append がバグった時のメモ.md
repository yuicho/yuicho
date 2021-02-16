dictを使い回してappendするような時はコピーしないとバグる元になる。

# どゆこと？
例えばこんな感じ
```python
>>> _tmp = dict()
>>> _list = list()
>>> 
>>> _tmp['a'] = 'hoge'
>>> _list.append(_dict)
>>> 
>>> _tmp['b'] = 'huga'
>>> _list.append(_dict)
>>> 
>>> _list
[{'a': 'hoge', 'b': 'huga'}, {'a': 'hoge', 'b': 'huga'}]
>>> 
```
この時 `_list` は `[{'a': 'hoge'}, {'a': 'hoge', 'b': 'huga'}]` となるはずでは……？

# なんでなん？
listにおける `append` は、要素のコピーではなく `id` の追加だから
```python
>>> id(_list[0])
139632634542408
>>> id(_list[1])
139632634542408
>>> 
```
つまり、一時的な `_tmp` を作って `_list[]` へ転記するイメージではなく、単純に `_tmp` というモノへのリンクを貼っているだけなイメージ。

# じゃあどうすればええのん？
いじる前にコピることで `id` が変わる
```python
>>> import copy
>>> 
>>> _tmp = dict()
>>> _list = list()
>>> 
>>> _tmp['a'] = 'hoge'
>>> _list.append(_tmp)
>>> 
>>> _tmp = copy.deepcopy(_tmp)
>>> _tmp['b'] = 'huga'
>>> _list.append(_tmp)
>>> 
>>> _list
[{'a': 'hoge'}, {'a': 'hoge', 'b': 'huga'}]
>>> id(_list[0])
139797555681536
>>> id(_list[1])
139797556515248
>>> 
```

# というか……
使いまわしつつ途中で `append` とか普通ありえないけど、ちゃんと使った後は初期化しようねっていう話。
```python
>>> _tmp = dict()
>>> _list = list()
>>> 
>>> _tmp['a'] = 'hoge'
>>> _list.append(_tmp)
>>> 
>>> _tmp = dict(_tmp)
>>> _tmp['b'] = 'huga'
>>> _list.append(_tmp)
>>> 
>>> _list
[{'a': 'hoge'}, {'a': 'hoge', 'b': 'huga'}]
>>> 
```
