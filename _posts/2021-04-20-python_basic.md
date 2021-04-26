---
title: "[Python] 기본 문법 정리"
classes : wide
tags:
- python
categories:
- python
---

<https://wikidocs.net/book/1>

사이트를 참조해서 공부한거를 정리한다.

### 파이썬 기본 특징
------------------------------------------------------------------------------

- **세미콜론 (;) 사용안함.**

- **중괄호 ({) 사용안함.** 들여쓰기로 판별함.

- 함수선언은** def name(arg) :** 형식으로 함. **리턴타입 명시 안해도됨.**

- 변수 선언시 **자료형 명시 안해도됨.**

- 외부파일 사용시 **form 모듈 import 이름**. 혹은 **import 모듈** 로 외부 메소드 실행한다. 전체를 가져올려면 이름에 \*를 사용한다.


<br>
<br>


### 반복문
---------------------------------------------------------------------------


**for 문**

ex)

<div class="colorscripter-code" style="color:#010101;font-family:Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; position:relative !important;overflow:auto"><table class="colorscripter-code-table" style="margin:0;padding:0;border:none;background-color:#fafafa;border-radius:4px;" cellspacing="0" cellpadding="0"><tr><td style="padding:6px 0;text-align:left"><div style="margin:0;padding:0;color:#010101;font-family:Consolas, 'Liberation Mono', Menlo, Courier, monospace !important;line-height:130%"><div style="padding:0 6px; white-space:pre; line-height:130%">family&nbsp;<span style="color:#0086b3"></span><span style="color:#a71d5d">=</span>&nbsp;[<span style="color:#63a35c">'mother'</span>,&nbsp;<span style="color:#63a35c">'father'</span>,&nbsp;<span style="color:#63a35c">'gentleman'</span>,&nbsp;<span style="color:#63a35c">'sexy&nbsp;lady'</span>]</div><div style="padding:0 6px; white-space:pre; line-height:130%">&nbsp;</div><div style="padding:0 6px; white-space:pre; line-height:130%"><span style="color:#a71d5d">for</span>&nbsp;x&nbsp;<span style="color:#a71d5d">in</span>&nbsp;family:&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color:#999999">#&nbsp;family의&nbsp;각&nbsp;항목&nbsp;x에&nbsp;대하여:</span></div><div style="padding:0 6px; white-space:pre; line-height:130%">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color:#066de2">print</span>(x,&nbsp;<span style="color:#066de2">len</span>(x))&nbsp;&nbsp;&nbsp;&nbsp;<span style="color:#999999">#&nbsp;x와&nbsp;x의&nbsp;길이를&nbsp;출력하라.</span></div></div></td><td style="vertical-align:bottom;padding:0 2px 4px 0"><a href="http://colorscripter.com/info#e" target="_blank" style="text-decoration:none;color:white"><span style="font-size:9px;word-break:normal;background-color:#e5e5e5;color:white;border-radius:10px;padding:1px">cs</span></a></td></tr></table></div>


<br>
family 의 값들이 차례대로 x 에 들어감.

family 의 길이 만큼 반복함.

<br>
결과 : 

            mother 6
		father 6
		gentleman 9
		sexy lady 9

<br>
range 사용 for 문 예제)

<div class="colorscripter-code" style="color:#010101;font-family:Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; position:relative !important;overflow:auto"><table class="colorscripter-code-table" style="margin:0;padding:0;border:none;background-color:#fafafa;border-radius:4px;" cellspacing="0" cellpadding="0"><tr><td style="padding:6px 0;text-align:left"><div style="margin:0;padding:0;color:#010101;font-family:Consolas, 'Liberation Mono', Menlo, Courier, monospace !important;line-height:130%"><div style="padding:0 6px; white-space:pre; line-height:130%"><span style="color:#a71d5d">for</span>&nbsp;i&nbsp;<span style="color:#a71d5d">in</span>&nbsp;<span style="color:#066de2">range</span>(<span style="color:#0099cc">5</span>):</div><div style="padding:0 6px; white-space:pre; line-height:130%">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color:#066de2">print</span>(i)&nbsp;</div><div style="padding:0 6px; white-space:pre; line-height:130%">...</div><div style="padding:0 6px; white-space:pre; line-height:130%"><span style="color:#0099cc">0</span></div><div style="padding:0 6px; white-space:pre; line-height:130%"><span style="color:#0099cc">1</span></div><div style="padding:0 6px; white-space:pre; line-height:130%"><span style="color:#0099cc">2</span></div><div style="padding:0 6px; white-space:pre; line-height:130%"><span style="color:#0099cc">3</span></div><div style="padding:0 6px; white-space:pre; line-height:130%"><span style="color:#0099cc">4</span></div></div></td><td style="vertical-align:bottom;padding:0 2px 4px 0"><a href="http://colorscripter.com/info#e" target="_blank" style="text-decoration:none;color:white"><span style="font-size:9px;word-break:normal;background-color:#e5e5e5;color:white;border-radius:10px;padding:1px">cs</span></a></td></tr></table></div>

i 에 값이 0,1,2,3,4 들어가면서 5번 반복.

<br>
<br>

enumerate
- 반복문 사용시 몇번째 반복문인지 알아야 될 때가 있는데 이때 사용된다.
- 인덱스 번호(i), 컬렉션 원소(v) 값을 tuple 형태로 반환한다.

간단 예제 1)
<br>
<div class="colorscripter-code" style="color:#010101;font-family:Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; position:relative !important;overflow:auto"><table class="colorscripter-code-table" style="margin:0;padding:0;border:none;background-color:#fafafa;border-radius:4px;" cellspacing="0" cellpadding="0"><tr><td style="padding:6px 0;text-align:left"><div style="margin:0;padding:0;color:#010101;font-family:Consolas, 'Liberation Mono', Menlo, Courier, monospace !important;line-height:130%"><div style="padding:0 6px; white-space:pre; line-height:130%">t&nbsp;<span style="color:#0086b3"></span><span style="color:#a71d5d">=</span>&nbsp;[<span style="color:#0099cc">1</span>,&nbsp;<span style="color:#0099cc">5</span>,&nbsp;<span style="color:#0099cc">7</span>,&nbsp;<span style="color:#0099cc">33</span>,&nbsp;<span style="color:#0099cc">39</span>,&nbsp;<span style="color:#0099cc">52</span>]</div><div style="padding:0 6px; white-space:pre; line-height:130%"><span style="color:#a71d5d">for</span>&nbsp;p&nbsp;<span style="color:#a71d5d">in</span>&nbsp;enumerate(t):</div><div style="padding:0 6px; white-space:pre; line-height:130%">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color:#066de2">print</span>(p)</div><div style="padding:0 6px; white-space:pre; line-height:130%">...&nbsp;</div><div style="padding:0 6px; white-space:pre; line-height:130%">(<span style="color:#0099cc">0</span>,&nbsp;<span style="color:#0099cc">1</span>)</div><div style="padding:0 6px; white-space:pre; line-height:130%">(<span style="color:#0099cc">1</span>,&nbsp;<span style="color:#0099cc">5</span>)</div><div style="padding:0 6px; white-space:pre; line-height:130%">(<span style="color:#0099cc">2</span>,&nbsp;<span style="color:#0099cc">7</span>)</div><div style="padding:0 6px; white-space:pre; line-height:130%">(<span style="color:#0099cc">3</span>,&nbsp;<span style="color:#0099cc">33</span>)</div><div style="padding:0 6px; white-space:pre; line-height:130%">(<span style="color:#0099cc">4</span>,&nbsp;<span style="color:#0099cc">39</span>)</div><div style="padding:0 6px; white-space:pre; line-height:130%">(<span style="color:#0099cc">5</span>,&nbsp;<span style="color:#0099cc">52</span>)</div></div></td><td style="vertical-align:bottom;padding:0 2px 4px 0"><a href="http://colorscripter.com/info#e" target="_blank" style="text-decoration:none;color:white"><span style="font-size:9px;word-break:normal;background-color:#e5e5e5;color:white;border-radius:10px;padding:1px">cs</span></a></td></tr></table></div>
<br>
<br>

간단예제 2)
<br>
<div class="colorscripter-code" style="color:#010101;font-family:Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; position:relative !important;overflow:auto"><table class="colorscripter-code-table" style="margin:0;padding:0;border:none;background-color:#fafafa;border-radius:4px;" cellspacing="0" cellpadding="0"><tr><td style="padding:6px 0;text-align:left"><div style="margin:0;padding:0;color:#010101;font-family:Consolas, 'Liberation Mono', Menlo, Courier, monospace !important;line-height:130%"><div style="padding:0 6px; white-space:pre; line-height:130%"><span style="color:#a71d5d">for</span>&nbsp;i,&nbsp;v&nbsp;<span style="color:#a71d5d">in</span>&nbsp;enumerate(t):</div><div style="padding:0 6px; white-space:pre; line-height:130%">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color:#066de2">print</span>(<span style="color:#63a35c">"index&nbsp;:&nbsp;{},&nbsp;value:&nbsp;{}"</span>.<span style="color:#066de2">format</span>(i,v))</div><div style="padding:0 6px; white-space:pre; line-height:130%">...&nbsp;</div><div style="padding:0 6px; white-space:pre; line-height:130%">index&nbsp;:&nbsp;<span style="color:#0099cc">0</span>,&nbsp;value:&nbsp;<span style="color:#0099cc">1</span></div><div style="padding:0 6px; white-space:pre; line-height:130%">index&nbsp;:&nbsp;<span style="color:#0099cc">1</span>,&nbsp;value:&nbsp;<span style="color:#0099cc">5</span></div><div style="padding:0 6px; white-space:pre; line-height:130%">index&nbsp;:&nbsp;<span style="color:#0099cc">2</span>,&nbsp;value:&nbsp;<span style="color:#0099cc">7</span></div><div style="padding:0 6px; white-space:pre; line-height:130%">index&nbsp;:&nbsp;<span style="color:#0099cc">3</span>,&nbsp;value:&nbsp;<span style="color:#0099cc">33</span></div><div style="padding:0 6px; white-space:pre; line-height:130%">index&nbsp;:&nbsp;<span style="color:#0099cc">4</span>,&nbsp;value:&nbsp;<span style="color:#0099cc">39</span></div><div style="padding:0 6px; white-space:pre; line-height:130%">index&nbsp;:&nbsp;<span style="color:#0099cc">5</span>,&nbsp;value:&nbsp;<span style="color:#0099cc">52</span></div></div></td><td style="vertical-align:bottom;padding:0 2px 4px 0"><a href="http://colorscripter.com/info#e" target="_blank" style="text-decoration:none;color:white"><span style="font-size:9px;word-break:normal;background-color:#e5e5e5;color:white;border-radius:10px;padding:1px">cs</span></a></td></tr></table></div>
<br>
<br>

**while 문**

간단 예제)
<br>
<div class="colorscripter-code" style="color:#010101;font-family:Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; position:relative !important;overflow:auto"><table class="colorscripter-code-table" style="margin:0;padding:0;border:none;background-color:#fafafa;border-radius:4px;" cellspacing="0" cellpadding="0"><tr><td style="padding:6px 0;text-align:left"><div style="margin:0;padding:0;color:#010101;font-family:Consolas, 'Liberation Mono', Menlo, Courier, monospace !important;line-height:130%"><div style="padding:0 6px; white-space:pre; line-height:130%">treeHit&nbsp;<span style="color:#0086b3"></span><span style="color:#a71d5d">=</span>&nbsp;<span style="color:#0099cc">0</span></div><div style="padding:0 6px; white-space:pre; line-height:130%"><span style="color:#a71d5d">while</span>&nbsp;treeHit&nbsp;<span style="color:#0086b3"></span><span style="color:#a71d5d">&lt;</span>&nbsp;<span style="color:#0099cc">10</span>:</div><div style="padding:0 6px; white-space:pre; line-height:130%">&nbsp;&nbsp;&nbsp;&nbsp;treeHit&nbsp;<span style="color:#0086b3"></span><span style="color:#a71d5d">=</span>&nbsp;treeHit&nbsp;<span style="color:#0086b3"></span><span style="color:#a71d5d">+</span><span style="color:#0099cc">1</span></div><div style="padding:0 6px; white-space:pre; line-height:130%">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color:#066de2">print</span>(<span style="color:#63a35c">"나무를&nbsp;%d번&nbsp;찍었습니다."</span>&nbsp;%&nbsp;treeHit)</div><div style="padding:0 6px; white-space:pre; line-height:130%">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color:#a71d5d">if</span>&nbsp;treeHit&nbsp;<span style="color:#0086b3"></span><span style="color:#a71d5d">=</span><span style="color:#0086b3"></span><span style="color:#a71d5d">=</span>&nbsp;<span style="color:#0099cc">10</span>:</div><div style="padding:0 6px; white-space:pre; line-height:130%">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color:#066de2">print</span>(<span style="color:#63a35c">"나무&nbsp;넘어갑니다."</span>)</div></div></td><td style="vertical-align:bottom;padding:0 2px 4px 0"><a href="http://colorscripter.com/info#e" target="_blank" style="text-decoration:none;color:white"><span style="font-size:9px;word-break:normal;background-color:#e5e5e5;color:white;border-radius:10px;padding:1px">cs</span></a></td></tr></table></div>
<br>
<br>
출력결과 :

    나무를 1번 찍었습니다.
		나무를 2번 찍었습니다.
		나무를 3번 찍었습니다.
		나무를 4번 찍었습니다.
		나무를 5번 찍었습니다.
		나무를 6번 찍었습니다.
		나무를 7번 찍었습니다.
		나무를 8번 찍었습니다.
		나무를 9번 찍었습니다.
		나무를 10번 찍었습니다.
		나무 넘어갑니다.

<br>
<br>
<br>
### 함수
-------------------------------------------------------------------------------

파이썬 함수 구조

**def 함수명(매개변수):**
<br>    <수행할 문장1>
<br>    <수행할 문장2>
<br>    ...

<br>
<br>
<br>

### 가변 인자
-----------------------------------------------

#### 위치가변인자 (\*args)

-임의의 갯수의 매개변수를 받을때 사용한다.

- 매개변수에는 보통 for 문을 돌려서 접근한다. (**for x in args**)

- 추가적인 인자를 튜플로 전달한다.


간단 예제)

```python
def f(x, *args):
    # x -> 1
    # args -> (2,3,4,5)
```
<br>
<br>

ex) 입력받은 매개변수대로 더해서 결과를 리턴하는 함수
<br>
<div class="colorscripter-code" style="color:#010101;font-family:Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; position:relative !important;overflow:auto"><table class="colorscripter-code-table" style="margin:0;padding:0;border:none;background-color:#fafafa;border-radius:4px;" cellspacing="0" cellpadding="0"><tr><td style="padding:6px 0;text-align:left"><div style="margin:0;padding:0;color:#010101;font-family:Consolas, 'Liberation Mono', Menlo, Courier, monospace !important;line-height:130%"><div style="padding:0 6px; white-space:pre; line-height:130%"><span style="color:#a71d5d">def</span>&nbsp;add_many(<span style="color:#0086b3"></span><span style="color:#a71d5d">*</span>args):&nbsp;</div><div style="padding:0 6px; white-space:pre; line-height:130%">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;result&nbsp;<span style="color:#0086b3"></span><span style="color:#a71d5d">=</span>&nbsp;<span style="color:#0099cc">0</span>&nbsp;</div><div style="padding:0 6px; white-space:pre; line-height:130%">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color:#a71d5d">for</span>&nbsp;i&nbsp;<span style="color:#a71d5d">in</span>&nbsp;args:&nbsp;</div><div style="padding:0 6px; white-space:pre; line-height:130%">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;result&nbsp;<span style="color:#0086b3"></span><span style="color:#a71d5d">=</span>&nbsp;result&nbsp;<span style="color:#0086b3"></span><span style="color:#a71d5d">+</span>&nbsp;i&nbsp;</div><div style="padding:0 6px; white-space:pre; line-height:130%">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color:#a71d5d">return</span>&nbsp;result&nbsp;</div><div style="padding:0 6px; white-space:pre; line-height:130%">&nbsp;</div></div></td><td style="vertical-align:bottom;padding:0 2px 4px 0"><a href="http://colorscripter.com/info#e" target="_blank" style="text-decoration:none;color:white"><span style="font-size:9px;word-break:normal;background-color:#e5e5e5;color:white;border-radius:10px;padding:1px">cs</span></a></td></tr></table></div>

<br>
<br>


#### 키워드 가변인자 (\*\*kwargs)

- 임의의 갯수의 키워드도 가변인자로 받을수 있다.
- 키워드 : ex) flag=True,   mode='fast',   header='debug' ......

간단 예제)

```python
def f(x, y, **kwargs):
    # x -> 2
    # y -> 3
    # kwargs -> { 'flag': True, 'mode': 'fast', 'header': 'debug' }
```
<br>
<br>

두가지 혼합 간단 예제)
```python
def f(*args, **kwargs):
    # args = (2, 3)
    # kwargs -> { 'flag': True, 'mode': 'fast', 'header': 'debug' }
```
<br>
<br>


### 클래스와 객체
-------------------

#### self
<https://velog.io/@magnoliarfsit/RePython-1.-self-%EC%9D%B4%ED%95%B4%ED%95%98%EA%B8%B0>

-하나의 클래스를 선언하고, 인스턴스를 새로 생성하면 self 는 그 인스턴스의 값이 된다.
<br>
-클래스 내부에 정의된 함수(메서드)의 매개변수는 첫번째로 무조건 self 이여야 한다. 안그러면 에러가 난다.

예를들어

<div class="colorscripter-code" style="color:#010101;font-family:Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; position:relative !important;overflow:auto"><table class="colorscripter-code-table" style="margin:0;padding:0;border:none;background-color:#fafafa;border-radius:4px;" cellspacing="0" cellpadding="0"><tr><td style="padding:6px 0;text-align:left"><div style="margin:0;padding:0;color:#010101;font-family:Consolas, 'Liberation Mono', Menlo, Courier, monospace !important;line-height:130%"><div style="padding:0 6px; white-space:pre; line-height:130%"><span style="color:#a71d5d">class</span>&nbsp;Car:</div><div style="padding:0 6px; white-space:pre; line-height:130%">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color:#a71d5d">def</span>&nbsp;func1():</div><div style="padding:0 6px; white-space:pre; line-height:130%">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color:#066de2">print</span>(<span style="color:#63a35c">"call&nbsp;func1"</span>)</div><div style="padding:0 6px; white-space:pre; line-height:130%">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color:#a71d5d">def</span>&nbsp;func2(<span style="color:#066de2">self</span>):</div><div style="padding:0 6px; white-space:pre; line-height:130%">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color:#066de2">print</span>(<span style="color:#63a35c">"call&nbsp;func2"</span>)</div></div></td><td style="vertical-align:bottom;padding:0 2px 4px 0"><a href="http://colorscripter.com/info#e" target="_blank" style="text-decoration:none;color:white"><span style="font-size:9px;word-break:normal;background-color:#e5e5e5;color:white;border-radius:10px;padding:1px">cs</span></a></td></tr></table></div>
<br>
라고 가정할때
<br>
<div class="colorscripter-code" style="color:#010101;font-family:Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; position:relative !important;overflow:auto"><table class="colorscripter-code-table" style="margin:0;padding:0;border:none;background-color:#fafafa;border-radius:4px;" cellspacing="0" cellpadding="0"><tr><td style="padding:6px 0;text-align:left"><div style="margin:0;padding:0;color:#010101;font-family:Consolas, 'Liberation Mono', Menlo, Courier, monospace !important;line-height:130%"><div style="padding:0 6px; white-space:pre; line-height:130%">car&nbsp;<span style="color:#0086b3"></span><span style="color:#a71d5d">=</span>&nbsp;Car()</div><div style="padding:0 6px; white-space:pre; line-height:130%">car.func1()</div></div></td><td style="vertical-align:bottom;padding:0 2px 4px 0"><a href="http://colorscripter.com/info#e" target="_blank" style="text-decoration:none;color:white"><span style="font-size:9px;word-break:normal;background-color:#e5e5e5;color:white;border-radius:10px;padding:1px">cs</span></a></td></tr></table></div>
<br>
하면 takes 0 positional arguments but 1 was given 에러가 발생하고
<br>
<br>
<div class="colorscripter-code" style="color:#010101;font-family:Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; position:relative !important;overflow:auto"><table class="colorscripter-code-table" style="margin:0;padding:0;border:none;background-color:#fafafa;border-radius:4px;" cellspacing="0" cellpadding="0"><tr><td style="padding:6px 0;text-align:left"><div style="margin:0;padding:0;color:#010101;font-family:Consolas, 'Liberation Mono', Menlo, Courier, monospace !important;line-height:130%"><div style="padding:0 6px; white-space:pre; line-height:130%">car&nbsp;<span style="color:#0086b3"></span><span style="color:#a71d5d">=</span>&nbsp;Car()</div><div style="padding:0 6px; white-space:pre; line-height:130%">car.func2()</div></div></td><td style="vertical-align:bottom;padding:0 2px 4px 0"><a href="http://colorscripter.com/info#e" target="_blank" style="text-decoration:none;color:white"><span style="font-size:9px;word-break:normal;background-color:#e5e5e5;color:white;border-radius:10px;padding:1px">cs</span></a></td></tr></table></div>
<br>
하면 에러가 발생 안한다.

그 이유는 self 는 새롭게 생성된 인스턴스의 id 를 갖고있고, 여기서 id 는 메모리 위치값이다.

func1 은 self 가 없어서 새롭게 생선된 인스턴스의 id 가 없어서 바인딩이 안되어서 에러가 나는 것 같다.

반대로 Car.func1() 하면 에러가 안나온다. 대신 Car.func2() 하면 인수가 하나 빠졌다고 에러가 나온다.
(파이썬에서 클래스는 그 자체로 하나의 네임스페이스 이기 때문에 인스턴스 생성을 안하고도 Car.func1() 처럼 바로 메소드를 직접 사용할수 있다.)

Car.func2(car) 로 인스턴스를 매개변수로 넣으면 오류가 안나온다.

즉 car.func2() 나 Car.func2(car) 나 둘다 같은거고 차이는 없다.






따라서 클래수 내부의 함수에 self 인자를 제일 처음 넣어야 되는것은, **새롭게 생성될 인스턴스 객체에 바인딩 하기 위해서**이다.

**self 는 새롭게 생성된 객체의 인스턴스 자기 자신을 말하는 것이다.** 보통 매개변수 값으로 안넣어도 자동으로 전달된다.
