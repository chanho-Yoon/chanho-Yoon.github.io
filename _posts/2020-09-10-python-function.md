---
title: '파이썬 함수'
excerpt: '파이썬 함수에 대해 공부하겠습니다.'
categories: [Python]
tags: [Python Function, 파이썬 함수]
last_modified_at: 2020-09-10T01:15:00-16:00
toc: true
toc_label: '목차'
---

## 함수?

<img src='/assets/images/functionImg.png' alt='profile' style="width:600px; margin-top:15px; margin-bottom:15px; box-shadow: rgba(50, 50, 93, 0.25) 0px 13px 27px -5px, rgba(0, 0, 0, 0.3) 0px 8px 16px -8px, rgba(0, 0, 0, 0.024) 0px -6px 16px -6px;"/>

프로그래밍에선 함수란 어떠한 입력 받은 값을 가지고 어떠한 일을 수행해서 거기에 맞는 결과값을 산출해내는 것 입니다. <br>

### 함수를 사용하는 이유

프로그래밍을 하다보면 중복된 내용을 작성할 때가 있습니다. 만약 한 학생의 점수 총합을 구해야 하는데 100명의 학생들이 있다고 했을때
각각의 학생들의 점수들을 일일히 더하는 것보다 점수만 입력받고 총합을 반환하는 함수를 만들면 중복된 코드가 발생하지 않고 간편하게 구할 수 있습니다. <br>
또한 언제든 만들어놓은 함수를 재사용할 수 있습니다.

```python
student1Total = 60 + 30 + 50
student2Total = 70 + 55 + 80
student3Total = 77 + 50 + 60

def sum(국어,영어,수학):
  return 국어+영어+수학

student1Total = sum(60,30,50)
student2Total = sum(70,55,80)
student3Total = sum(77,50,60)
```

### 파이썬 함수의 사용

```python
def 함수명(매개변수):
  ...
  return
```

파이썬에서 함수를 사용할 때에는 `def`를 사용해서 만들고 이어 **함수이름** 그리고 안에 **매개변수**를 받습니다. <br>
예제로 간단하게 곱셈 결과를 반환하는 함수를 만들어보겠습니다.

```python
def multiple(x,y): # 매개변수로 받은 x,y값을 곱해서 반환
  return x*y

a=3
b=4
multipleResult=multiple(a,b) # 인수로 a,b 값을 전달 합니다.
print(multipleResult)
```

### 매개변수, 인수 차이

언뜻 보면 비슷하지만 어디서 사용하느냐에 따라 용어가 틀리므로 기억해야합니다.

- **매개변수**<br>
  매개변수는 함수에서 전달받는 변수를 **"매개변수"**라고 부릅니다.

- **인수**<br>
  인수는 `multipleResult=multiple(a,b)`와 같이 함수에 전달하는 변수를 **"인수"**라고 부릅니다

## 다양한 함수의 형태

### 입력값과 반환값이 있는 함수

```python
def add(a,b):
  return a+b
```

### 입력값이 있고 반환값이 없는 함수

```python
def printSum(a,b):
  print("%d + %d = %d" % (a,b,(a+b))
```

### 입력값이 없고 반환값이 있는 함수

```python
def hello():
  return 'Hello World'
```

### 입력값과 반환값이 없는 함수

```python
def hello():
  print('Hellow World')
```

## 매개변수

### 매개변수 지정

일반적으로 함수에 인수값을 전달할 때에는 순서대로 매개변수에 값이 전달됩니다. 하지만 인수로 전달할 때 매개변수 이름을 직접 지정하여 값을 전달할 수도 있습니다.

```python
def sub(x,y):
  return x-y

print(sub(x=5, y=2))
print(sub(y=5, x=2))
# result
3
3
```

### 매개변수에 초깃값 지정

함수에 전달 받는 값인 매개변수는 일반적으로 인수로 전달된 값을 받지만, 초깃값을 미리 설정하여 해당 매개변수로 값이 들어오지 않았을 경우에 초깃값을 사용할 수 있게 만들 수 있습니다.

```python
def sub(x,y=77):
  return x-y

print(sub(x=5, y=2))
print(sub(x=2))
# result
3
-75
```

## 가변 매개변수

만약 함수를 작성하는데 매개변수로 들어올 값들을 모르겠다면 **가변 매개변수**를 사용하여 해결가능합니다.

### 가변 매개변수 사용

```python
def 함수명 (매개변수1, 매개변수2,...*가변 매개변수):
  ...
```

- <span style="color:red">주의사항</span>
  1. 가변 매개변수 뒤로는 일반적인 매개변수가 올 수 없습니다.
  2. 가변 매개변수는 단 하나만 사용이 가능합니다.

```python
def multiple(a, *data):  # 가변인자를 받는데 처음 받는 매개변수 a * 가변 매개변수
    for i in data:
        print(a * i, end=' ')

multiple(3, 1, 2, 3, 4, 5)
print()
multiple(5, 1, 2, 3)
# result
3 6 9 12 15
5 10 15
```

## 함수의 리턴값은 하나

함수의 리턴값은 절대적으로 하나입니다.

### 리턴값 예제

```python
def sub(x, y):
    return x-y
    return x+y


print(sub(x=5, y=2))
#result
3
```

이와 같이 되는 이유는 함수는 `return`을 하게될 경우 값을 반환하고 함수를 종료하게 됩니다. 즉 `x-y`의 값을 반환하고 sub 함수를 종료해버립니다. 이러한 특성을 이용해 `return` 다양하게 사용할 수 있습니다.

### return을 활용한 예제

앞서 설명드린 것과 같이 `return`을 사용하여 특별한 상황일 때 함수를 빠져나올 수 있습니다.<br>
많은 예시가 있지만 함수안에 반복문을 빠져나오는 것을 해보겠습니다.

```python
def multiple(x, *data):
    result = 0
    for n in data:
        result = x*n
        if result >= 20:
            return print('result 값( %d )가 20보다 크거나 같기 때문에 함수를 종료합니다' % (result))
    return print('result 값 : %d ' % (result))

multiple(5, 1, 2, 3, 4, 5, 6)
# result
result 값( 20 )가 20보다 크거나 같기 때문에 함수를 종료합니다
```

보면 "아니 함수에서는 `return`값이 무조건 하나라고 하지 않았나요??" 라고 하실 수도 있지만 구조상 보면 결국 return 값은 하나 입니다.
result값이 20이상이 된 경우와 아닌 경우 결국 하나의 `return`값만을 반환하게 됩니다.<br>
결과를 보면 result 값이 20 이상이기 때문에 `return print('result 값 : %d ' % (result))` 이 문장이 실행 되지 않는 것을 볼 수 있습니다.

> [점프투파이썬](https://wikidocs.net/24)<br>[림코딩](https://devpouch.tistory.com/82)
