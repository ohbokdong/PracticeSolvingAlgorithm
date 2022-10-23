### [프로그래머스 > 코딩테스트 연습 > 월간 코드 챌린지1 > 이진 변환 반복하기](https://school.programmers.co.kr/learn/courses/30/lessons/70129)

- 문제에서 정의한 이진 변환
  - 입력된 문자열에서 "0"제거
  - "0"이 제거된 문자열의 길이를 다시 2진수로 변환
  - 2진수로 변환 시 값이 "1"이 될 때까지 위 과정을 반복
- 입력
  - 이진변환할 이진수 문자열
- 출력
  - 이진변환 횟수와 0이 제거된 수를 담은 배열

### 내 풀이

```js
function solution(s) {
    let round = 0
    let removeZero = 0
    
    while(s.length > 1) {
        const sLength = s.length
        s = s.split('').filter(v => v === '1').join('')
        const newLen = s.length
        removeZero+=sLength-newLen
        s=newLen.toString(2)
        round++
    }
    return[round,removeZero]
}
```