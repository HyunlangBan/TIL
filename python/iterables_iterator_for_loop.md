# Iterable
iterable은 iteration에서 사용될 수 있는 객체이다. 만약 어떠한 객체가 iterable이라면 python의 built-iin function인 `iter()`을 통과하여 iterator를 리턴한다.
iterable을 직접 만드는 것을 보면 더 이해가 쉽다.
```python
class Iterable(object):

    def __init__(self,values):
        self.values = values
        self.location = 0

    def __iter__(self):
        return self

    def next(self):
        if self.location == len(self.values):
            raise StopIteration
        value = self.values[self.location]
        self.location += 1
        return value
```

# Iterator
`iter()`로 interator를 얻은 후에는 어떻게 할까?
iterator는 iterable 객체로부터 연속된 값들을 yield(return과는 다르므로 yield를 그대로 쓰겠다)한다. built-in function인 `next()`로 iterator의 다음 값을 얻을 수 있다.
```python
>>> list_a = ['hello', 'world', 'python'] # define iterables
>>> itr = iter(list_a) # get iterator
>>> itr
<list_iterator object at 0x7f95db362550>
>>> next(itr) # yield values
'hello'
>>> next(itr)
'world'
>>> next(itr)
'python'
```
# How for loop works
![t ba63222d63f5](https://user-images.githubusercontent.com/45524783/118516030-e9b36380-b770-11eb-8086-7bf0ac36106a.png)
- iterator를 얻기 위해 `iter()`를 호출한다.
- iterator에서 각 값들을 얻기 위해서 `next()`를 반복적으로 호출한다.
- `next()`에서 `StopIteration` exception이 발생하면 loop를 종료한다.

그러니까 정리하자면 우리가 for문에서 사용하는 list나 dictionary등은 iterables로 `iter()`, `next()`를 기본적으로 내포하고 있으며 for문을 사용할때 iterable에 있는 iter을 호출하여 iterator를 리턴하고, next를 호출하면서 각 값들을 불러올 수 있던 것이었다.

## 출처
- https://realpython.com/python-for-loop/
- https://wiki.python.org/moin/ForLoop
