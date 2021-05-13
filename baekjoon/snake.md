>## 뱀 (백준 3190번)   
>시뮬레이션 문제 유형으로, 문제 조건에 따라서 구현만 하면 된다.   
>문제는 맞았지만, 중간중간 구현 내용을 따로 함수로 만들면 가독성을 높일 수 있을 것 같다.   
 
<br>

**먼저 뱀이 지나다닐 보드판을 길이에 맞춰서 만든다. 그 다음에, 사과를 미리 보드판에 넣어둔다.**   

**뱀의 진행방향에 유의하며, 게임을 진행한다.**   

<br>

- 내가 푼 풀이   

<br>

```python
import heapq
N = int(input())
K = int(input())



# 보드판과 사과를 배치 (사과를 숫자 2로 나타낸다.)   
board = [[0] * N for _ in range(N)]
for _ in range(K):
    row, col = map(int, input().split())
    board[row-1][col-1] = 2


# 변환 조건 (시간, 방향)    
# 우선순위 큐 활용
heap = list()
L = int(input())
for _ in range(L):
    XC = input().split()
    heapq.heappush(heap, (int(XC[0]),XC[1]))


# 제일 빨리 오는 변환 횟수 받음.(우선순위 큐의 heappop을 이용해서 제일 낮은 시간을 빼낸다.)
change = heapq.heappop(heap)
time = change[0]
direction = change[1]


# 방향 설정 (index로 방향을 설정할 수 있게)
c_dir_list = ["R", "B", "L", "U"]
c_dir = 0  ---> 초기 방향 0 ("R")
c_time = 0 
distance = 1


# 뱀머리의 현재 위치
snake = [0,0]

# 뱀의 길이에 따라 차지하고 있는 보드 위치
snake_list = [[0,0]]


while 1:
    # 반복을 시작하고 바로 시간을 늘린다.
    c_time+=1          
    

    # 현재시간 - 1 과 방향 전환 시간이 같다면, 방향을 바꾼다.
    if c_time-1 == time:
        if direction == "L":
            c_dir -= 1
            if c_dir <= -1:
                c_dir = 3

        else:
            c_dir += 1
            if c_dir >= 4:
                c_dir = 0
        
        if heap:
            change = heapq.heappop(heap)
            time = change[0]
            direction = change[1]
    
    
    #진행방향에 따라 다르게 진행
    if c_dir == 0:
        snake[1] += 1
        
    elif c_dir == 1:
        snake[0] += 1
        
    elif c_dir == 2:
        snake[1] -= 1
        
    elif c_dir == 3:
        snake[0] -= 1
    
    
    #보드판을 벗어나거나, 뱀이 이미 차지하고 있는 부분이면, 반복문 파괴
    if snake[1] >= N or snake[1] < 0 or snake[0] >= N or snake[0] < 0 or board[snake[0]][snake[1]] == 1:
        break
    
    #사과에 도착하면, 길이를 늘리고, 차지하고 있는 자리 추가.
    if board[snake[0]][snake[1]] == 2:
        distance += 1
        snake_list.append([snake[0],snake[1]])
        for i in range(distance):
            board[snake_list[i][0]][snake_list[i][1]] = 1


    #사과가 아닌 빈땅에 도착하면, 뱀의 꼬리부분이 차지하고 있던 부분을 뺀다. 
    else:
        snake_list.append([snake[0],snake[1]])
        tmp = snake_list.pop(0)
        board[tmp[0]][tmp[1]] = 0
        for i in range(distance):
            board[snake_list[i][0]][snake_list[i][1]] = 1
        
        
    
print(c_time)
