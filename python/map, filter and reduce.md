## `map()`, `filter()`, `reduce()`
이 함수들은 python에서 함수적인 접근을 가능하게 하며(functional programming) for loop, list comprehension을 대체할 수 있다.

<br>

### Note: lambda
위의 함수들을 사용할 때 lambda와 함께 많이 쓰는데 그 이유는 첫번째 인자로 들어오는 함수들은 보통 일회성으로 사용되기 때문에 굳이 정의할 필요가 없는 경우가 많다.

<br>

## `map(function, iterable)`
주어진 iterable의 item을 돌면서 function을 모두 실행한다.
```python
>>> list(map(lambda x: x*2, [1,2,3,4,5]))
[2, 4, 6, 8, 10]
```

## `filter(function, iterable)`
iterable에서 function의 조건에 맞는 것들만 새로운 리스트에 저장한다.
```python
>>> list(filter(lambda x: x%2==0, [1,2,3,4,5]))
[2, 4]
```

## `reduce(function, sequence)`
*sequence: int 타입 인덱스를 통해, 원소에 접근할 수 있는 iterable 입니다. iterable의 하위 카테고리라고 생각하시면 됩니다. list, str, tuple이 여기 속합니다. ( dictionary는 다양한 타입을 통해 원소에 접근할 수 있기 때문에 sequence에 속하지 않습니다.*
<br>

가장 처음에 sequence에 있는 두 개의 요소를 함수에 적용한 후, 그 결과 값과 sequence에서의 그 다음 값(처음 두 개의 값 이후)을 다시 함수에 적용하는 것을 반복한다.
```python
reduce(lambda x,y: x+y, [1,2,3,4,5])
```
1. 1+2
2. 3(1+2) + 3
3. 6(3+3) + 4
4. 10(6+4) + 5
= 15

---

### Reference
- [map(), filter(), and reduce() in Python with Examples](https://stackabuse.com/map-filter-and-reduce-in-python-with-examples)
- [프로그래머스 - 파이썬을 파이썬답게](https://programmers.co.kr/learn/courses/4008/lessons/13171)
