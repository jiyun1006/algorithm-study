from collections import defaultdict

def solution(record):
    answer = []
    
    u_dict = defaultdict()
    result_temp = []
    
    
    # 분기점을 나눠서 최종적으로 uid에 대응하는 닉네임을 저장하는 딕셔너리를 만든다.
    for info in record:
        temp = info.split()
        if temp[0] == "Enter":
            u_dict[temp[1]] = temp[2]
            result_temp += [[temp[0], temp[1]]]
        elif temp[0] == "Change":
            u_dict[temp[1]] = temp[2]
        else:
            result_temp += [[temp[0], temp[1]]]
    
    # 이후, Enter Leave에 따라서 뒤의 문자열 구문을 다르게 해준다.
    for result in result_temp:
        answer.append(u_dict[result[1]] + "님이 " + enter_leave(result[0]))

    
    return answer


def enter_leave(word):
    return "들어왔습니다." if word == "Enter" else "나갔습니다."
        
