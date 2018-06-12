
# Function
- basic: 선언, 호출, parameter, argument 개념 (보통 parameter로 통용), return
- `*args`, `**kwargs` 
- docstring -> 만든 함수에 대한 설명
- scope: global, local
- inner function (익명함수)
- lambda function
- map, filter, reduce
- decolater

## 1. Basic

### 1.1 선언과 호출

- 선언
```
def <function name>():
    <code>
```
- 호출
```
<function name>()
```


```python
# 선언

def sum_func(a,b):
    print(a+b)
```


```python
# 호출 -> 함수에 작성된 코드 실행

sum_func(1,2)
```

    3
    


```python
type(sum_func) # 데이터 타입은 function
```




    function



### 1.2 Parameter, Argument
- parameter: 함수의 입력 값 인터페이스
- argument: 실제 pararmeter에 대입|


```python
def sum_func(a,b): # a, b: parameter
    print(a+b)
```


```python
sum_func(1,2) # 1, 2: argument - format처럼 자동으로 순서대로 들어감.
```

    3
    


```python
def div_func(a,b):
    print(a/b)
```


```python
div_func(10,2)
```

    5.0
    


```python
# keyword argument

div_func(b=10,a=2) # key=value를 지정해 parameter의 변수명과 함수 호출시 설정한 arguement의 keyword에 의해서 value 대입 
```

    0.2
    


```python
# default parameter

def sum_func(a,b=0): # b=0을 default로 설정
    print(a+b)
```


```python
sum_func(1) # 호출 시 default parameter에 대한 arg가 없으면 default값이 나옴
```

    1
    


```python
sum_func(2,3) # 둘 다 들어가도 당연히 나오고
```

    5
    


```python
# 주의! default parameter를 앞에다 쓰면 안 됨. (error)

# def sum_func(b=0,a):
#    print(a+b)
```


```python
# 이렇게 모두 뒤에다 몰아서 써줘야 함.

def sum_func(a,b,c=1,d=3):
    print(a+b+c+d)
```

### 1.3 Return
- 함수를 호출했을 때 결과를 반환하는 용도로 사용 -> out에 결과값 나옴
- return 값은 넣어줘도 되고, 안 넣어줘도 됨(optional)
- return 값이 없는 함수는 print 하면 None이 찍힘


```python
def sum_func(a,b):
    return a+b  
sum_func(1,2) 

# result=sum_func(1,2) 
# result 
# 는,
# sum_func 함수를 호출한 후 함수의 리턴값을 result라는 변수에 저장하고 result 변수 출력

# 리턴이 있는 함수는 변수로 받아서 추후에 계속 사용하는 것.
```




    3



## 2. `*Args`, `**Kwargs`
- 함수를 만들고 호출할 때, 아규먼트나 파라미터의 개수에 구애받지 않고 싶을 때 사용
- `*` : 전부, 모두, All의 의미 -> 모든 아규먼트 / 모든 키워드와 밸류
- `*Args` : keyword가 '없는' 아규먼트를 파라미터로 받을 때 사용
- `**Kwargs` : keyword가 '있는' 아규먼트를 파라미터로 받을 때 사용


```python
# *args

def sum_func(*args):
    print(args)
    print(type(args)) # args의 데이터 타입은 튜플
    print(args[2]) # 튜플의 offset처럼 이용 가능
sum_func(1,2,3,4,5) # 아규먼트 개수 상관 없음. -> 수정 가능
```

    (1, 2, 3, 4, 5)
    <class 'tuple'>
    3
    


```python
# **kwargs

def points(**kwargs):
    print(kwargs)
    print(type(kwargs)) # kwargs의 데이터 타입은 딕셔너리 (key, value 값이 있으니까)
    print(kwargs["math"]) # math key에 대한 value 값 프린트
points(math=90,science=70) # 아규먼트 개수 상관 없음. -> 수정 가능
```

    {'math': 90, 'science': 70}
    <class 'dict'>
    90
    


```python
# 두 개 같이 사용

def dss(*args, **kwargs):
    print(args)
    print(kwargs)
dss(1,2,3,num1=10,num2=20) # 키워드가 없는 건 args로, 있는 건 kwarg로 자동으로 들어감
```

    (1, 2, 3)
    {'num1': 10, 'num2': 20}
    


```python
# argument에 *ls 넣기

def dss (*args):
    print(args)
    
ls=[1,2,3,4]
dss(*ls) # ls 각각의 데이터가 각각의 args로 바뀌어 받아짐.
```

    (1, 2, 3, 4)
    


```python
# *args를 이용하여 평균을 구하는 코드

def avg_func(*args):
    return sum(args)/len(args)
avg_func(100,70,80,99,85,60,80)
```




    82.0




```python
# **kwargs를 이용하여 평균을 구하는 코드

def avg_func(**kwargs):
    total, count=0,0
    for subject, point in kwargs.items():
        print(subject,point)
        total+=point
        count+=1
    return total/count
avg_func(korean=100,english=70,math=80)
```

    korean 100
    english 70
    math 80
    




    83.33333333333333



## 3. Docstring
- 함수에 대한 설명을 넣는 것
```
def <function_name>():
    "description"
    
    혹은
    
    """
    description_1
    description_2
    """
```
- 함수를 선언한 코드 아래에 문자열로 넣음.
- 보통 멀티라인으로 사용
- PEP 20 : The Zen of Python
    - readability counts : 가독성은 중요하다.
- PEP 8 : Style Guide for Python Code


```python
import this
```

    The Zen of Python, by Tim Peters
    
    Beautiful is better than ugly.
    Explicit is better than implicit.
    Simple is better than complex.
    Complex is better than complicated.
    Flat is better than nested.
    Sparse is better than dense.
    Readability counts.
    Special cases aren't special enough to break the rules.
    Although practicality beats purity.
    Errors should never pass silently.
    Unless explicitly silenced.
    In the face of ambiguity, refuse the temptation to guess.
    There should be one-- and preferably only one --obvious way to do it.
    Although that way may not be obvious at first unless you're Dutch.
    Now is better than never.
    Although never is often better than *right* now.
    If the implementation is hard to explain, it's a bad idea.
    If the implementation is easy to explain, it may be a good idea.
    Namespaces are one honking great idea -- let's do more of those!
    


```python
def echo(anything):
    "echo returns its input argument"
    return anythig
```


```python
# docstring 보기 1) 함수 이름 옆에 커서 두고 shift + Tab

echo 
```




    <function __main__.echo>




```python
# 2) ?

echo?
```


```python
# 3) ?? - 소스 보기

echo??
```


```python
def echo(anything):
    """
    echo return its input argument
    The option is:
        1. print anything
        2. return anything
    """
    return anythig
```


```python
# 4) help함수

help(echo)
```

    Help on function echo in module __main__:
    
    echo(anything)
        echo return its input argument
        The option is:
            1. print anything
            2. return anything
    
    


```python
# 만든 함수 말고도 docstring 볼 수 있는 함수들이 몇 가지 있음.
# parameter 확인할 때 쓰면 좋음.

print?
```

## 4. Scope
- global: 어디에서나 사용 가능 
- local: 특정 영역에서만 사용 가능


```python
gv=10
def print_gv():
    print(gv)
print_gv()
```

    10
    


```python
gv=10
def print_gv():
    gv=100 # 100으로 바꿈
    print(gv)
print_gv()
```

    100
    


```python
gv # 100이 아님!!
```




    10




```python
# Global VS Local

# gv=10은 global 영역
# print_gv가 local 영역
# local 영역에 gv=100이 들어간 것
# local 영역 안에 들어간 건 local 영역 내에서만 사용 가능
```


```python
gv=10
def print_gv():
    gv=100
    print(gv)
```


```python
# globals() - global 변수 보는 함수

print(globals())
```

    {'__name__': '__main__', '__doc__': 'Automatically created module for IPython interactive environment', '__package__': None, '__loader__': None, '__spec__': None, '__builtin__': <module 'builtins' (built-in)>, '__builtins__': <module 'builtins' (built-in)>, '_ih': ['', 'gv=10\ndef print_gv():\n    gv=100\n    print(gv)', '# globals() - global 변수 보는 함수\n\nprint(globals())'], '_oh': {}, '_dh': ['C:\\Users\\Hyejeong Kim\\fc_dss\\note'], 'In': ['', 'gv=10\ndef print_gv():\n    gv=100\n    print(gv)', '# globals() - global 변수 보는 함수\n\nprint(globals())'], 'Out': {}, 'get_ipython': <bound method InteractiveShell.get_ipython of <ipykernel.zmqshell.ZMQInteractiveShell object at 0x000000000563E240>>, 'exit': <IPython.core.autocall.ZMQExitAutocall object at 0x00000000056C4278>, 'quit': <IPython.core.autocall.ZMQExitAutocall object at 0x00000000056C4278>, '_': '', '__': '', '___': '', '_i': 'gv=10\ndef print_gv():\n    gv=100\n    print(gv)', '_ii': '', '_iii': '', '_i1': 'gv=10\ndef print_gv():\n    gv=100\n    print(gv)', 'gv': 10, 'print_gv': <function print_gv at 0x00000000069F92F0>, '_i2': '# globals() - global 변수 보는 함수\n\nprint(globals())'}
    


```python
type(globals()), globals()["gv"] # key, value 값으로 들어가있음.
```




    (dict, 10)




```python
# locals() - local 변수 보는 함수

print(locals())
```

    {'__name__': '__main__', '__doc__': 'Automatically created module for IPython interactive environment', '__package__': None, '__loader__': None, '__spec__': None, '__builtin__': <module 'builtins' (built-in)>, '__builtins__': <module 'builtins' (built-in)>, '_ih': ['', 'gv=10\ndef print_gv():\n    gv=100\n    print(gv)', '# globals() - global 변수 보는 함수\n\nprint(globals())', 'type(globals()), globals()["gv"] # key, value 값으로 들어가있음.', '# locals() - local 변수 보는 함수\n\nprint(locals())'], '_oh': {3: (<class 'dict'>, 10)}, '_dh': ['C:\\Users\\Hyejeong Kim\\fc_dss\\note'], 'In': ['', 'gv=10\ndef print_gv():\n    gv=100\n    print(gv)', '# globals() - global 변수 보는 함수\n\nprint(globals())', 'type(globals()), globals()["gv"] # key, value 값으로 들어가있음.', '# locals() - local 변수 보는 함수\n\nprint(locals())'], 'Out': {3: (<class 'dict'>, 10)}, 'get_ipython': <bound method InteractiveShell.get_ipython of <ipykernel.zmqshell.ZMQInteractiveShell object at 0x000000000563E240>>, 'exit': <IPython.core.autocall.ZMQExitAutocall object at 0x00000000056C4278>, 'quit': <IPython.core.autocall.ZMQExitAutocall object at 0x00000000056C4278>, '_': (<class 'dict'>, 10), '__': '', '___': '', '_i': 'type(globals()), globals()["gv"] # key, value 값으로 들어가있음.', '_ii': '# globals() - global 변수 보는 함수\n\nprint(globals())', '_iii': 'gv=10\ndef print_gv():\n    gv=100\n    print(gv)', '_i1': 'gv=10\ndef print_gv():\n    gv=100\n    print(gv)', 'gv': 10, 'print_gv': <function print_gv at 0x00000000069F92F0>, '_i2': '# globals() - global 변수 보는 함수\n\nprint(globals())', '_i3': 'type(globals()), globals()["gv"] # key, value 값으로 들어가있음.', '_3': (<class 'dict'>, 10), '_i4': '# locals() - local 변수 보는 함수\n\nprint(locals())'}
    


```python
gv=10
def print_gv():
    gv=100
    print(locals()) # local 영역에 들어간 gv=100을 프린트하게 됨.
print_gv()
```

    {'gv': 100}
    


```python
# global 예약어 - local 영역에서(함수 내에서) global 변수 변경

gv=10
def dss():
    global gv 
    gv=100
    print(gv)
```


```python
gv
```




    10




```python
dss()
```

    100
    


```python
gv # dss 함수 실행해주면 global 변수가 변경됨.
```




    100



## 5. inner function
- global : 전역변수, 전역함수
- local : 지역변수, 지역함수
- 지역함수 local function (a.k.a. 익명함수)
- local 영역에 함수를 숨겨서 global 영역에서 사용할 수 없도록 함.
    - local 영역은 함수를 실행해야만 메모리에 올라감.


```python
def outer(a,b):
    def inner(c,d):
        return c+d
    return inner(a,b) # inner함수 실행한 결과를 리턴 => 3

outer(1,2) # 이게 호출 안 되면 inner function은 메모리에 안 올라감.
```




    3




```python
# inner(1,2)  - global 영역에서는 inner function에 접근 불가. (error남)
```


```python
def outer(a,b):
    def inner(c,d):
        return c+d
    return inner # inner 함수를 리턴 - 이렇게 하면 inner 함수를 global에서 사용 가능.
                    # 함수도 하나의 데이터 타입이기 때문에 리턴 가능.
i=outer(1,2) # outer(a,b)는 리턴된 inner 함수를 나타냄. 그 함수를 i 변수에 저장.
```


```python
i(1,2)
```




    3



## 6. Lambda function
- 간단한 파라미터를 받아서 리턴해주는 함수를, 람다함수를 이용하여 간단하게 만들어 줄 수 있음.
- `lambda <parameters> : <return_value>`
- 람다함수에 조건을 넣으려면 삼항연산 이용
    - `lambda <parameters> : <return_value1> if <조건> else <return_value2>`


```python
def sum_func(a,b):
    return a+b
sum_func(1,2)
```




    3




```python
# 위 함수를 람다함수를 이용해 만들기

sum_func2=lambda a,b : a+b
sum_func2(1,2)
```




    3




```python
# 함수와, 그에 관련된 파라미터에 대해 함수값을 계산해주는 calc 함수를 만들기

def calc(fn,a,b):
    return fn(a,b)
```


```python
def sum_func(a,b):
    return a+b

calc(sum_func,1,2) # 함수를 만들어놓고 호출
```




    3




```python
def minus_func(a,b):
    return a-b

calc(minus_func,1,2)
```




    -1




```python
# 위 함수를 람다함수를 이용해 만들기

# def calc(fn,a,b):
#     return fn(a,b) 후에
calc(lambda a,b : a+b, 1,2) # 함수가 호출될 때 바로 람다함수를 만드는 것.
```




    3




```python
calc(lambda a,b : a-b, 1,2)
```




    -1




```python
(lambda a,b : a-b)(1,2) # 이렇게 익명함수로 사용!! calc과 같은 함수를 지정해주지 않아도 사용 가능
```




    -1



## 7. Map, Filter, Reduce

### 7.1 Map
- 함수와 리스트를 입력받아서 각 요소에 함수를 적용한 결과를 리스트로 리턴해주는 함수
- `map(function,*list)` 리스트가 여러개 올 수 있다는 것이 특징
- 람다함수 쓰게되면
    `map(lambda <parameters> : <return_value1> if <조건> else <return_value2>, *list)`


```python
ls=[1,2,3,4,5]

def minus_one(num):
    return num-1

# map 사용하지 않고 for문 사용 시

result=[]

for value in ls:
    result.append(minus_one(value))
    
result
```




    [0, 1, 2, 3, 4]




```python
# map 사용 시

# def minus_one(num):
#     return num-1 (선언된 함수)

result=list(map(minus_one,ls)) # 리스트로 형 변환해줘야 리스트로 사용 가능!!!!
result
```




    [0, 1, 2, 3, 4]




```python
result=list(map(lambda num : num-1,ls)) # map에 들어가는 함수 자체를 람다함수로 작성
result
```




    [0, 1, 2, 3, 4]




```python
# map의 docstring을 보면 *iterables 라고 되어있음.
    # 뜻: 순서가 있는 collection이 여러 가지 올 수 있다는 뜻!
```


```python
# 여러 개의 파라미터 사용

ls1=[1,2,3,4]
ls2=[5,6,7,8]

result=list(map(lambda num1, num2 : num1+num2, ls1, ls2))
result

# 리스트의 개수와 함수의 파라미터 개수가 일치해야 함
# 또한, 각 리스트의 요소 개수도 같아야 함. error나지 않도록.
    # 첫 번째 리스트보다 요소가 많으면 error는 안나고 그 요소를 무시하고,
    # 요소가 적으면 error가 남.
```




    [6, 8, 10, 12]




```python
# Quiz) map을 이용하여 names 리스트에서 성만 리스트 결과로 출력하는 코드를 작성하시오.

names=["kim dss", "park python", "lee science", "jung school"]

# def last_name(value):
#     return value.split()[0]

# result=list(map(last_name,names)) 내가 한 것

result=list(map(lambda name : name.split()[0], names)) # 람다함수 이용
result

# names -> 리스트
# lambda 함수의 parameter name -> 리스트 내 각 요소
# name.split()[0] -> 각 요소를 공백으로 분리 후 0번째 값(성)
```




    ['kim', 'park', 'lee', 'jung']




```python
# Quiz 2) 1 ~ 10까지의 숫자 리스트에서 홀수는 odd, 짝수는 even을 출력하고
# key, value 형태의 dict 데이터 타입으로 출력하는 코드를 작성하시오.

number_list=list(range(1,11))

result=list(map(lambda num : "even" if num % 2==0 else "odd", number_list)) 
                                                # 삼항연산을 실행하는 람다함수 만들고 맵핑
    
result=dict(zip(number_list, result)) # zip을 이용해 number_list와 result를 각각 key, value로 만들고
                                        # dict로 형변환
result
```




    {1: 'odd',
     2: 'even',
     3: 'odd',
     4: 'even',
     5: 'odd',
     6: 'even',
     7: 'odd',
     8: 'even',
     9: 'odd',
     10: 'even'}




```python
# Quiz 3) map 함수 구현

ls1=[1,2,3,4]
ls2=[5,6,7,8]
ls3=[9,10,11,12]

def sum_func(*args):
    return sum(args) # sum(args) - 모든 argus를 더 해주는 함수

def map_func(func,*args):
    result=[]
    
    # TODO
    # 리스트 개수와, 리스트 내 요소 수가 바뀔 수 있다는 것을 map함수에 반영해야 함.
    values_count=len(args[0]) # 4 - args개수 넣고
    for idx in range(len(args)): # args 개수 만큼 for문을 돌려서
        values_count = values_count if values_count < len(args[idx]) else len(args[idx])
                                # 작은 데이터가 value_count에 들어가도록
    
    params_count=len(args) # 3 - 리스트 args의 개수
    
    for idx_1 in range(values_count): # for문이 4번 돌고
        params=[]
        for idx_2 in range(params_count): # for문이 3번 돌고
            params.append(args[idx_2][idx_1])
            
        result.append(func(*params))
        
    return result

map_func(sum_func,ls1,ls2,ls3)
# result- [15,18,21,24]
```




    [15, 18, 21, 24]



### 7.2 Filter
- 리스트 데이터에서 조건에 맞는 value 데이터를 필터링 해주는 함수
- filter에 사용되는 함수의 결과 값은 항상 true 아니면 false
    - 그 결과값이 true면 리스트에 남아있고 false면 제거
- `filter(<function>,<list(iterable)>)` 리스트 한 개밖에 못 오는 특징
- 람다함수 쓰게되면
    - `filter(lambda <parameter> : 조건, <list(iterable)>)`


```python
ls=[1,2,3,4,5]
result=list(filter(lambda num : num%2==1, ls)) # 리스트로 변환해주기
result
```




    [1, 3, 5]




```python
# 위 식을 람다 대신 함수 선언해서 만들어보기

ls=[1,2,3,4,5]

def odd(number):
    return number%2==1 # 조건에 맞으면 true값을 리턴

result=list(filter(odd,ls)) # odd 함수에서 true값이 나오는 리스트 요소만 필터링.
result
```




    [1, 3, 5]




```python
# Quiz 1-1) filter를 이용해서 사람 이름의 성이 lee인 사람의 이름만 결과로 출력하는 코드를 작성하시오.

names=["kim dss", "park python", "lee science", "jung school", "lee java"]
result=list(filter(lambda name : name.split()[0]=="lee", names))
result
```




    ['lee science', 'lee java']




```python
# Quiz 1-2) 맨 앞글자 대문자로 만든 후에 해당 코드 작성

names=["kim dss", "park python", "lee science", "jung school", "lee java"]
names = list(map(lambda name : name[:1].upper() + name[1:] , names))
result=list(filter(lambda name : name.split()[0]=="Lee", names)) # "Lee"
result
```




    ['Lee science', 'Lee java']




```python
# Quiz 2) 1~10까지 숫자 중에 짝수를 필터링하는 함수와 홀수를 필터링 함수를 적용하여 filter 코드를 구현하시오.

ls=list(range(1,11))

def odd(number):
    return number % 2==1

def even(number):
    return number % 2==0 

is_odd_even={
    "odd":odd,
    "even":even,
}

def filter_func(func, data_list):
    result=[]
    
    # TODO
    for data in data_list:
        if func(data):
            result.append(data)
    return result

result_1=list(filter_func(is_odd_even["odd"],ls))
result_2=list(filter_func(is_odd_even["even"],ls))
result_1, result_2
```




    ([1, 3, 5, 7, 9], [2, 4, 6, 8, 10])



### 7.3 Reduce
- 리스트 데이터를 처음부터 순서대로 함수로 실행하여,
- 실행결과를 다시 함수의 파라미터로 넣어 함수를 실행해서 
- 결국엔 하나의 값이 리턴되는 함수
- `reduce(<function>, <list>)`


```python
from functools import reduce # reduce는 import해서 사용해야 함.
```


```python
ls=[1,2,3,4,5]

reduce(lambda x, y : x+y,ls) # 1+2라는 결과를 다시 함수의 파라미터로 넣어 3+3 실행하고... -> 다 더한 값 리턴
```




    15




```python
# 가장 큰 수를 구하는 코드

ls=[1,2,5,8,3,4,7]
reduce(lambda x,y : x if x>y else y, ls) # 형변환 해줄 필요없이 하나의 값만 리턴 됨

# 1, 2 들어가면 1>2가 false니까 2 출력,
# 2, 5 들어가면 2>5가 false니까 5 출력....
```




    8




```python
# Quiz) reduce를 이용해서 이름의 길이가 가장 긴 사람을 출력하시오.

names=["kim dss", "park python", "lee science", "jung fastschool", "lee java"]

reduce(lambda x, y : x if len(x)>len(y) else y,names)
```




    'jung fastschool'




```python
# Quiz 2) reduce 함수를 구현하시오.

ls=[1,2,3,4,5]

def reduce_func(func, data_list):
    
    # TODO
    result=data_list[0] # 가장 먼저 첫번째 데이터를 넣고 (1을 넣고)
    del data_list[0] # 그 값을 삭제
    
    for data in data_list:
        result=func(result,data) # result가 첫번째 param, data가 두번째 param
    
    return result
reduce_func(lambda num1, num2 : num1+num2, ls)
# result - 15
```




    [1, 3, 5]



## 8. Decorator
- 여러 개의 함수를 작성하는데, 여러 개의 함수에서 공통된 코드를 뽑아서 묶어 사용할 때 씀.
- 코드를 바꾸지 않고 (공통된) 코드를 수정하거나 추가하고 싶을 때 사용.

```
def A():
    code1
    code2
    code3
  
def B():
    code1
    code4
    code3
```
- 위 A와 B함수에서 공통된 코드인 code 1,3을 따로 빼서 묶어 사용하고 싶을 때 쓰는 것!

```
def C(func):      - decorator 함수 정의
    def wrapper(*args, **kwargs)      - 모든 argu를 호환하기 위해 둘 다 넣어줌
        code1
        result=func(*args, **kwargs)      - 올라온 func(A나 B함수)에 대한 리턴값을 result에 저장
        code3
        return result      - result 반환
    return wrapper      - wrapper 함수 반환 -> global에서 wrapper 함수 사용 
                        -> @이용 시 A나 B함수가 wrapper 함수가 되는 것!!

@C      - C라는 함수를 찾고
def A():      - A 함수가 decorator에 적용될 parameter로 들어감.
    code2
    
@C    
def B():
    code4

A() - code1, code2, code3
B() - code1, code4, code3
```


```python
# A

def sum_func(a,b):
    return a+b # code 2
```


```python
# B

def minus_func(a,b):
    return a-b # code 4
```


```python
# decolator function인 C

def disp(func):
    def wrapper(*args,**kwargs):
        # code 1
        print("running function :", func.__name__) # 함수 이름 보여주기
        print("args :",args)
        print("kwargs :",kwargs)
        result=func(*args,**kwargs)
        # code 3
        print("result: ",result)
        return result
    return wrapper
```


```python
@disp # 데코레이터 넣어주고 
def sum_func(a,b): # A함수 호출
    return a+b # code 2
```


```python
sum_func(1,2)
```

    running function : sum_func
    args : (1, 2)
    kwargs : {}
    result:  3
    




    3




```python
@disp
def minus_func(a,b):
    return a-b # code 4
```


```python
minus_func(5,3)
```

    running function : minus_func
    args : (5, 3)
    kwargs : {}
    result:  2
    




    2




```python
# 함수의 실행 시간을 측정하는 데코레이터 함수

import time
def run_time(func): # @ 실행 시 func 안에 sum_func이 들어감
    def wrapper(*args,**kwargs):
        # code 1
        start_time=time.time() # 시간 불러오고 저장
        result=func(*args,**kwargs) # 들어온 sum_func 실행한 값
        # code 3
        end_time=time.time() # 시간 불러오고 저장
        print("run time :", end_time - strat_time)
        return result
    return wrapper # sum_func이 wrapper 함수가 되는 것, ls가 wrapper에 파라미터로 들어감.
```


```python
@run_time
def sum_func(ls):
    return sum(ls)
```


```python
# ls=list(range(10000))
# sum_func(ls)
# 윈도우는 어떻게..
```


```python
# 관리자 계정을 확인해서 관리자 계정이면 패스워드를 출력하는 함수를 작성하기

# @adimn
# def dss():
#     code
```


```python
admin_ls=["pdj","dss"] # 관리자 계정 리스트
pw="dss8"

def admin(func):
    def wrapper(*args,**kwargs):
        # code 1 - 관리자인지 확인
        user_id=func(*args,**kwargs) # userm_id 받아주기
        if user_id in admin_ls: # user_id가 admin_ls 안에 있으면
            print("allow permission [pw:{}]".format(pw)) # 이걸 출력
        else:
            print("you ar not admin.")
    return wrapper
```


```python
@admin
def input_user(): # user_id 입력받는 함수
    return input("insert user id : ")
```


```python
input_user()
```

    insert user id : dss
    allow permission [pw:dss8]
    


```python
user_id={
    1:"dss",
    2:"data",
    3:"python",
}

@admin
def input_num():
    user_num=int(input("insert user id : "))
    return user_id[user_num]
```


```python
input_num()
```

    insert user id : 1
    allow permission [pw:dss8]
    
