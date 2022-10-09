### [프로그래머스 > 코딩테스트 연습 > 옹알이](https://school.programmers.co.kr/learn/courses/30/lessons/120956)

- 입력
  - 머쓱이의 발음조합으로 표현 가능할지 모르는 발음 배열(babbling)
    - 1 <= babbling <= 10
    - 1 <= babbling[i]의 길이 <= 30
    - 문자열은 소문자로만 구성
- 출력
  - 머쓱이가 발음 가능한 옹알이 단어의 개수

### 내 풀이

1. 머쓱이가 발음 가능한 조합 배열 생성(coos)
2. reduce로 입력된 babbling 단어들을 순회하며 발음가능 여부 확인 후 누적합을 구함
3. 예외 조건 - 머쓱이는 연속된 같은 발음을 못 함
4. coos 순회하며 발음 가능한 문자열들로 bWord에서 계속 제거
5. coos 순회가 끝날 때 bWord의 길이가 0인 경우가 발음 가능한 경우, 이 때만 +1 누적합

```js
function solution(babbling) {
    // 조카가 발음할 수 있는 네가지 조합
    const coos = ["aya", "ye", "woo", "ma"];
    
    return babbling.reduce((cnt, bWord) => {

        for (let i=0; i<coos.length; i++) {
            const coo = coos[i];

            // 같은 발음이 연속된 경우
            if (bWord.indexOf(coo + coo) != -1) {
                break;
            }

            // bWord에서 발음 가능한 단어를 제거
            while(bWord.indexOf(coo) !== -1) {
                 bWord = bWord.slice(0, bWord.indexOf(coo)) +
                         bWord.slice(bWord.indexOf(coo) + coo.length);
            }
        }
        
        if (bWord.length === 0) {
            return cnt + 1;
        } else {
            return cnt;
        }
    }, 0);
}
```

### 남의 풀이

1. [Array.prototype.some](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/some) 메서들르 사용하여 연속된 단어인지 판별, 연속된 경우 다음 단어로 continue
2. [String.prototype.replaceAll](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/replaceAll) 메서드로 옹알이 단어들을 모두 빈 문자열로 치환
3. 문자열의 길이가 0과 같은 경우만 카운트하여 발음 가능한 단어 수 누적합을 구함

```js
function solution(babbling) {
    let df = [ "aya", "ye", "woo", "ma"];
    let res = 0;
    for(let w of babbling) {
        if(df.some(f => w.includes(f+f))) continue;

        let rest = 
           df.reduce((a, f) => a.replaceAll(f, ""), w);

        if (rest.length > 0) continue;

        res++;
    }

    return res;
}
```
