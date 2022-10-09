### [프로그래머스 > 코딩테스트 연습 > 월간 코드 챌린지 > 3진법 뒤집기](https://school.programmers.co.kr/learn/courses/30/lessons/68935)

- 입력
  - 자연수 n(1<= n <= 100,000,000)
- 출력
  - n을 3진법 상에서 앞뒤로 뒤집은 후, 다시 10진법으로 표현한 수

### 내 풀이(이전 풀이)

1. 10진법 수 n을 3으로 나눈 나머지들을 문자열로 누적(뒤집어진 3진법 수의 문자열)
2. 뒤집힌 3진법 수를 10진법으로 재변환

```js
function solution(n) {
    // 1. 10진법 수 n을 뒤집힌 3진법 문자열(reveresedTernaryStr)로 변환
    let reversedTernaryStr = "";
    while (n > 0) {
        const r = n % 3;
        reversedTernaryStr = reversedTernaryStr + r; // 붙이는 방향으로 3진법 수의 순서 반전
        n = parseInt(n / 3);
    }
    
    // 2. 10진법 수로 재변환
    return [...reversedTernaryStr].reduce((acc, num, idx) => {
        return acc + parseInt(num) * Math.pow(3, reversedTernaryStr.length - (idx + 1));
    }, 0);
}
```

### 남의 풀이

- JS에선 `10진수.toString(변환할 진수)`로 쉽게 진법 변환이 가능

1. n을 `toString`을 이용해서 3진법 수 문자열로 변환
2. `...` 스프레드 연산자로 각 자리 문자를 갖는 배열로 바꾼 뒤 `reverse` 메서드로 순서를 뒤집음
3. `join` 메서드로 배열을 다시 하나의 문자열로 합침
4. `parseInt` 메서드로 기존 3진법의 수를 10진법의 수로 변환

```js
const solution = (n) => {
    return parseInt([...n.toString(3)].reverse().join(""), 3);
}

const solution = (n) => {
    // when n is 45
    const ternaryStr = n.toString(3); // "1200"

    const charArr = [...ternaryStr]; // ['1','2','0','0']

    const reversedTernaryStr = charArr.reverse().join(""); // "0021"

    const decimal = parseInt(reversedTernaryStr, 3); // 7

    return decimal;
}
solution(45)
```
