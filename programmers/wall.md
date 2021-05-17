>## 외벽 점검 (카카오 2020)
>#### 처음에 원형 꼴로 조건을 나타내서 일단 펼쳐서 풀려고 시도.   
>#### 어디서 부터 시작할지 시계방향으로 갈지 반 시계 방향으로 갈지 고민.     

<br> 

**순열을 사용해서 모든 순서를 고려한다음, 모든 경우의 수를 다 계산**     

```python
def solution(n, weak, dist):
    # 파손된 부분의 개수 
    length = len(weak)
    
    # 원형을 일자로 펴는 작업
    for i in range(length):
        weak.append(weak[i]+n)
    
    # min을 쓰기위한 밑작업
    ans = len(dist) + 1
    
    # 첫 파손 부분부터 마지막 파손부분까지 순서대로 넣어본다.
    for i in range(length):
        
        # 고치러 갈 사람의 조합 모두 생각.
        for person in list(permutations(dist, len(dist))):
            cnt = 1
            
            # 고치러 간 사람이 갈 위치
            loc = weak[i] + person[cnt - 1]
            
            # 처음 간 사람이 가고도 파손된 부분이 남으면 더 보내고,
            # 그게 아니라면 끝낸다.
            for idx in range(i, i+length):
                if loc < weak[idx]:
                    cnt += 1
                    if cnt > len(dist):
                        break
            
                    loc = weak[idx] + person[cnt-1]
            ans = min(ans, cnt)
    if ans > len(dist):
        return -1
    return ans
```
