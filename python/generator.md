## Generator
- A function which returns an iterator
```python
>>> def generator(list_a):
...     for i in list_a:
...          yield i
>>> x = generator([1,2,3,4,5])
>>> x
<generator object gen at 0x1035fe9e8>
```

### Iterator
- an object that contains a countable number of elements that can be iterated upon. -> [iterable](https://github.com/HyunlangBan/TIL/blob/main/python/iterables_iterator_for_loop.md#iterable)한 객체

## Generator vs. List
```python
>>> generator = (i for i in range(5))
>>> list = [i for i in range(5)]
>>> generator
<generator object <genexpr> at 0x100c9c9e8>
>>> next(generator)
0
>>> next(generator)
1
>>> next(generator)
2
>>> next(generator)
3
>>> next(generator)
4
>>> next(generator)
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
StopIteration
>>> list
[0, 1, 2, 3, 4]
```
- 제너레이터는 `next()`를 실행할때마다 yield에 있는 값을 return하고 그 부분에서 멈춘다. 그리고 다음 `next()`를 호출하면 멈춘 부분에서 다시 시작한다.
- 리스트는 모든 요소를 한꺼번에 리턴한다.         

=> 이러한 제너레이터의 특성은 반복할 데이터의 양이 많을때 메모리를 한꺼번에 할당하는 것이 아니라 한번에 element 하나씩에 대해서만 사용할 수 있게 한다.

## Concurrency
- 병행성이라고 하며 여러 일을 동시에 처리할 수 있는 것
  - 여기서 동시에는 정말 "동시"에 모든 일을 한다는 것이 아니라 내가 아침에 일어나서 자기 전까지 하나의 일만 하는 것이 아니라 양치도 하고, 커피도 마시고, 밥도 먹고, 일도 하고 이런 식으로 여러 가지 일을 처리할 수 있음을 의미한다.
  - 즉, 싱글 스레드에서 여러가지 작업을 처리하는 것을 병행성이라고 한다.
  - generator의 yield가 이를 가능하게 해준다.
- Parallelism과 반대되는 말이다.
  - 병렬성(parallelism)은 각기 다른 worker가 각각 하나의 일을 도맡아서 동시에 수행하는 것이다.

### Coroutines
![image](https://user-images.githubusercontent.com/45524783/147057067-f47916ec-7be6-4ef9-a9ab-145ad54e5d3a.png)
- 위에서 말한 제너레이터, 병행성에 비동기의 특성까지 합쳐진 개념이다.
- yield, send를 사용하여 메인과 서브 루틴이 양방향으로 통신, 비동기(여러 일을 동시에 실행가능)로 실행되며 병행성을 가진다.
  - 메인 루틴에서는 send로 서브 루틴에 데이터를 보내고, 서브 루틴에서는 yield로 흐름제어와 데이터 전송을 한다.
- 코루틴의 장점은 멀티 스레드가 아니기에 context switching이 발생하지 않아서 오버헤드가 적다는 것이다.
```python
# 서브루틴
def coroutine1():
	print('coroutine started')
	i = yield
	print('coroutine recieved: {}'.format(i))

# 메인 루틴
cr1 = coroutine1()

# 값 전송
next(cr1)
>> coroutine started
cr1.send(100)  # yield를 통해서 데이터 전송 가능 + 다음 지점으로 이동 
               # => 메인과 서브 루틴에서 서로 데이터 교환이 가능해짐
>> coroutine recieved: 100
```

----
### 참고
- https://www.youtube.com/watch?v=c6uoxhaenHg
- https://www.youtube.com/watch?v=bD05uGo_sVI
- https://www.inflearn.com/course/%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D-%ED%8C%8C%EC%9D%B4%EC%8D%AC-%EC%A4%91%EA%B8%89-%EC%9D%B8%ED%94%84%EB%9F%B0-%EC%98%A4%EB%A6%AC%EC%A7%80%EB%84%90/lecture/28634?tab=note&speed=1.75
