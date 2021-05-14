>## 특정 거리의 도시 찾기 (백준 18352)   
>#### bfs알고리즘을 이용해서 이동하는 노드에 계속해서 거리를 더해간다.   
>#### 노드의 개수가 300,000개이고, 간선의 개수도 1,000,000이므로 bfs로 해결 가능하다.   

<br>

**중요한 건, 출발 도시는 거리를 0으로 생각해야 된다.(이것 때문에 오래 걸림)**   

**처음 나온 도로의 정보를 그래프로 바꾼다.**   

<br>

```python
N, M, K, X = map(int,input().split())

# 도로의 정보를 그래프로 바꾸는 과정 (0번 도시는 없기 때문에, 길이를 하나 더 추가한다.)
road = [[] for _ in range(N+1)]

for _ in range(M):
    s, e = map(int,input().split())
    road[s].append(e)


q = deque([X])

# 모든 도시의 거리를 -1로 초기화
dist = [-1] * (N+1)

# 하지만 주어진 현재 도시 정보로 현재 도시는 거리를 0으로
dist[X] = 0


# bfs 
while q:
    tmp = q.popleft()
    for i in road[tmp]:
        if dist[i] == -1:
            dist[i] = dist[tmp] + 1
            q.append(i)
    

ans = False
for idx,i in enumerate(dist):
    if i == K:
        print(idx)
        ans = True

if not ans:
    print(-1)
       
```
