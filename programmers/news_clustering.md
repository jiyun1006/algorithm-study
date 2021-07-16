### 뉴스 클러스터링


정규표현식과 중복되는 원소를 구하면 되는 문제.   

처음에 set을 이용해서 풀려고 했으나, set은 중복되는 원소를 다 지우기 때문에,   

문제가 생겼고, 리스트를 순회하면서 중복되는 개수를 구하는 방식으로 교집합을 구함.   


```python
import re

def solution(str1, str2):
    answer = 0
    # 소문자로 통일
    str1, str2 = str1.lower(), str2.lower()
    
    # 집합으로 만듬.
    str1 = make_set(str1)
    str2 = make_set(str2)
    
    
    # 모두 공집합일 경우
    if (not str1) &  (not str2):
        return 65536
    
    if len(str1) < len(str2):
        a = [str2.remove(i) for i in str1 if i in str2]
        
    else:
        a = [str1.remove(i) for i in str2 if i in str1]
    
    J = len(a)/len(str1+str2)
    
    answer = int(65536 * J)
    return answer


    
def make_set(string):
    length = len(string)
    temp = list()
    
    for i in range(length):
        temp_str = ""
        if i == (length - 1):
            break
        
        temp_str = string[i] + string[i+1]
        if temp_str.isalpha():    
            temp.append(temp_str)
            
    return temp
    
```
