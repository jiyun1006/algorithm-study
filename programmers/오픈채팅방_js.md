### kakao 오픈채팅방(js풀이)   

- 기본적으로 주어진 배열을 조건에 맞게 조작하는 문제이다.   

- 주어진 배열에서 한 번 순회해서 닉네임이 변경되면, 모두 다 변경한 채로 저장한다.   

- 생각보다 js로 푸는 것이 어렵지 않았다.(문제도 쉬웠고, 다른 언어와 푸는 법이 다르지 않다.)   

```js
let solution = (record) => {
    let answer = [];

    let newArr = record.map(x=>x.split(" "));
    
   
    let nickNameSet = {};
    for(let i=0; i<newArr.length; i++){
        if(newArr[i].length === 3){
            nickNameSet[newArr[i][1]] = newArr[i][2];
        }
    }
    
    
    for(let i=0; i<newArr.length; i++){
        if(newArr[i][0] === "Enter"){
            answer.push(nickNameSet[newArr[i][1]] + "님이 들어왔습니다.")
        } else if(newArr[i][0] === "Leave"){
            answer.push(nickNameSet[newArr[i][1]] + "님이 나갔습니다.")
        }
        
    }
    
    return answer;
}
```
