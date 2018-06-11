
## 1. 조건문
- if, elif, else

### 1.1 if
```
조건이 True면 code 실행

if (조건):
    code
```


```python
flag=True
if flag:
    print("dss") # flag는 True이기 때문에 code 실행
print("done") # 이건 따로 써준 것
```

    dss
    done
    

### 1.2 else
```
조건이 False면 code_2 실행

if (조건):
    code_1
else:
    code_2
```


```python
flag=False
if flag:
    print("dss")
else:
    print("data")
print("done")
```

    data
    done
    

### 1.3 elif
```
조건_1이 False면 조건_2를 봐주고 그것이 True면 code_2 실행, 조건_2도 False면 code_3 실행

if (조건_1):
    code_1
elif (조건_2):
    code_2
else:
    code_3
```
- if 조건 여러개. if를 모두 봐주지 않고 마지막으로 넘어감


```python
# 등급 매기기
# 10~8 - A; 
# 7~4 - B; 
# 3~0 - C

point=7
result="" # "", 0처럼 공백의 값 지정
if point>=8:
    result="A"
elif point<8 or point>=4:
    result="B"
else:
    result="C"
print("done",result)
```

    done B
    


```python
# Quiz) 숫자를 하나 입력 받아서 홀수이면 "odd", 짝수이면 "even"를 출력하는 코드를 만드시오.

number=int(input("insert number : "))
if number % 2 == 1:
    print("odd")
else:
    print("even")
```

    insert number : 4
    even
    

### 1.4 삼항연산
- if else를 한 줄로!
- `(True) if (condition) else (False)`


```python
number=int(input("insert number : "))
result="odd" if number % 2 == 1 else "even"
print(result)
```

    insert number : 9
    odd
    

## 2. 반복문
- while, for, list comprehension

### 2.1 while
```
조건이 True일 '동안' code를 반복 실행, False가 될 때까지!

while (조건):
     code
```     
- 조건이 만족하는 동안 반복 명령문을 실행
- 반복 횟수를 모를 때 사용


```python
a=3
while a>0:
    print(a)
    a-=1
a

# a>0인 조건 안에서 a를 출력하고 a를 계속 1만큼씩 빼다가 a>0이 아닌 순간 반복 종료 후 그 순간의 값 출력
```

    3
    2
    1
    




    0




```python
# break - break 코드를 만나면 강제로 반복문이 종료됨.
#        반복 루프가 거기서 캔슬됨 (FOR 반복문 종료)

a=3
while a>0:
    print(a)
    if a==2:
        break
    a-=1
a
```

    3
    2
    




    2




```python
# continue - continue 코드를 만나면 바로 반복문 구문으로 이동됨.
#            해당 루프만 한번만 스킵하고, 그 이후에는 루프 반복
a=3
while a>0:
    print(a)
    if a==2:
        a=0 # a가 2일 때 0으로 바꾸고 
        continue # 반복문으로 이동 (하지만 0>0이 아니라서 자동 종료됨)
    a-=1
a
```

    3
    2
    




    0



### 2.2 For
- range, zip, enumerate
- while보다 더 많이 쓰임.

#### 1) range
```
for (value) in (list):
    code (value)
```

- 순서가 있는 collection 내의 value값 하나씩


```python
ls=[0,1,2,3,4,5]
ls
```




    [0, 1, 2, 3, 4, 5]




```python
# 0~99까지 등 큰 데이터를 만들고 싶을 때 range 사용!

range(100)
```




    range(0, 100)




```python
# 보여주기 위해서 range를 리스트로 형변환한 것뿐

list(range(6))
```




    [0, 1, 2, 3, 4, 5]




```python
list(range(2,6)) # offset처럼! 2<=a<6
```




    [2, 3, 4, 5]




```python
list(range(0,6,2)) # 2는 offset의 step에 해당
```




    [0, 2, 4]




```python
list(range(6,0,-1)) # 6>=a>0, 내림차순
```




    [6, 5, 4, 3, 2, 1]




```python
for _ in range(5):
    print("dss") 
```

    dss
    dss
    dss
    dss
    dss
    


```python
for num in range(5):
    print("dss")

# 이렇게도 쓰지만 위에껄로 많이 씀
```

    dss
    dss
    dss
    dss
    dss
    


```python
for num in range(5):
    print("dss", num)

# num까지 같이 프린트해주고 싶을 때
```

    dss 0
    dss 1
    dss 2
    dss 3
    dss 4
    


```python
ls=["data","science","school"]
for idx in range(len(ls)):
    print(ls[idx])
    
# len(ls)는 3 -> range 0~2에 대해 ls[0], ls[1], ls[2]를 출력
```

    data
    science
    school
    

- DSS에서 들은 내용


```python
basket=['apple', 'banana', 'chicken', 'pineapple', 'cherry']

for stuff in basket:
    print(stuff)
    
# basket 리스트에 있는 stuff 요소들을 모두 하나씩 꺼내서 print해줌(반복)

# 위 반복문은 아래의 실행문과 결과가 같습니다. 
# stuff = basket[0]
# print(stuff)
# stuff = basket[1]
# print(stuff)
# stuff = basket[2]
# print(stuff)
# stuff = basket[3]
# print(stuff)
# stuff = basket[4]
# print(stuff)
```

    apple
    banana
    chicken
    pineapple
    cherry
    


```python
# range(_,_) 뒤에 숫자 바로 앞 숫자까지가 range에 속함
# range(1,5) => 1 부터 4 까지

for i in range(1,5):
    print(i)
```

    1
    2
    3
    4
    


```python
# range(1,6) => 1 부터 5 까지

for i in range(1,6):
    if i==5:
        print("beep!")
    
    print(i)
```

    1
    2
    3
    4
    beep!
    5
    


```python
# break 삽입하면 반복 루프가 거기서 캔슬됨 (FOR 반복문 종료)

for i in range(1,6):
    if i==5:
        print("beep!")
        break
        
    print(i)
```

    1
    2
    3
    4
    beep!
    


```python
for i in range(1,6):
    if i==2:
        print("boop!")
    if i==5:
        print("beep!")
        break
        
    print(i)
```

    1
    boop!
    2
    3
    4
    beep!
    


```python
# continue는 해당 루프만 한번만 스킵하고, 그 이후에는 루프 반복

for i in range(1,6):
    if i==2:
        print("boop!")
        continue
        
    if i==5:
        print("beep!")
        break
        
    print(i)
```

    1
    boop!
    3
    4
    beep!
    

#### 2) zip
- 2개의 리스트를 key, value 형태(딕셔너리)로 묶어주는 함수


```python
subs=["math","english","science"]
points=[100,80,90]

# dic={"math":100,"english":80,"science":90}
# 이런 딕셔너리를 만들어 주고자 함

# zip을 사용하지 않은 경우

result={}
for idx in range(len(subs)):
    result[subs[idx]]=points[idx]
result
```




    {'english': 80, 'math': 100, 'science': 90}




```python
# zip 사용한 경우

for sub, point in zip(subs,points):
    result[sub]=point
result
```




    {'english': 80, 'math': 100, 'science': 90}




```python
# zip을 튜플이나 딕셔너리로 형변환 해주기

tuple(zip(subs,points)), dict(zip(subs,points))
```




    ((('math', 100), ('english', 80), ('science', 90)),
     {'english': 80, 'math': 100, 'science': 90})



#### 3) enumerate
- 리스트 형태의 데이터를 index와 value를 동시에 사용할 수 있음.


```python
# enumerate 사용 안한 경우

num=0
ls=["math","science","korean"]
for value in ls:
    print(num,value)
    num+=1
```

    0 math
    1 science
    2 korean
    


```python
# enumerate 이용한 경우

ls=["math","science","korean"]
for num, value in enumerate(ls):
    print(num,value)
```

    0 math
    1 science
    2 korean
    


```python
# Quiz) for문을 이용해 리스트 내에 숫자들을 모두 더하는 코딩을 하시오.

numbers=[1,3,5,7,9]
result=0

for number in numbers:
    result+=number
result

```




    25



### 2.3 List Comprehension
- 반복되어 출력되는 리스트 형태의 데이터를 만들어 주는 문법
- for문보다 속도가 빠름. (제약이 좀 있지만 list comprehension으로 쓸 수 있는 건 써주는 게 좋다)

- ls=`[<value> for <value> in <list> if <조건>]`
- 삼항연산 시 ls=`[(True) if <조건> else (False) <value> for <value> in <list>]`
- if는 리스트 내에 조건 걸고 싶을 때 사용. true에 해당하는 value만 추가


```python
ls=[1,2,3,4,5]
ls
```




    [1, 2, 3, 4, 5]




```python
ls=[]
ls.append(1)
ls.append(2)
ls.append(3)
ls.append(4)
ls.append(5)
ls
```




    [1, 2, 3, 4, 5]




```python
# for문 이용 시

ls=[]
for num in range(1,6):
    ls.append(num)
ls
```




    [1, 2, 3, 4, 5]




```python
# 위 식을 list comprehension으로

ls=[num for num in range(1,6)]
ls
```




    [1, 2, 3, 4, 5]




```python
%%timeit # for와 list comprehension으로 만든 것 속도 비교

ls=[]
for num in range(1,10001):
    ls.append(num)
    
len(ls) # 만 개 잘 들어갔음을 확인
```

    1.37 ms ± 14.9 µs per loop (mean ± std. dev. of 7 runs, 1000 loops each)
    


```python
%%timeit

ls=[num for num in range(1,10001)]

len(ls) # 만 개 잘 들어갔음을 확인
```

    632 µs ± 90.8 µs per loop (mean ± std. dev. of 7 runs, 1000 loops each)
    


```python
# 0 ~ 10까지 숫자를 출력하고 해당 숫자가 짝수인지 홀수인지를 판별해서 odd와 even 문자열을 추가하는 코드

# 삼항연산 이용

ls=[str(num) + ":even" if num % 2==0 else str(num) + ":odd" for num in range(11)]
ls
```




    ['0:even',
     '1:odd',
     '2:even',
     '3:odd',
     '4:even',
     '5:odd',
     '6:even',
     '7:odd',
     '8:even',
     '9:odd',
     '10:even']




```python
# 홀수만 출력되게 코드 작성 (filtering 개념)

# 조건 if 사용

ls=[num for num in range(11) if num % 2==1]
ls
```




    [1, 3, 5, 7, 9]




```python
# Quiz) lee씨 성을 가진 사람의 성을 삭제하는 코드를 작성하세요

names=["kim dss", "lee python", "park data", "lee macpro"]

result_1=[
    name.split(" ")[1] if name.split(" ")[0] == "lee" else name # 공백으로 분리하고 0번째가 성, 1번째가 이름
    for name in names
]
result_1

# result_1=[value[4:] if value[:3]=="lee" else value for value in names]  이건 내가 한 것
```




    ['kim dss', 'python', 'park data', 'macpro']




```python
# result_1 + park씨 성을 가진 데이터를 제거까지

result_2=[
    name.split(" ")[1] if name.split(" ")[0] == "lee" else name
    for name in names
    if name.split(" ")[0] != "park" # 성이 park인 경우는 아예 리스트에 안 들어가는 것
]
result_2
```




    ['kim dss', 'python', 'macpro']


