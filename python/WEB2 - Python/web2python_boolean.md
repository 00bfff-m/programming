# boolean

```{r}
print(True)
print(False)
#Expression
print(1+1) #숫자를 표현하는 표현식
print('Hello '+'world') #문자를 표현하는 표현식

#Comparison operator(비교 연산자)
print(1==1)
print(1<2)
print(2<1)

#Membership operator
print('world' in 'Hello world')

import os.path
print(os.path.exists('boolean.py')) #boolean.py라는 파일이 존재하는가?

#자료형에 요솟값이 있을 경우 참, 없으면 거짓
a = [1,2,3,4]
while a: #a가 True일 동안
    print(a.pop()) #리스트의 마지막 요소를 하나씩 꺼낸다.

print(bool('babo'))
print(bool(''))
print(bool(0))
print(bool(3))
```
