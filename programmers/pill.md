>## 기둥과 보(카카오2020)   
>처음에는 행렬로 나타내고, 기존의 1x1행렬을 채우는 것이 아니라, 선을 채운다고 생각해서 혼동이 왔다.   
>다시 생각해보니,굳이 선, 면으로 생각하지 않고 하면 되는 문제였다.    

**시뮬레이션 문제로 기둥과 보를 설치하는 조건을 함수로 만들어서 충족하면 추가/삭제하도록 만듬.**   

<br>

```python
def solution(n, build_frame):
    answer = []
    for frame in build_frame:
        x, y, pil, inst = frame
        if inst == 0:
            answer.remove([x,y, pil])  ---> 먼저 삭제하고 
            if not check(answer):    ---> 조건을 만족시키지 못하면, 다시 추가.
                answer.append([x,y,pil])     
        if inst == 1:
            answer.append([x,y,pil])  ---> 먼저 추가하고
            if not check(answer):   ---> 조건을 만족시키지 못하면, 다시 추가.
                answer.remove([x,y,pil])               


    return sorted(answer)


def check(answer):
    for x, y, pil in answer:
        if pil == 0:
            if y == 0 or [x, y-1, 0] in answer or [x-1, y, 1] in answer or [x,y,1] in answer:
                continue
            return False
            
        elif pil == 1:
            if [x, y-1, 0] in answer or ([x-1, y, 1] in answer and [x+1, y, 1]) in answer or \
            [x+1, y-1, 0] in answer:
                continue
            return False
    return True
    
```
