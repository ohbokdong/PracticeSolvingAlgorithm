# [프로그래머스 > 코딩테스트 연습 > 연습문제 > 약수의 합](https://school.programmers.co.kr/learn/courses/30/lessons/12928)

```js
function solution(n) {
    var answer = 0;
    let i = 1;
    // using while loop
    while (i <= n) {
        // finding submultiple
        if(n%i === 0) answer += i;
        i++;
    }
    return answer;
}
```