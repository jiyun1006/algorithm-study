>## 문자열 압축(2020카카오)   
 
<br>

- 내가 푼 풀이   

<br>

**python for문에서 반복 단위를 늘려가며 단위마다의 줄어드는 길이 확인**   

**얼만큼 줄어드는지에 대한 잘못된 코드로, 답이 안나옴**   

```python
for j in range(1,length+1):
    idx, cnt = 0, 0
    tmp = ''
    cnt2 = 1   ---> 반복 횟수를 저장하는 변수
    for i in range(0, len(s)+1, j):
        if tmp != s[idx:i]:
            if tmp and cnt2 > 1:   ---> 2번 이상 반복되었다면, 실행
                cnt += j*(cnt2-1)-1  ---> 압축을 해서 줄어드는 길이를 저장하는 변수
          
                cnt2 = 1
        if tmp == s[idx:i]:
            cnt2 += 1
        tmp = s[idx:i]
        idx = i   

    if cnt2 > 1:     ----> 남은 문자열 중, 줄어드는 길이 저장.
        cnt += j*(cnt2-1)-1            
    cnt_list.append(cnt)
```   

<br>

- 풀이   

**알고리즘 자체는 동일하나, 문자열 자체를 저장함으로써 줄어드는 길이에 대한 복잡함 해소.**   

```python
for j in range(1,length+1):
    idx, cnt = 0, 1
    tmp = s[0:j]
    tmp2 = ''
    for i in range(j, len(s), j):
        if tmp == s[i:i+j]:
            cnt += 1    ---> 반복횟수 기록.
        else:
            tmp2 += str(cnt) + tmp if cnt >= 2 else tmp     ---> 반복횟수가 2회 이상이면, 해당 문자열 저장.
            tmp = s[i:i+j]
            cnt = 1

    tmp2 += str(cnt) + tmp if cnt >= 2 else tmp   ---> 남은 문자열 처리
    answer = min(answer, len(tmp2))
```
