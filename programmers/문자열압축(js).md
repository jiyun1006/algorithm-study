### kakao 문자열 압축(javascript)   

- python이 아닌 javascript로 문자열 슬라이싱을 해서 약간 어색했다.   

- js에서는 슬라이싱 메서드가 3개가 있다.   
  `str.substr(start, length)`, `str.slice(start, end)`, str.substring(start, end)`   

- 슬라이싱을 이용해서 주어진 조건에 따라 문자열을 나눈다.   

- 알고리즘 자체는 처음 풀었을 때와 달리진 점은 없다.   

- js에서는 python의 내장 라이브러리와 같은 기능을 잘 몰라서 삼항 연산자를 최대한 활용했다.   

```js
function solution(s) {
    let answer = s.length;
    const len = parseInt(s.length/2);
        
    for (let i=1; i<len+1; i++){
        let temp = "";
        let cnt = 1;
        let sub_str =  s.substr(0,i);
        for (let j=i; j < s.length; j+=i){
            const temp_str = s.substr(j,i);
            if (sub_str === temp_str){
                cnt++;
            }else{
                temp += (cnt > 1 ? cnt + sub_str : sub_str)
                sub_str = temp_str;
                cnt = 1;
            }
        }
        
        temp += (cnt > 1 ? cnt + sub_str : sub_str);
        answer = (temp.length < answer ? temp.length : answer)
    }
    
    
    return answer;
}
```
