## in을 사용하고 딕셔너리 키가 없을때 KeyError를 처리하기보다는 get을 사용하라
```python
fruits = {
  'red': ['apple', 'cherry'],
  'yellow': ['banana']
}

color = 'pink'
fruit = 'peach'

try:
  pink_fruit = fruits[color]
except KeyError:
  fruits[color] = pink_fruits = []

pink_fruits.append(fruit)

print(fruits)
>>>{'red': ['apple', 'cherry'], 'yellow': ['banana'], 'pink': ['peach']}
```

### Better way: `get()`
```python
pink_fruits = fruits.get(color)
if pink_fruits is None:
  fruits[color] = pink_fruits = []

pink_fruits.append(fruit)
print(fruits)
>>>{'red': ['apple', 'cherry'], 'yellow': ['banana'], 'pink': ['peach']}
```

### Simpler way: `setdefault()`
```python
print(fruits)
>>>{'red': ['apple', 'cherry'], 'yellow': ['banana']}
pink_fruits = fruits.setdefault(color, [])
print(pink_fruits)
>>{'red': ['apple', 'cherry'], 'yellow': ['banana']}
print(fruits)
>>{'red': ['apple', 'cherry'], 'yellow': ['banana'], 'pink': []}

pink_fruits.append(fruit)
print(pink_fruits)
>>>['peach']
print(fruits)
>>>{'red': ['apple', 'cherry'], 'yellow': ['banana'], 'pink': ['peach']}

red_fruits = fruits.setdefault('red', [])
print(red_fruits)
>>>['apple', 'cherry']
print(fruits)
>>>{'red': ['apple', 'cherry'], 'yellow': ['banana'], 'pink': ['peach']}
## key가 있는 경우에는 변경되지 않는다.

fruits.setdefault('apricot', pink_fruits)
print(fruits)
>>>{'red': ['apple', 'cherry'], 'yellow': ['banana'], 'pink': ['peach'], 'apricot': ['peach']}

pink_fruits.append('not_pink')
print(fruits)
>>>{'red': ['apple', 'cherry'], 'yellow': ['banana'], 'pink': ['peach', 'not_pink'], 'apricot': ['peach', 'not_pink']}
```
- setdefult에 전달된 디폴트 값이 별도로 복사되지 않고 딕셔너리에 **직접 대입**된다.
- 이는 키에 해당하는 디폴트 값을 setdefult에 전달할때마다 그 값을 새로 만들어야 한다는 뜻이다.
- 즉 호출할 때 마다 리스트를 만들어야 하므로 성능이 크게 저하될 수 있다. 
- 만약 가독성과 효율성을 향상시키고자 디폴트 값에 사용하는 객체를 재활용한다면 이상한 동작을 하게되고 버그가 발생할 것이다.
  -> `pink`, `apricot`의 경우
- `fruits.setdefault(color, []).append(fruit)`로 더 간단하게 쓸 수도 있다.
- 
## 내부 상태에서 원소가 없는 경우를 처리할 때는 setdefult보다 defaultdict를 사용하라
### setdefault
```python
class Fruits:
  def __init__(self):
    self.data = fruits

  def add(self, color, fruit):
    fruit_set = self.data.setdefault(color, [])
    print(id(fruit_set))
    fruit_set.append(fruit)

fruits = Fruits()
fruits.add('orange', 'orange')
print(fruits.data)
>>>140233721929088
>>>{'red': ['apple', 'cherry'], 'yellow': ['banana'], 'orange': ['orange']}

fruits.add('yellow', 'pineapple')
print(fruits.data)
>>>140233721796224
>>>{'red': ['apple', 'cherry'], 'yellow': ['banana', 'pineapple'], 'orange': ['orange']}
```
- 주어진 색이 딕셔너리에 있든 없든 관계없이 호출할때마다 새로 인스턴스를 만들기때문에 효율적이지 않다


### defaultdict
```python
from collections import defaultdict

class Fruits:
  def __init__(self):
    self.data = defaultdict(list)

  def add(self, color, fruit):
    self.data[color].append(fruit)

fruits = Fruits()
fruits.add('orange', 'orange')
print(fruits.data)
>>>defaultdict(<class 'list'>, {'orange': ['orange']})

fruits.add('yellow', 'pineapple')
print(fruits.data)
>>>defaultdict(<class 'list'>, {'orange': ['orange'], 'yellow': ['pineapple']})
```
- `add` 코드는 data 딕셔너리에 있는 키에 접근하면 항상 기존 인스턴스가 반환된다.


---
### Reference
- 파이썬 코딩의 기술(Effective Python)
