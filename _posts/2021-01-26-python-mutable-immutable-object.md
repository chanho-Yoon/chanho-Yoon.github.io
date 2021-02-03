---
title: '파이썬 가변 객체와 불변 객체'
excerpt: 'python에서 가변(mutable) 객체와 불변(immutable) 객체에 대해 알아보겠습니다.' 
categories: [python]
tags: [파이썬 가변 객체, 파이썬 불변 객체]
last_modified_at: 2021-01-26T01:18:00-19:00
toc: true 
toc_label: '목차'
sitemap :
  changefreq : daily
  priority : 1.0
---

## 1. 객체

파이썬의 모든 데이터 타입들은 객체(Object)로 객체 단위로 메모리 상에서 정보를 관리합니다.

### 1.1 객체의 3가지의 특성

- 값(value) : 메모리에 기록된 내용, 가변 객체는 값 변경(o) 불변 객체는 값의 변경(x)
- 유형(type) : 객체의 유형
- 정체성(identity) : 각각의 객체를 식별하기 위한 **id** 고유번호(메모리 상에 위치한 주소 값)를 말합니다.

## 2. 가변 객체와 불변 객체

### 2.1 가변, 불변 객체 종류

| 가변 객체  | 불변 객체          |
| :------------------------: | :-------------: |
| list,set,dict | int, float, bool, tuple, string, unicode |

### 2.2 가변 객체와 불변 객체의 차이

가변 객체와 불변 객체의 가장 큰 차이점은 불변성입니다. <br>
불변 객체는 말 그대로 <span style="color:orange">메모리에 위치하는 불변 객체의 값을 수정할 수 없다는 것</span> 입니다.
즉 불변 객체는 생성될 때 그 값이 결정된다고 보면 됩니다.

```python
tuple1 = (3,4,5)
tuple1[1] = 3
```

```
----------------------------------------------------------------------
TypeError                            Traceback (most recent call last)
<ipython-input-2-5993a3ad4be5> in <module>
      1 tuple1 = (3,4,5)
----> 2 tuple1[1] = 3;

TypeError: 'tuple' object does not support item assignment
```

튜플 자료형은 불변형 객체이므로 내용을 수정할 수 없습니다. 

<br>

```python
a = (3,4)
a = (5,6)
```
```
5,6
```

튜플은 불변형 객체라서 값의 변경이 안되는데 값이 바뀌었습니다. 하지만 이것은 값을 바꾼게 아닌 새로운 불변형 객체를 재정의 한거기 때문에
값을 변경했다고 볼 수 없습니다. 그러므로 정상작동 합니다. 그것을 확인 하려면 id값을 확인해보면 됩니다.

```python
a = (3,4)
print(id(a))
a = (5,6)
print(id(a))
```

```
4359004096
4359003456
```

id값이 바뀌었습니다. 이것은 무엇을 뜻하는 걸까요?? <br>
기존에 3,4 를 가지고 있는 a 변수를 가리키는 레퍼런스 값이 기존 3,4 -> 5,6 으로 레퍼런스가 참조하는 값이 바뀐게 아닌 a를 재정의함으로써 새로운 레퍼런스 값을 가지고 있습니다.
<br>

### 2.3. 불변성 객체인 튜플안에 리스트 값을 변경할 수 있을까?

됩니다!

```python
li = [10,20,30]
a = (1,2,li)

print(a)
print('tuple id : %d' %id(a))
print('list id : %d' %id(a[2]))
a[2][0] = 100
print(a)
print('tuple id : %d' %id(a))
print('list id : %d' %id(a[2]))
```

```
(1, 2, [10, 20, 30])
tuple id : 4358989568
list id : 4359066944
(1, 2, [100, 20, 30])
tuple id : 4358989568
list id : 4359066944
```

위와 같이 튜플은 불변성으로 안의 값을 변경하지 못하지만 위의 코드에선 **튜플이 리스트에 대한 참조만을 가지고 있기 때문**입니다. <br>
조금 더 쉽게 설명하자면 튜플은 리스트의 **참조(reference)값**만 가지고 있고 이 리스트의 참조(reference) 값이 바뀌지 않는 이상 튜플 입장에선 불변성을 유지하고 있는 것 입니다. <br>

아래 와 같이 새로운 리스트를 튜플에 넣을려고 할 경우엔 에러가 나는 이유도 그 때문입니다.

```python
li = [10,20,30]
a = (1,2,li)
li2 = [100,200,300]

print(a)
print('tuple id : %d' %id(a))
print('list id : %d' %id(a[2]))
a[2] = li2
print(a)
print('tuple id : %d' %id(a))
print('list id : %d' %id(a[2]))
```

위와 같이 기존 튜플에 새로운 리스트를 넣을려고하면 기존에 있던 튜플 리스트의 참조값이 바뀌게 되므로 이것은 불변성을 어기는 행동이 됩니다.

---

**참고** <br>
[Under The Pencil](https://elvanov.com/599){:target="\_blank"} <br>
[훈훈훈](https://wave1994.tistory.com/40){:target="\_blank"} <br>


