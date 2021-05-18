>## 자물쇠와 열쇠 (2020카카오)   
>처음에 문제를 보고 적당한 구현 알고리즘을 떠올리지 못했다. 따라서 다른 사람의 알고리즘을 보고, 구현을 시도했다.   
>아직 완전탐색 문제들에 대한 경험 부족으로, 다양한 구현방법이 숙지가 안됨.   

<br>  

**기본적으로 문제에서 제공하는 자물쇠와 열쇠의 크기가 작기 때문에, 완전탐색으로 모든 리스트를 접근할 수 있다.   
(앞으로 시간복잡도, 공간복잡도에 대한 감을 키워야 할 듯.)**   

**또한 key의 원소를 이동시키는 것과 lock 리스트에 패딩을 줘서 더 넓은 범위에서 이동하는 행위가 같다.**   

**따라서 따로 만들 함수는 lock이 모두 1인지와, key를 90도 회전 시키는 함수이다.**   

<br>
 
*key를 90도 회전 시키는 함수*   
```python
def rotate(key):
    n = len(key)
    m = len(key[0])
    new_list = [[0]*n for _ in range(m)]

    for i in range(n):
        for j in range(m):
            new_list[i][j] = key[n-1-j][i]
    return new_list
```    

<br>

*lock이 1인지 확인하는 함수*   
```python
def check(lock):
    n = len(lock)
    m = len(lock[0])
    length = n//3

    for i in range(length, length*2):
        for j in range(length, length*2):
            if lock[i][j] != 1:
                return False
    return True
```    
<br>

*main 함수*    
```python
def solution(key, lock):
    answer = False
    n = len(lock)
    m = len(lock[0])

    big_lock = [[0]*3*n for _ in range(m*3)]  ---> padding 생성
    for i in range(n):
        for j in range(m):
            big_lock[i+n][j+n] = lock[i][j]    ---> padding을 포함한 list에 lock 넣기.

    for _ in range(4):
        key = rotate(key)
        for i in range(n*2):
            for j in range(n*2):
                for x in range(len(key)):
                    for y in range(len(key[0])):
                        big_lock[i+x][j+y] += key[x][y]  ---> padding에도 값을 더하고, lock부분에도 값을 더한다.
                if check(big_lock):
                    return True
                for x in range(len(key)):
                    for y in range(len(key[0])):
                        big_lock[i+x][j+y] -= key[x][y]   ---> 잘못된 key라면 더했던 값 빼기

    return answer
```

