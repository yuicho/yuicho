# 前提
```python
>>> a = [1,2,4,4]
>>> b = [1,3]
```

# まず set にする
この時点で重複は省かれてしまう
```python
>>> set_a = set(a)
>>> set_b = set(b)
```

# 色々求める
## aにしかないもの
```python
>>> set_a = set(a)
>>> set_b = set(b)
```
## bにしかないもの
```python
>>> set_b - set_a
{3}
```
## どちらかにあるもの
```python
>>> set_a | set_b
{1, 2, 3, 4}
```
## どちらにもあるもの
```python
>>> set_a & set_b
{1}
```
