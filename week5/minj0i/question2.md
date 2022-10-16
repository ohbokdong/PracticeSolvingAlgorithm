### [프로그래머스 > 코딩테스트 연습 > 월간 코드 챌린지 > 3진법 뒤집기](https://school.programmers.co.kr/learn/courses/30/lessons/68935)

- 입력
  - 자연수 n(1<= n <= 100,000,000)
- 출력
  - n을 3진법 상에서 앞뒤로 뒤집은 후, 다시 10진법으로 표현한 수

### 내 풀이

- 3진법 찾다가 답을 봐버려버림..
- toString(3)으로 3진법
- split("")으로 쪼개고
- reverse()로 바꾸고
- join('')로 문자열을 다시 합치고
- parseInt()로 3진법을 10진법으로 계산

```js
function solution(n) {
    return parseInt(n.toString(3).split("").reverse().join(''), 3)
}
```