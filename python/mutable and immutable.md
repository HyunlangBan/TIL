[인프런](https://www.inflearn.com/course/%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D-%ED%8C%8C%EC%9D%B4%EC%8D%AC-%EC%A4%91%EA%B8%89-%EC%9D%B8%ED%94%84%EB%9F%B0-%EC%98%A4%EB%A6%AC%EC%A7%80%EB%84%90/dashboard)에서 클로저를 공부하다가 mutable, immutable 변수에 대해 궁금증이 생겼다.

### Closure Example 1
```python
def clousre_ex1():
	series = []
	def averager(v):
		sereis.append(v)
		return sum(series)/len(series)
	return averager
```

### Closure Example 2
```python
def closure_ex2():
	cnt = 0
	total = 0

	def averager(v):
		cnt += 1
		total += v
		return total/cnt
	return averager

avg_clo2 = closure_ex2()
print(avg_clo2(10))
# error: local variable 'cnt' referenced before assignment
```

예시 1번은 inner function에서 `series`를 잘 찾는데, 왜 예시 2번에서는 바로 위에 있는 `cnt`, `total`을 찾지 못하는 걸까? 
그 이유는 list는 mutable하고 int는 immutable하기 때문이다.
<br>

## Mutable
- 수정 가능한 객체. local scope 밖에서 변경 가능하다.
- list, dict

## Immutable
- 수정 불가능한 객체. local scope 밖에서 변경할 수 없다.
- int, float, str, tuple
<br>
=> 즉 immutable한 변수는 읽을 수만 있고 값을 갱신할 수는 없으므로 예시 2번에서 에러가 발생한다.
<br>

`전문가를 위한 파이썬`에는 다음과 같이 설명되어 있다.

```
불변형은 읽을수만 있고 값을 갱신할 수 없다. count = count+1 과 같은 문장으로 변수를 다시 바인딩하면 암묵적으로 count라는 지역 변수를 만든다. 
count가 더이상 자유변수가 아니므로 클로저에 저장되지 않는다.
nonlocal은 변수에 새로운 값을 할당하더라도 그 변수는 자유 변수임을 나타낸다.
```
*[자유변수](https://zetawiki.com/wiki/%ED%8C%8C%EC%9D%B4%EC%8D%AC_%EC%9E%90%EC%9C%A0%EB%B3%80%EC%88%98): 어떤 코드블록 안에서 사용되지만, 글로벌 변수도 아니고 그 블록 내에 정의하지도 않은 변수
