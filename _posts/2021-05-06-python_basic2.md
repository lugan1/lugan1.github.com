---
title: "[Python] 기본 문법 정리 (2)"
tags:
- python
categories:
- python
- 코딩테스트
date: '2021-05-06 13:29:57 +0900'
classes: wide
last_modified_at: '2021-09-10 15:13:01 +0900'
---

얼마전 인터넷으로 '이것이 취업을 위한 코딩테스트다' 서적을 구매해서 공부한거 정리


# 1. 자료형
<br>

## 1.1 실수형 변수 선언

**(0생략, 간소화 선언 방법)**
<br>ex)
```python
a = 2.
# 2.0

a = -.7
# -0.7
```
<br>

**지수표현방식 이용 (e)**
<br>ex)
```python
a = 1e9
#1000000000.0 (정수부분 0갯수 9개, 1e^9-> 1*10^9)

a = 75.25e1
#752.5 (75.25*10^1)
#e가 양수일경우 : 오른쪽(->)으로 점 n번이동

a = 3954e-3
#3.954
#e가 음수일경우 : 왼쪽(<-)으로 점 n번 이동
```
<br>

**round() 함수**

- 보통의 컴퓨터 시스템에서는 실수 처리시 Floating-point(부동소수점) 방식을 이용하고, 실수형 저장시에 4 byte 혹은 8 byte 메모리를 할당해서 실수 표현시에 정확도가 떨어짐

- 0.3 + 0.6 = 0.899999999999999 로 저장이됨. 2진수에서는 0.9를 정확히 표현할수 있는 방법이 없기 때문에 오차발생.

- 때문에 round() 함수를 이용해서 반올림을 해주어야함.

ex)
```python
a = 0.3 + 0.6
print(round(a, 4))
# 0.9
# round(반올림할 값, 반올림할 자리수-1)
```
<br>

**수 자료형 연산**
```python
a = 7
b = 3

# 나머지 연산
c = a % b     #결과 : c->1

# 몫
c = a // b    #결과 : c->2

# 거듭제곱 연산
c = a ** b    #결과 : c-> 343 (7^3)
```
<br><br>


## 1.2 리스트 자료형

**리스트 선언**
<br>
ex)
```python
a = [1, 2, 3, 4, 5, 6, 7, 8, 9]
print(a[4]) #결과 : 5

#빈 리스트 선언 방법1
a = list()

#빈 리스트 선언 방법2
a = []

#뒤에서 첫번째 원소 출력
print(a[-1]) #결과 : 9

#뒤에서 세 번재 원소 출력
print(a[-3]) #결과 : 7

#두 번째 원소부터 네 번째 원소까지 출력 (슬라이싱)
print(a[1 : 4]) #결과 : [2, 3, 4]
#[시작 : 끝 인덱스-1]
```

<br>

**리스트 컴프리헨션**
- 대괄호 안에 조건문과 반복문을 넣어서 리스트를 초기화 하는 방법
- [넣을변수(변수이용 식도 가능), 반복문or조건문]
- [i\*i .... 반복문... 조건문] -> append(i*i)

ex)
```python
# 0부터 19까지의 수 중에서 홀수만 포함하는 리스트

# 방법1 (리스트 컴프리헨션 이용)
array = [i for in range(20) if i % 2 == 1]
#1, 3, 5, 7, 9, 11, 13, 15, 17, 19

# 방법2
array = []
    for i in range(20):
        if i % 2 == 1:
            array.append(i)
#1, 3, 5, 7, 9, 11, 13, 15, 17, 19


# 1부터 9까지의 수의 제곱 값을 포함하는 리스트
array = [i * i for i in range(1, 10)]
#ragne() 함수 -> ragne(시작값, 끝 값+1)

# N * M 크기의 2차원 리스트 초기화
n = 4
m = 4
list = [[0] * m for _ in range(n)]
# list = [value]*n -> 크기가 n인 리스트 초기화 방법
# 반복문에서 _ 역할 -> for _ in range(5) 처럼 변수 필요없을때, 즉 더미 변수 사용하고 싶을때 씀

print(list)
#[[0, 0, 0, 0,], [0, 0, 0, 0], [0, 0, 0, 0], [0, 0, 0, 0]]


# 리스트 컴프리헨션 사용하지 않고 N * M 2차원 리스트 초기화 (같은 참조값을 갖음)
list = [[0] * m] * n

print(list)
#[[0, 0, 0, 0,], [0, 0, 0, 0], [0, 0, 0, 0], [0, 0, 0, 0]]

arra[1][1] = 5
print(array)
# [[0, 5, 0, 0,], [0, 5, 0, 0], [0,5, 0, 0], [0, 5, 0, 0]]
# 3개의 리스트가 같은 참조 주소값을 가져서 셋다 동시에 바뀜
```
<br>

**리스트 관련 함수**

|함수명|설명|시간 복잡도|
|:------:|:---:|:---:|
|append()|리스트 끝에 원소삽입|O(1)|
|reverse()|리스트의 원소 순서 뒤집음|O(N)|
|insert()|특정 위치에 원소 삽입 (*append 보다 느림)|O(N)|
|remove()|특정값 원소 제거, 여러개 중복시 하나만 제거|O(N)|

<br>

**\*특정값의 원소를 리스트에서 모두 제거하려면 따로 코드상으로 구현해야된다. remove_all()같은 함수가 없음.**

ex)
```python
list = [1, 2, 3, 4, 5, 6, 7]
remove = {4, 6}

# remove_set에 포함되지 않은 값만을 저장
# i는 for i in list 인데, i가 remove 에 포함되지 않을때 append(i)
result = [i for i in list if i not in remove]
#result -> [1, 2, 3, 5, 7]
```
<br><br>


## 1.3 문자열


ex)
```python
#이스케이프 문자 \ 사용 (큰따음표 ""기입가능)
string = "\"python\""
print(string)
# "python"

string = "test"
print(string *3)
# testtesttest

a = "ABCDEF"
print(a[2 : 4])
# CD
# index 2~3 까지 출력
```
<br><br>


## 1.4 튜플

- 한번 선언되면 값 변경 불가
- 소괄호 사용. ( )

ex)
```python
tuple = (1, 2, 3, 4, 5)
print(tuple)

tuple[1] = 4
#값 변경시 컴파일 에러 (한번 값 설정하면 변경불가)
```

<br><br>



## 1.5 사전

- key, value 쌍으로 데이터를 가지는 자료형.
- 변경 불가능한 값을 key 값으로 사용 가능함.
- 해시 테이블(Hash Table)을 사용함.
- 시간복잡도는 O(1)

ex)
```python
num = dict()
num["one"] = 1
num["two"] = 2
num["three"] = 3
# num -> {'one' : 1, 'two' : 2, 'three' : 3}

# in 문법. (iterable 자료형 모두 사용가능)
# iterable 자료형 -> 리스트, 문자열, 튜플, 사전
if 'one' in num :
    print("true")
# 해당 key 값을 갖은 데이터가 존재하는지 확인

print(num.keys())
# dict_keys(['one', 'two', 'three'])
# keys()함수 -> key값만 뽑아옴

print(num.values())
# dict_values(['1', '2', '3'])
# values()함수 -> value 값만 뽑아옴
```

## 1.6 집합 (수학에서 말하는 집합 자료형)
- 중복값 허용 x (중복값으로 선언해도 하나의 값만 들어간다.)
- 순서 x
- 특정 원소가 존재하는지 확인하는 연산의 시간복잡도는 O(1)
- 주로 특정한 데이터가 이미 등장한 적이 있는지 여부를 확인하기 위해서 사용

ex)
```python
#집합 자료형 초기화 방법 1
data = set([1, 1, 2, 3, 4, 4, 5])
print(data) #{1, 2, 3, 4, 5}

#집합 자료형 초기화 방법 2
data = {1, 1, 2, 3, 4, 4, 5}
print(data) #{1, 2, 3, 4, 5}


#집합 자료형 연산
a = set([1, 2, 3, 4, 5])
b = set([3, 4, 5, 6, 7])

print(a : b) #합집합 {1, 2, 3, 4, 5, 6, 7}
print(a & b) #교집합 {3, 4, 5}
print(a - b) #차집합 {1, 2}

#집합 자료형 관련 함수
#add() - 원소 추가
#update() - 원소 여러개 추가
#remove() - 특정값 원소 삭제

a.add(6) #{1,2,3,4,5,6}
a.remove(6) #{1,2,3,4,5}
a.update(7,8) #{1,2,3,4,5,7,8}
```

<br>

# 2. 조건문 (생략)
- x in 리스트 (리스트에 x가 포함되면 TRUE)
- x not in 리스트 (리스트에 x가 포함되지 않으면 TRUE)
- 조건부 표현식 (result = "Success" if score >= 80)
- 부동식 사용 
<br>if 0 < x < 30:
<br>print ("x는 0 초과, 30미만의 숫자");
<br>
<br>
<br>

# 3. 반복문 (생략)
- continue (반복문의 처음으로 돌아감)
<br>
<br>
<br>
<br>

# 4. 함수
함수 작성 예시
```python
def 함수명(매개변수):
    실행할 소스코드
    return 반환 값


def add(a, b):
    print('함수의 결과:', a+b)

add(b=3, a=3)


#함수 안에서 global 키워드 사용시에 지역변수가 만들어지지 않고 함수 바깥 변수를 참조하게 됨

a = 0

def func():
    global a
    a += 1

for i in range(10):
    func()

print(a) #10

#람다 표현식사용
print((lambda a, b: a + b)(3, 7)) #10
```
<br>
<br>
<br>

# 5. 입출력

## 5.1 입력 input()
- 입력받은 문자열을 띄어쓰기로 구분하여 각각 숫자 자료형으로 리스트에 저장하는 방법
- input() 을 이용하여 입력받음
- split() 을 이용하여 공백으로 나뉘는 리스트로 변환
- map() 을 이용하여 해당 리스트의 모든 원소에 int() 함수 적용
- list() 를 이용하여 각각의 숫자 자료형을 리스트에 저장


```python
# 첫번째 입력은 데이터의 갯수
# 두번째 입력은 학생 성적을 받아서
# 내림차순으로 출력하는 예시

# 데이터의 갯수 입력
n = int(intput())

# 각 데이터를 공백으로 구분하여 입력
data = list(map(int, input().split()))

data.sort(reverse = True)

print(data)


# n, m, k를 공백으로 구분하여 입력
n, m, k = map(int input().split())
#3, 5, 7 입력


print(n, m, k) #3, 5, 7
```
<br>

- 입력의 갯수가 많을 경우에는 sys.stdin.readline() 함수 사용

- 입력후 엔터키가 줄바꿈 기호로 입력되기 때문에 rstrip() 함수를 이용해서 공백 문자를 제거해야됨
<br>
<br>
```python
import sys

# 문자열 입력
data = sys.stdin.readline().rstrip()
print(data)
```
<br>
<br>

## 5.2 출력 print()
- int형 변수 + 문자열 하면 에러 발생
<br> ex) print("구입하신 항목은" + number + "개 입니다.")

- str() 함수를 이용하여 츨력하고자 하는 변수를 문자형으로 형변환 해야됨.
<br> ex) print("구입하신 항목은" + str(number) + "개 입니다.")
- 혹은 컴마(,) 로 변수를 구분해줘야 됨  
ex) print("구입하신 항목은", number , "개 입니다.")
<br>
- f-string 문법 사용시 간편하게 변수 출력가능 (f와 중괄호 {} 로 표현)
<br> ex) print(f"구입하신 항목은 {number} 입니다.")

