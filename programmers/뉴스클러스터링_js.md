### 뉴스 클러스터링(javascript)

- javascript의 정규표현식읖 이용해서 문자열의 특수기호들을 정리했다.   
  (string.match 를 이용해서 특수문자를 검색)   

- 이후 처음에는 1번 문자열을 기준으로 2번에서 교집합을 찾아내려 했는데, 서로의 교지합 원소 개수에 따라 답이 달라질 수 있기 때문에, 공통으로 집합으로 만든 후 시행했다.   

```js
function solution(str1, str2) {
    var answer = 0;
    str1 = str1.toLowerCase();
    str2 = str2.toLowerCase();
    const str1_list = make_list(str1);
    const str2_list = make_list(str2);

    // 두 배열 다 공집합일 경우
    if(str1_list.length === 0 && str2_list.length === 0) return 1 * 65536;


    if(str1_list.length === 0 || str2_list.length === 0) return 0;
    // 교집합 합집합

    const str_set = new Set([...str1_list, ...str2_list]);
    let union = 0;
    let intersect = 0;

    str_set.forEach(str =>{
        let str1_inter = str1_list.filter(a => a === str).length;
        let str2_inter = str2_list.filter(a => a === str).length;

        union += Math.max(str1_inter, str2_inter);
        intersect += Math.min(str1_inter, str2_inter);

    })
    answer = parseInt(65536 * (intersect/union));

    return answer;
}

function make_list(str){
    let str_list = [];
    let temp = '';
        for (let i = 0; i < str.length-1; i++){
            temp = str.substr(i, 2);
            if(!temp.match(/[^a-z]/)){
                str_list.push(temp);
            }
        }
    return str_list;
    }
```
