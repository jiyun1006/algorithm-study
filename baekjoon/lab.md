>## 연구소 문제 (백준 14502)   
>#### 완전탐색과 DFS가 섞여 있는 듯한 문제, 처음에 어떻게 벽을 설치할지에서 막힘.   
>#### 나머지 부분에서는 dfs를 이용해서 해결 

<br>

```python
...<생략>...

# 탐색 문제에서 주로 하는 방향 리스트 설정   
dx = [-1, 0, 1, 0]
dy = [0, 1, 0, -1]

result = 0


# 연구실에 바이러스 퍼트리는 함수
def fill_vir(x,y):

   
    for i in range(4):
        nx = x + dx[i]
        ny = y + dy[i]
        
        # 주위에 벽이아니고, 빈 공간일시에 바이러스를 퍼트린다.
        if nx >= 0 and ny >= 0 and nx < n and ny < m:
            if temp[nx][ny] == 0:
                temp[nx][ny] = 2
                fill_vir(nx, ny)     
 
 
# 안전지대 개수 세는 함수
def get_score():
    score = 0 
    for i in range(n):
        for j in range(m):
            if temp[i][j] == 0:
                score += 1
    return score
        

# 연구실을 탐색하며, 바이러스 퍼트리고, 벽 설치 해제를 반복
def dfs(cnt):
    global result
    
    # 벽이 3개 설치됐을 때, 임시 행렬에 연구소 모습 복사 후, 안전지대 개수 확인.
    if cnt == 3:
        for i in range(n):
            for j in range(m):
                temp[i][j] = lab[i][j]
        for i in range(n):
            for j in range(m):
                if temp[i][j] == 2:
                    fill_vir(i, j)
        result = max(result, get_score())
        return
    
    # 연구소에 벽 설치 해제 부분
    for i in range(n):
        for j in range(m):
        
            # 공간이 0 이라면, 벽 설치
            if lab[i][j] == 0:
                lab[i][j] = 1
                cnt += 1
                
                계속해서 벽 설치를 이어가며, 점수 체크 후, 해제하고 다른 공간에 설치
                dfs(cnt)
                lab[i][j] = 0
                cnt -= 1

               
```   
