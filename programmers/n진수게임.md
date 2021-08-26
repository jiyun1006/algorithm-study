>### kakao n진수 게임(py)    

- divmod를 이용하면, n진수 문제를 쉽게 풀 수 있다.   
  (divmod는 나눗셈의 몫과 나머지를 한 번에 구해주는 메서드이다.)   

- '123456789ABCDEF' 를 기준으로 나머지를 인덱스 삼아서 숫자를 나열한다.   
  (기본적으로 n진수를 구하는 방법이다.)   

- 또한 n의 값과 튜브가 말해야 하는 개수인 t를 곱해서 이 수보다 더 적게 숫자 리스트를 만든다.   

```py
def solution(n, t, m, p):
    answer = ''
    num = 0
    ans_list = []
    while len(ans_list) < t*m:
        ans_list += list(change(num,n))
        num += 1
    for i in range(t):
        answer += ans_list[i*m+(p-1)]
        
    return answer

def change(num, n):
    string = '0123456789ABCDEF'
    
    a, b = divmod(num, n)
    if a == 0:
        return string[b]
    
    else:
        return change(a, n) + string[b]


```

