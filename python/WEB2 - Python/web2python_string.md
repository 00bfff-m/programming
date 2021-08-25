# string

## string 1
```
print("Life is too short, You need Python")
print("Python's favorite food is perl") #문자열 작은 따옴표가 포함되어 있을 경우
print('"Python is very easy." he says.') #문자열 큰 따옴표가 포함되어 있을 경우

#escape
print("Hell'o' \"w\"orld") #작은 따옴표를 문자 그대로 사용하고 싶을 때

#newline
print('H')
print('e')
print('l')
print('l')
print('o')
print('H\ne\nl\nl\no')

#docstring
print('''
H
e
l
l
o
''')

multiline = '''
Life is too short
you need Python
'''
print(multiline)
```

## string 2(Indexing, Slicing)
```
food = "Python's favorite food is perl"
say = '"Python is very easy." he says.'

print(food+say) #문자열 연산
print((food+'\n')*2) 

print(len(food))

#문자열  Indexing, Slicing
print(food[3]) #파이썬은 숫자를 0부터 센다.
print(food[-1]) #뒤에서 첫 번째 문자
print(food[-4:]) #슬라이싱을 할 때 끝번호에 해당하는 문자는 포함되지 않는다.
```

## string 3(formatting)
```
print("I eat %d apples" % 3) # %d(digit): 숫자 바로 대입
print("I eat %s apples" % "three") # %s(string): 문자열 바로 대입

number = 3
day = "three"
print("I eat %s apples, so I was sick for %s days" % (number, day)) #둘 이상의 값 넣기

print("Error is %d%%" %98) # 문자 '%' 넣기
print("%10s" %'hi') # 전체 길이 10개인 문자열 공간에서 대입되는 값을 오른쪽 정렬
print("%-10sjane" %'hi') # 전체 길이 10개인 문자열 공간에서 대입되는 값을 왼쪽 정렬

import math
a = math.pi
print("%0.4f" %a) #원주율 소수점 4째 자리까지

name = 'egoing'
age = 'one'
print('to '+name+'. Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim apple veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. '+name+' Duis aute irure dolor in '+age+' reprehenderit apple computer in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui '+name+' officia deserunt mollit anim id est laborum.')

#positional formatting
print('to {}. Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim apple veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. {} Duis aute irure dolor in {} reprehenderit apple computer in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui {} officia deserunt mollit anim id est laborum.'.format('egoing', 12, 'egoing', 'egoing'))

#Named placeholder
print('to {name}. Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim apple veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. {age:d} Duis aute irure dolor in {name} reprehenderit apple computer in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui {name} officia deserunt mollit anim id est laborum.'.format(name='egoing', age=12))

number = 3
day = "three"
print(f"I eat {number+1} apples, so I was sick for {day} days") #둘 이상의 값 넣기 + expression

d = {'number':3, 'day':'three'}
print(f"I eat {d['number']+1} apples, so I was sick for {d['day']} days") #딕셔너리 사용

print(f"{'hi':=^10}") #공백 채우기
import math
a = math.pi
print(f"{a:0.4f}") #소수점 나타내기
```
