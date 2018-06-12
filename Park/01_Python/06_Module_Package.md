
## Module
- 변수, 함수, 클래스들을 모아놓은 파일
- `import` 예약어로 모듈 호출
- 모듈의 식별자는 짧은 소문자로 작성. 합성어를 사용할 땐 snake_case 사용
- C/C++ 모듈은 식별자가 `_`로 시작
- 모듈 사용 이유: 코딩할 때 파일 하나로 서비스를 만들 수 없기 때문에, 분리해서 만든 후 모아서 사용
- 확장자 꼭 있어야 함


```python
%%writefile dsm.py 

# magic command 이용해 모듈로 사용할 파일 만들기


    #변수

var=1234

    #함수

def disp1(s):
    print("disp1: ",s)
    
def disp2(s):
    print("disp2:",s)
    
def disp3(s):
    print("disp3:",s)

    #클래스   

class Calc:
    
    def plus(self, *args):
        return sum(args)
```

    Overwriting dsm.py
    

모듈 호출 - import 모듈명


```python
import dsm
```


```python
%whos # 모듈만 불러왔고, 모듈 내 변수, 함수, 클래스는 호출이 되지 않은 상태
```

    No variables match your requested type.
    

모듈 사용


```python
dsm.var
```




    1234




```python
dsm.disp1("test")
```

    disp1 test
    


```python
cal=dsm.Calc()
```


```python
cal.plus(1,2,3)
```




    6



모듈 내 일부 함수만 호출 - from 모듈명 import 함수명


```python
from dsm import disp1, disp2
```


```python
%whos
```

    Variable   Type        Data/Info
    --------------------------------
    disp1      function    <function disp1 at 0x00000000036E5AE8>
    disp2      function    <function disp2 at 0x0000000006E56048>
    dsm        module      <module 'dsm' from 'C:\\U<...>e\\Park\\Python\\dsm.py'>
    


```python
disp1("test1"), disp2("test2") 
```

    disp1:  test1
    disp2: test2
    




    (None, None)




```python
# disp3("test3") -> 호출되지 않은 disp3 함수 사용 불가
```


```python
%reset
```

    Once deleted, variables cannot be recovered. Proceed (y/[n])? y
    

모듈 내 모든 변수,함수,클래스 호출


```python
from dsm import *
```


```python
% whos # 모듈 내 모든 변수, 함수, 클래스가 호출됨.
```

    Variable   Type        Data/Info
    --------------------------------
    Calc       type        <class 'dsm.Calc'>
    disp1      function    <function disp1 at 0x00000000036E5AE8>
    disp2      function    <function disp2 at 0x0000000006E56048>
    disp3      function    <function disp3 at 0x0000000006E561E0>
    var        int         1234
    

## Package
- 디렉토리와 모듈로 이루어져 있음.
- 디렉토리 안에는 `__init__.py` 파일이 있어야 하는데 python 3.3 이후엔 없어도 동작 됨.
    - 그래도 호환성을 위해 `__init__.py` 파일을 무조건 넣어준다고 보면 됨.

디렉토리 만들기


```python
!mkdir school
```


```python
!mkdir school\dss
```


```python
!mkdir school\web
```


```python
!tree school 
```

    Local Disk 볼륨에 대한 폴더 경로의 목록입니다.
    볼륨 일련 번호는 9EFF-A5BF입니다.
    C:\USERS\HYEJEONG KIM\FC_DSS\NOTE\PARK\PYTHON\SCHOOL
    ├─dss
    └─web
    


```python
# 각 디렉토리에 __init__.py 파일 추가

!touch school\dss\__init__.py
!touch school\web\__init__.py
```


```python
!tree school # 깔아야 보임..
```

    매개 변수가 너무 많습니다 - #
    

모듈 만들기


```python
%%writefile school/dss/data.py

# dss 디렉토리에 data.py 안에 아래 코드가 들어가는 것


def plus(*args):
    return sum(args)
```

    Writing school/dss/data.py
    


```python
%%writefile school/web/url.py

def make(url):
    protocol="http://"
    return url if url[::7]==protocol else "http://" + url 
```

    Writing school/web/url.py
    


```python
!tree school
```

    Local Disk 볼륨에 대한 폴더 경로의 목록입니다.
    볼륨 일련 번호는 9EFF-A5BF입니다.
    C:\USERS\HYEJEONG KIM\FC_DSS\NOTE\PARK\SCHOOL
    ├─dss
    └─web
    

모듈 호출 
- 디렉토리나 모듈은 .으로 구분
- 호출 시엔 항상 모듈명이 제일 마지막에 있어야 함.


```python
import school.web.url # url 모듈 호출
```


```python
school.web.url.make("google.com") # 모듈 내 함수 사용
```




    'http://google.com'




```python
import school.web.url as url # 복잡한 것은 as 별명으로 지정해서 씀.
```


```python
url.make("fastcampus.com")
```




    'http://fastcampus.com'




```python
%reset
```

    Once deleted, variables cannot be recovered. Proceed (y/[n])? y
    


```python
%whos
```

    Variable   Type      Data/Info
    ------------------------------
    url        module    <module 'school.web.url' <...>rk\\school\\web\\url.py'>
    


```python
import sys
```


```python
for path in sys.path:
    print(path)
```

    
    C:\ProgramData\Anaconda3\python36.zip
    C:\ProgramData\Anaconda3\DLLs
    C:\ProgramData\Anaconda3\lib
    C:\ProgramData\Anaconda3
    C:\ProgramData\Anaconda3\lib\site-packages
    C:\ProgramData\Anaconda3\lib\site-packages\win32
    C:\ProgramData\Anaconda3\lib\site-packages\win32\lib
    C:\ProgramData\Anaconda3\lib\site-packages\Pythonwin
    C:\ProgramData\Anaconda3\lib\site-packages\IPython\extensions
    C:\Users\Hyejeong Kim\.ipython
    
