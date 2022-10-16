### [프로그래머스 > 코딩테스트 연습 > 옹알이](https://school.programmers.co.kr/learn/courses/30/lessons/120956)

- 입력
  - 머쓱이의 발음조합으로 표현 가능할지 모르는 발음 배열(babbling)
    - 1 <= babbling <= 10
    - 1 <= babbling[i]의 길이 <= 30
    - 문자열은 소문자로만 구성
- 출력
  - 머쓱이가 발음 가능한 옹알이 단어의 개수

### 내 풀이

- replace는 첫번째만 바꿔주는 걸 사용
- 테스트케이스 1을 자꾸 통과 못함

```js
function solution(babbling) {
    const able = ["aya", "ye", "woo", "ma"]
    for(let i=0; i<babbling.length; i++) {
        for(let j=0; j<able.length; j++) {
            let ableword = able[j]
            babbling[i] = babbling[i].replace(able[j], "")
        }
    }
    const found = babbling.filter(e => e === "");
    
    return found.length;
}
```

- babbling에서 ""가 들어오는 케이스를 넣어줌
- 근데도 실패함(이유가 뭘까요..?)
- 정규식으로 하면 좋을 것 같은데 중복처리를 어케할지 모르겠음

```js
function solution(babbling) {
    const able = ["aya", "ye", "woo", "ma"]
    let count = 0;    
    for(let i=0; i<babbling.length; i++) {
        if(babbling[i] !== "") {
            for(let j=0; j<able.length; j++) {
                let ableword = able[j]
                babbling[i] = babbling[i].replace(able[j], "")
            }
            if(babbling[i] === "") count++
        }
    }
    return count;
}
```
