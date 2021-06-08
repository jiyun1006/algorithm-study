from collections import defaultdict
from itertools import combinations
from bisect import bisect_left


def solution(info, query):
    answer = []
    info = info_decom(info)
    
    for qr in query:
        
        # 마지막 점수 부분이 and 로 이어지지 않기 때문에, and를 공백으로 대체.
        qr = qr.replace('and ', '')
        qr = qr.split()
        
        # 앞의 조건문을 key로 만들고, 뒤의 점수를 value로 하는 딕셔너리 생성.
        query_key = qr[:-1]
        query_value = int(qr[-1])
        while '-' in query_key:
            query_key.remove('-')
            
        qr_key = ''.join(query_key)
    
        if not qr_key in info:
            answer.append(0)
        else:
            
            # bisect_left를 이용해서 기준 점수 밑의 개수 제거
            ans = info[qr_key]
            answer.append(len(ans) - bisect_left(ans,query_value))
        
    return answer


# info 배열 정보 분해하는 함수
def info_decom(info):
    
    info_dec = {}
    for i in info:
        information = i.split(' ')
        keys = information[:-1]
        value = int(information[-1])
        for n in range(5):
            combi = list(combinations(keys, n))
            for comb in combi:
                key = ''.join(comb)
                if info_dec.get(key) is None:
                    info_dec[key] = [value]
                else:
                    info_dec[key].append(value)
                
    for key in info_dec.keys():
        info_dec[key] = sorted(info_dec[key])
    return info_dec

