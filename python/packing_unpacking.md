## Packing

변수 하나에 여러 값을 담는 것(묶어줌)

```sql
>>> a = 1,2,3
>>> a
(1, 2, 3)
```

또는 position argument에서 packing이 적용됨 → 튜플로 묶어준다.

```sql
>>> def a(*args):
...     print(args)

>>> a(1,2,3)
(1, 2, 3)
```

keyword arguments에서도 packing이 적용됨 → 딕셔너리로 묶어준다.

```sql
>>> def b(**kwargs):
...     print(kwargs)

>>> b(a="hello", b="world")
{'a': 'hello', 'b': 'world'}
```
<br>

## Unpacking

변수 안의 값을 여러 변수로 나눔

```sql
>>> a, b = (1, 2)
>>> a
1
>>> b
2
```

또한 함수 호출시 인자에 `*`(위치 인자), `**`(키워드 인자)를 붙이면 unpack 가능(함수 정의시에는 붙이지 않음)

```sql
>>> def test_unpack(a,b,c):
...     print(a, b, c)
>>> list_a = [1,2,3]
>>> dic_b = {'a': 1, 'b': 2, 'c': 3}

# List Unpack
>>> test_unpack(list_a)
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: test_unpack() missing 2 required positional arguments: 'b' and 'c'
>>> test_unpack(*list_a)
1 2 3

# Dictonary Unpack
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: test_unpack() missing 2 required positional arguments: 'b' and 'c'
>>> test_unpack(**dic_b)
1 2 3
>>> test_unpack(*dic_b)
a b c
```

즉, 함수 정의시에 `*`, `**`가 붙는다면 packing, 함수 호출 시에 `*`, `**`가 붙는다면 unpacking이다.

### +) unpacking을 이용해서 간단히 swap하기

```sql
>>> list = [1,2,3,4]
>>> list[1], list[0] = list[0], list[1]
>>> list
[2, 1, 3, 4]
```

먼저 우항의 `list[0], list[1]`에서 임시 튜플이 생성되며 이 튜플은 좌항의 `list[1], list[0]`으로 언패킹되어 list의 첫번째와 두번째 요소가 swap된다.
