from itertools import combinations
import collections


def solution(orders, course):
    answer = []
    
    # 메뉴 개수를 중심으로 반복문 진행.    
    for i in course:
        temp = []
        for order in orders:
            
            # 손님마다 시킨 메뉴의 순서가 다를 수 있기 때문에, 오름차순으로 정렬을 해준다.
            # 조합을 이용해서 경우의 수 계산.
            temp += combinations(sorted(order), i)
        
        
        # most_common을 이용해서 많이 나온 순으로 정렬한다.
        result_temp = collections.Counter(temp).most_common()
        
        # 조건 (최소 한 번 이상 주문이 된 음식 & 최대로 많이 주문된 음식)
        answer += [''.join(a) for a, b in result_temp if b > 1 and b == result_temp[0][1]]
    
    answer.sort()
    
    
    return answer


