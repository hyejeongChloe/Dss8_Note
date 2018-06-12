
# Class
- 변수와 함수들을 묶은 사용자 정의 데이터 타입 (커스텀 데이터 타입)
- 객체지향을 구현하기 위해 만들어진 개념 (실제 세계를 모델링)
    - 다형성, 캡슐화, 추상화, 상속 등의 특징이 있음.
- 구조, 생성자, 상속, 다중상속, super, getter & setter, is a / has a, magic method
- 클래스는 도면, 청사진, 객체는 실제 물건! 
- 클래스를 이용해서 객체를 만들어야 클래스에 정의된 함수나 변수를 사용할 수 있음.
    - 함수에선 호출을 해주어야 하듯, 클래스는 객체화 해야 사용 가능.
    
```
class A:
    method - a,b,c
obj = A()    - 객체화를 해주면
obj.a(), obj.b()      - 이제 class 안에 method 사용 가능
```

## 1. 구조 (Structure)

### 1.1 클래스 선언과 객체

#### 1) 선언


```python
# 계산기 클래스 Calculator 만들기

class Calculator:
    
    def setdata(self, num1, num2): # self를 이용하여 변수 할당, def를 이용하여 함수 선언
                                    # 함수 선언 시 첫 번째 parameter에 항상 self를 넣어야 함!
                                    # self는 객체 자신
                                    # 여기서는 self안에 객체 cal이 들어가는 것.
        self.num1=num1
        self.num2=num2
        self.result=0 # 변수로는 num1, num2, result가 있는 것
    
    def plus(self): # 계산기의 plus 기능 추가 
        return self.num1 + self.num2 # self.num을 해야 설정한 num들을 불러올 수 있음
    
    def minus(self):
        self.result=self.num1 - self.num2  # 리턴값은 없고 minus한 값을 result에 다시 저장      
```

#### 2) 객체화


```python
cal=Calculator() # Calculator 클래스를 객체 cal에 저장(객체 생성) -> 메모리에 올라가 이제 사용 가능
```


```python
cal.setdata(1,2) # 객체의 함수에 접근->호출->실행. 1, 2라는 초기값 설정
```


```python
cal.plus() # 객체의 plus 함수에 접근하여 초기값 1, 2를 넣고 함수 실행
```




    3




```python
cal.minus() # minus 함수는 return값이 없어서 아무것도 안나옴.
```


```python
cal.num1, cal.num2, cal.result # 객체의 변수에 접근.
                        # cal.result에 minus가 들어갔으니까 이렇게 하면 결과 볼 수 있음.
```




    (1, 2, -1)




```python
# 다른 객체에 같은 클래스를 저장하면 서로 다른 메모리 사용.

# cal2=Calculator() 와 cal1=Calculator()
```


```python
# 클래스로 객체를 생성 후 사용 (일반적 케이스)

cal=Calculator()
cal.setdata(5,6)
cal.num1, cal.num2
```




    (5, 6)




```python
# 클래스에 바로 접근 - (클래스명).(함수명)((obj),parameter1,parameter2) (이런 식으론 안 쓰긴 함.)

Calculator.setdata(cal,7,8) # 클래스의 함수의 self parameter로 어떤 객체를 넘길지 정해줘야 함!
                            # 여기서 객체 cal을 쓴 것.
cal.num1, cal.num2
```




    (7, 8)



## 2. 생성자(Constructor)
- 클래스가 객체가 될 때, 변수의 초기값을 설정해주는 역할
- `__init__` 이름으로 함수를 선언
- 클래스가 객체가 될 때, `__init__()` 함수를 먼저 실행해줌
- 객체를 만들 때 자동으로 실행됨. 
- 생성자를 선언 후 초기값이 없이 객체를 만들면, 객체를 만들 때 에러가 남.
    - 생성자를 선언하지 않았을 땐, 객체는 생성되고(메모리 할당) 초기값이 없이 함수 실행 시 그 때 에러가 남.
    - 생성자를 사용하는 이유: 메모리 절약
- 생성자 없을 때 객체화: obj=A()
- 생성자 있을 때 객체화: obj=A(초기 변수)
    - 변수를 변경하고 싶을 땐 setdata 사용: obj.setdata(변수)


```python
class Calculator2:
    
    def __init__(self, num1, num2=5): # __init__ 으로 함수를 작성하여 생성자 사용
                                    # 생성자 parameter에 default parameter를 넣어줄 수도 있음. 
        self.num1=num1 
        self.num2=num2
        self.result=0 
    
    def setdata(self, num1, num2): # setdata가 없는게 아님! 변수 변경 시 사용
        self.num1=num1
        self.num2=num2
        self.result=0 
        
    def plus(self):
        return self.num1 + self.num2 
    
    def minus(self):
        self.result=self.num1 - self.num2  
```


```python
# 생성자 사용 안 한 경우  

# cal=Calculator() - 객체는 생성됨. (이 순간에 메모리 할당)
# cal.plus()  - error point
                # cal.setdata(1,2)와 같이 사전 초기값 설정 없이 함수를 실행하면, 함수 실행 시 에러가 남.
```


```python
# 생성자 사용 시

# cal2=Calculator2() - error point
                # 생성자가 선언되어 있는 클래스는 초기에 변수가 선언되지 않으면 아예 객체가 만들어지지 않음.
```


```python
cal2=Calculator2(1,2) # 올바른 사용 예시!
```


```python
cal2.plus()
```




    3




```python
cal3=Calculator2(1) # default parameter num2=5 이용 시
```


```python
cal3.plus()
```




    6



## 3. 상속(Inheritance)
- 클래스의 기능을, 새로 만드는 클래스에서 사용하고 싶을 때 상속이라는 기능을 이용
- 파이썬에서는 단일 상속과 다중상속 모두 사용 가능

```
class iphone1:
    method - call, send_sms

class iphone2:
    method - wifi

가 있을 때 iphone2가 call, send_sms, wifi 기능 모두 가지게 하고 싶을 때

class iphone2(iphone1):     - iphone1(부모)의 기능을 상속받는 것!
    method - wifi
```

### 3.1 다형성 (overriding, overloading)

- overriding - 기존에 있는 기능을 덮어 씌워서 새로운 기능으로 만드는 것 (함수 재정의)
-  overloading - 같은 이름의 함수를 호출하지만, 파라미터의 개수가 다르면 다른 기능을 하는 개념
    - 여러 다른 기능들을 하나의 이름의 함수로 묶고 싶을 때 overloading 사용


```python
# python에서는 overloading이 지원이 안 되기 때문에 default parameter를 이용!

def test(num=None):
    if num is None:
        # code1
        return 10
    #code2
    return num
```


```python
test() # 파라미터가 없으면 code 1 실행
```




    10




```python
test(5) # 파라미터가 있으면 code 2 실행
```




    5



### 3.2 단일상속


```python
# Calculator2 클래스를 상속 받아 나누기 기능을 추가한 improvedCalculator class 만들기

class improvedCalculator(Calculator2):
    
    def div(self):
        return self.num1 / self.num2
```


```python
iCal=improvedCalculator(4,2) # 부모인 Calculator2는 생성자가 선언되어있기 때문에 초기값과 함께 객체화
```


```python
iCal.div()
```




    2.0




```python
# starcraft

class Human:
    
    def __init__(self):
        self.health=40 # 1) 체력 디폴트값 40
    
    def set_health(self, value): # value는 __init__에서 선언된 게 아니라, set_health 함수에서만 사용되는 변수
        self.health += value # 체력이 오르거나 떨어지는데
        if self.health > 40:
            self.health = 40 # 아무리 힐을 해줘도 max인 40 이상으론 안 올라가도록        
```


```python
class Marin(Human): # Human의 두가지 기능을 상속 받게 됨
    
    def __init__(self):
        self.health=40 
        self.attack_power=5
        self.kill=0
    
    def attack(self, target): # 공격대상인 target 변수 지정
                                # 마찬가지로 attack 함수 내에서만 쓰이는 변수
        target.set_health(-self.attack_power)  # 상속받았기 때문에 set_health 함수 사용 가능
                                                              
        if target.health<=0:
            print('die')
            self.kill+=1 # self의 킬 수 증가 (target의 kill이 아님!)
        else:
            print('alive [health:{}]'.format(target.health))
```


```python
m1, m2 = Marin(), Marin() # 마린 두명 객체화
```


```python
m1.health, m2.health, m1.kill # 처음엔 health가 둘다 40, kill수는 0
```




    (40, 40, 0)




```python
m1.attack(m2) # attack 함수 호출
```

    alive [health:35]
    


```python
# 코드 실행 순서
   
# class Marin(Human): 
    
#     def __init__(self):
#         self.health=40 
#         self.attack_power=5
#         self.kill=0
    
#     def attack(m1, m2):     - 1) 객체화 후 m1.attack(m2) 호출 시 m1이 self에, m2가 target이 됨.
#         m2.set_health(-5)     - 2) 부모 클래스 human의 set_health 함수 호출 
#                                    m1.attack_power는 5                                     

#   ----------------------------------
#     *def set_health(m2, -5):      - 3) m2가 self에, value는 -5가 됨.
#         m2.health += -5          - 4) m2.health가 5씩 감소 (attack 함수 실행할 때마다)
#         if m2.health > 40:
#             m2.health = 40 
#   ----------------------------------

#         if m2.health<=0:     - 5) m2.health > 0이면, 
#             print('die')     - 7) m2.health <= 0이 되면, 'die'가 출력 되고
#             m1.kill+=1      - 8)  m1.kill이 1 올라감
#         else:
#             print('alive [health:{}]'.format(target.health))     - 6) 'alive [health: m2.health]' 가 출력됨.
```


```python
class Medic(Human):
    
    def __init__(self):
        self.health=20
        self.heal_power=6
    
    def heal(self,target):
        target.set_health(self.heal_power) # heal_power만큼 체력 높이기
        print("health : ", target.health)
```


```python
m3, medic = Marin(), Medic()
```


```python
m1.health, m3.health
```




    (40, 40)




```python
m3.attack(m1) # m3이 m1을 공격
```

    alive [health:30]
    


```python
medic.heal(m1) # medic이 m1의 체력을 6만큼 채워주기 
```

    health :  36
    

## 4. 다중 상속

```
class galaxy:
    method - game

class galaxy2(iphone1, galaxy):
    method - show_image
    
galaxy2 - call, send_sms, game, show_image 기능을 가지게 됨

```


```python
# Human, Korean, Indian - 클래스
# Jin(Human, Korean), Anchal(Human, Indian) - 다중 상속

# 각 클래스 생성

class Human:
    
    def walk(self):
        print("walking")
        
class Korean:
    
    def eat(self):
        print("eat kimchi")

class Indian:
    
    def eat(self):
        print("eat curry")
```


```python
# 다중 상속받기

class Jin(Human, Korean):
    
    def skill(self):
        print("Coding")
        
    # overiding (상속 받은 함수를 재정의) - jin은 korean이지만 noodle을 먹는다
    
    def eat(self):
        print("eat noodles")
    
class Anchal(Human, Indian):
    
    def skill(self):
        print("English")
        
    # overiding & overloading
    
    def eat(self, place=None):
        if place is None:
            print("eat curry")
        else:
            print("eat curry in the", place)
```


```python
j=Jin()
a=Anchal()
```


```python
j.walk()
j.eat() # overiding 결과
j.skill()
```

    walking
    eat noodles
    Coding
    


```python
a.walk()
a.eat("seoul") # overloading 결과
a.skill()
```

    walking
    eat curry in the seoul
    English
    


```python
# Quiz) 야구선수 정보를 가지고 선수별 클래스 만들기.
# 클래스에 타율을 구하는 함수 추가

# 김선민(ksm) - 타석:476, 안타:176
# 박건우(pkw) - 타석:483, 안타:177
# 박민우(pmw) - 타석:386, 안타:141

class Player:
    
    def __init__(self,ab,hit): # 타석 ab 안타 hit 변수 지정
        self.ab=ab
        self.hit=hit
    
    def avg(self):
        return round(self.hit / self.ab, 3) # 소수점 n번째 자리까지 나타내주는 round 함수
```


```python
ksm = Player(476,176)
pkw = Player(483, 177)
pmw = Player(386, 141)
```


```python
ksm.avg(), pkw.avg(), pmw.avg()
```




    (0.37, 0.366, 0.365)



## Super
- 클래스를 상속받을 때 부모 클래스의 생성자 변수들을 받아오는 함수


```python
class Human:
    
    def __init__(self):
        self.health=40 
        
    def set_health(self, value):
        self.health += value 
        if self.health > 40:
            selfhealth = 40         
```


```python
class Marin(Human): # 클래스를 상속받을 때,
    
    def __init__(self):
        
                                # self.health=40라고 쓰면 overiding 할 때마다 써줘야하는 번거로움
        super(Marin,self).__init__() # 그럴 때 super 이용하여 생성자 변수를 받아옴
        
        self.attack_power=5
        self.kill=0
    
    def attack(self, target): 
        target.set_health(-self.attack_power) 
                                               
        if target.health<=0:
            print('die')
            self.kill+=1 
        else:
            print('alive [health:{}]'.format(target.health))
```


```python
# 다이아몬드 상속

# B(A), C(A), D(B,C)라 하고 init으로 가져오면
# D() - A,A (A 두번 호출 됨)

class A:
    def __init__(self):
        print("A.__init__")
    

class B(A):
    def __init__(self):
        print("B.__init__")
        A.__init__(self) # B가 A를 상속받음
    

class C(A):
    def __init__(self):
        print("C.__init__")
        A.__init__(self) # C가 A를 상속받음

class D(B,C): # D <- B <- A & C <- A
    def __init__(self):
        print("D.__init__")
        B.__init__(self)  # B와 A 모두 가져옴
        C.__init__(self)  # C와 A 모두 가져옴 => A가 중복됨.

D()
```

    D.__init__
    B.__init__
    A.__init__
    C.__init__
    A.__init__
    




    <__main__.D at 0x6ca4630>




```python
# super 사용하면 D() 호출 시 A를 중복하지 않고 A,B,C 가져옴 (Super를 쓰는 이유)

class A:
    def __init__(self):
        print("A.__init__")
    

class B(A):
    def __init__(self):
        print("B.__init__")
        super(B,self).__init__()

class C(A):
    def __init__(self):
        print("C.__init__")
        super(C,self).__init__()
        
class D(B,C): # D <- B <- C : super 이용시 D 호출시 B를 가져오고, B 호출시 C를 가져옴
    def __init__(self):
        print("D.__init__")
        super(D,self).__init__() # B와 C init을 두번 쓰지 않고 super(D,self)로 한번만 씀.
        
D()
```

    D.__init__
    B.__init__
    C.__init__
    A.__init__
    




    <__main__.D at 0x6a8f978>




```python
class A:
    def __init__(self):
        print("A.__init__")
        
class B:
    def __init__(self):
        print("B.__init__")
        
class C(A,B): # C <- A <- B
    def __init__(self):
        print("C.__init__")
        super(C,self).__init__()  # 여기에 C를 쓰면 C의 위에 있는 A가, 
                                    # A를 쓰면 A의 위에 있는 B가 가져와짐. 
                                    # 그래도 보통 C를 씀.. 아무것도 안쓰면 알아서 C를 가져오고

C()
```

    C.__init__
    A.__init__
    




    <__main__.C at 0x6ca49b0>



## Getter & Setter
- 객체의 내부 변수에 접근할 때, 바로 접근하지 않고 특정 함수를 이용해서 특정 코드를 거쳐 접근할 수 있도록 하는 방법
     - 예를 들어 class 안에 숫자만 넣을 수 있도록 하게 하고 싶을 때, getter/setter 이용해 숫자만 넣어지게 하는 함수를 이용
- property, decorator 두 가지 방법으로 구현



```python
# Property

class Person1:
    
    def __init__(self,input_name1,input_name2):
        self.hidden_name1=input_name1
        self.hidden_name2=input_name2
        
    def disp_name1(self): # getter 1
        print("disp_name1")
        return self.hidden_name1.upper()
    
    def disp_name2(self): # getter 2
        print("disp_name2")
        return self.hidden_name2
    
    def set_name1(self, input_name): # setter 1
        print("set_name1")
        self.hidden_name1=input_name

    def set_name2(self, input_name): # setter 2
        print("set_name2")
        self.hidden_name2=input_name
    
    # property의 object 설정. 변수 선언하듯
    
    name1=property(disp_name1,set_name1) # 앞에 getter 함수, 뒤에 setter 함수 넣기
    name2=property(disp_name2,set_name2)
```


```python
p=Person1("ksm","kek") # 각각 hidden_name 1,2에 들어감
```


```python
# 실제로 외부에서 접근하는 건 name1,2 (hidden_name1,2는 숨어있고)

p.name1, p.name2 # getter 함수 호출 = disp_name 동작 -> hidden_name 즉 input_name 출력
```

    disp_name1
    disp_name2
    




    ('KSM', 'kek')




```python
p.name1="ppp" # 새로운 값을 집어넣을 때는 setter가 호출 되도록 되어있음 -> set_name1 동작
```

    set_name1
    


```python
# Decorator

class Person2():
    def __init__(self,input_name):
        self.hidden_name=input_name
    
    @property
    def name(self): # getter
        print("getter")
        return self.hidden_name.upper()
    
    @name.setter
    def name(self, input_name): # setter
        print("setter")
        self.hidden_name="Mr. "+input_name
```


```python
p2=Person2("park")
```


```python
p2.name="kim" # setter
```

    setter
    


```python
p2.hidden_name # hidden_name에 직접 접근 
```




    'Mr. kim'




```python
p2.name # getter - setter 호출 해서 hidden_name을 Mr kim 으로 바꿔놓은 상태에서 getter 호출한 결과
```

    getter
    




    'MR. KIM'



## Private
- 위의 코드와 같이 생성자 함수에 변수를 선언하면 객체를 만들었을 때 getter를 통하지 않고 접근 가능
- class 내부 변수에 다이렉트로 접근하지 못하게 하고 싶을 때 사용
- 맹글링을 이용해서 구현 (변수명 앞에 `__`를 붙여서)
- 완벽한 방법은 아님


```python
p2.hidden_name # 소문자로 못가져오게 막고 싶을 때 이 부분을 private으로 설정가능 (다음 설명)
```




    'Mr. kim'




```python
class Person3:
    
    def __init__(self,input_name):
        self.__hidden_name=input_name # hidden_name 앞에 __
    
    @property
    def name(self): 
        print("getter")
        return self.__hidden_name.upper()
    
    @name.setter
    def name(self, input_name):
        print("setter")
        self.__hidden_name="Mr. "+input_name
```


```python
p3=Person3("Lee")
```


```python
# p3.hidden_name - private 이용시 에러남. 접근 불가
```


```python
p3.name
```

    getter
    




    'LEE'




```python
# 완벽하진 않은 이유 - _클래스명을 변수 앞에 붙이면 다이렉트 접근 가능

p3._Person3__hidden_name
```




    'Lee'



##### private funtion
- 클래스 내에서만 사용되는 함수의 이름 중복이 우려될 때 사용
- 사용하는 일은 거의 없음.


```python
class A:
    def __test(self): # 함수도 맹글링해서 priviate function으로 만들 수 있음.
        print("test")
```


```python
a=A()
```


```python
# a.__test() -> 에러 발생
```

## is a / has a
- is a : A is a B (A는 B이다)
    - 상속을 이용해서 구현
- has a : A has a B (A는 B를 가지고 있다.)
    - 객체를 이용


```python
# is a 

class B:
    def __init__(self, name, email):
        self.name=name
        self.email=email
        
class A(B):
    def about(self):
        print(self.name, self.email)
```


```python
person=A("doojin","pdj121@gmail.com")
```


```python
person.about()
```

    doojin pdj121@gmail.com
    


```python
# has a

class Name:
    
    def __init__(self,name):
        self.name=name
        
class Email:
    
    def __init__(self,email):
        self.email=email
        
class Person:
    
    def __init__(self, name, email): # self.name 같은 객체가 들어오고(가지고 있는 것) 거기에 접근
        self.name=name
        self.email=email
        
    def about(self):
        print(self.name.name, self.email.email)
```


```python
name=Name("Park")
email=Email("pdj121@gmail.com")
```


```python
person=Person(name,email) # 각 class를 선언한 객체를 초기변수로 가져옴
person.about()
```

    Park pdj121@gmail.com
    

## Magic(Special) Method
- 비교: `__eq__` (==), `__ne__`(!=), `__lt__`(<),`__gt__`(>), `__le__` (<=), `__ge__`(>=)
- 연산: add (+), sub (-), mul(*), 마찬가지로 __ 필요
- `__repr__`,`__str__`, `__len__`
     - __str__ : print와 같이 객체에 대한 정보를 문자열로 출력할 때 사용 (사용자용)
            객체의 변수 값을 나열하는 형태로 표현
     - __repr__ : 객체에 대한 정보를 출력할 때 사용 (개발자용)
             클래스명, 생성자 변수 이름, 변수 값을 나타냄



```python
# eq

class Txt:
    
    def __init__(self,txt):
        self.txt=txt
        
    def equals(self,txt_obj):
        return self.txt.lower()==txt_obj.txt.lower() # 자기자신의 txt 변수와 obj 안에 있는 txt 변수가 소문자롭 변환했을 때 같은가?
```


```python
txt1=Txt("fastcampus")
txt2=Txt("fastCampus")
txt3=Txt("dataScience")
txt4=Txt("fastcampus")
txt5=txt1
```


```python
txt1.equals(txt2), txt1.equals(txt3)
```




    (True, False)




```python
txt1==txt2,txt1==txt3,txt1==txt4,txt1==txt5 # 주소값 비교
```




    (False, False, False, True)




```python
# __eq__ 사용

class Txt:
    
    def __init__(self,txt):
        self.txt=txt
        
    def __eq__(self,txt_obj): # __eq__ 사용
        return self.txt.lower()==txt_obj.txt.lower() 
```


```python
txt1=Txt("fastcampus")
txt2=Txt("fastCampus")
txt3=Txt("dataScience")
txt4=Txt("fastcampus")
txt5=txt1
```


```python
txt1==txt2,txt1==txt3,txt1==txt4,txt1==txt5 # 오버라이딩?
```




    (True, False, True, True)




```python
# __ne__

ls=["a","b","a","d","a"]
ls.remove("a") # "a"가 하나밖에 안 지워짐.
ls
```




    ['b', 'a', 'd', 'a']




```python
ls=["a","b","a","d","a"]
s="a"
result=[data for data in ls if data !=s] # "a"가 아닌 요소만 담기
result
```




    ['b', 'd']




```python
# filter와 __ne__를 이용해 구현 

ls=["a","b","a","d","a"]
s="a"
list(filter(s.__ne__,ls)) # s.__ne__가 함수임! self != value가 filter의 조건이 되는 것
```




    ['b', 'd']




```python
# __add__

int.__add__??
```


```python
class Number:
    
    def __init__(self,num):
        self.num=num
        
    def __add__(self, other):
        return self.num + other.num
```


```python
n1=Number(3)
n2=Number(2)
n1+n2
```




    5




```python
class Number:
    
    def __init__(self,num):
        self.num=num
        
    def __add__(self, other):
        return self.num - other.num # - 연산으로 수정
```


```python
n1=Number(3)
n2=Number(2)
n1+n2
```




    1




```python
class Number2:
    
    def __init__(self,num):
        self.num=num
        
    def __add__(self, other):
        return self.num * other.num # * 연산으로 수정
```


```python
n1=Number(3)
n2=Number2(2)
n1+n2
```




    1




```python
n1=Number2(3)
n2=Number2(2)
n1+n2
```




    6




```python
# __str__ , __reor__

class Number:
    
    def __init__(self,num):
        self.num=num
        
    def __str__(self): # print와 같이 객체에 대한 정보를 문자열로 출력할때 사용 (사용자용), 객체의 변수 값을 나열하는 형태로 표현
        return str(self.num)
    
    def __repr__(self):
        return str("Number(num=" + str(self.num) + ")") # 객체에 대한 정보를 출력할때 사용 (개발자용), 
                                                        # 클래스명, 생성자변수이름, 변수 값 표현
```


```python
n=Number(5)
```


```python
print(n) # 5를 string으로 출력
```

    5
    


```python
n
```




    Number(num=5)




```python
n2 = Number(num=5)
```


```python
n2
```




    Number(num=5)


