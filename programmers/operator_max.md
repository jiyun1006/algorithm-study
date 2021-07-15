파이썬의 eval 메서드의 존재 덕분에 식을 상당히 간추릴 수 있었다.

처음에는 모든 기능을 하나하나 나눠서 풀려고 노력했지만, 식이 너무 길어지다보니, 혼동이 오게 되었다.

다른 사람의 풀이법을 보던 중, 가장 파이썬스럽게 푼 사람의 풀이를 보고,
비슷하게 풀어봤다.
리스트 컴프리헨션과 eval 메서드를 이용해서 상당히 간단하게 만들 수 있었다.

'''python
def solution(expression):
    answer = 0
    operator = [
        ["+", "-", "*"],
        ["+", "*", "-"],
        ["-", "+", "*"],
        ["-", "*", "+"],
        ["*", "+", "-"],
        ["*", "-", "+"]
    ]
    res = 0
    
    for oper in operator:
        res = int(cal(expression, oper, 0))
        answer = max(answer, abs(res))
    return answer


def cal(expression,oper, cnt):
    res= 0
    if cnt == 2:
        return str(eval(expression))
    
    if oper[cnt] == "+":
        res = eval('+'.join([cal(ex, oper, cnt+1) for ex in expression.split("+")]))
    if oper[cnt] == "-":
        res = eval('-'.join([cal(ex, oper, cnt+1) for ex in expression.split("-")]))
    if oper[cnt] == "*":
        res = eval('*'.join([cal(ex, oper, cnt+1) for ex in expression.split("*")]))
        
    return str(res)

'''
