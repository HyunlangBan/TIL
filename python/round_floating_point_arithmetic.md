## Round
```python
>>> round(1.2)
1
>>> round(1.7)
2
>>> round(1.5)
2
>>> round(2.5)
2
>>> round(3.5)
4
```
python3에서 `round()`를 쓰면 해당 소수와 가장 가까운 정수를 반환한다. 하지만 x.5에서는 가장 가까운 정수와의 거리가 양쪽으로 동일한데 python3에서는 Ties to nearest even 방식으로 가장 가까운 짝수가 반환된다.

python2에서는 Ties away from zero 방식으로 우리가 가장 많이 알고있는 반올림 방식이다. 버전에 따라 반올림 방식이 다름에 주의하자.
```python
>>> round(1.5)
2.0
>>> round(2.5)
3.0
>>> round(3.5)
4.0
```
이렇게 반올림 방식이 다른 것은 실수를 컴퓨터상에서 근사하여 표현하는 부동소수점 때문이다. 원하는 숫자를 정확하게 표현하고 싶다면 고정소수점인 `Decimal`을 사용하자.

### 부동소수점
```python
>>> 0.3 == 0.1 + 0.1 + 0.1
False
```

### 고정소수점
```python
>>> from decimal import Decimal
>>> Decimal("0.3") == Decimal("0.1") + Decimal("0.1") + Decimal("0.1")
True
```
