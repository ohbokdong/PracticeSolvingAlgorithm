# [프로그래머스 > 코딩테스트 연습 > 연습문제 > 정수 제곱근 판별](https://school.programmers.co.kr/learn/courses/30/lessons/12934)

```js
function solution(n) {
    var answer = 0;
    
    const sqrtN = Math.sqrt(n);

    Number.isInteger(sqrtN) ? answer = Math.pow(sqrtN + 1, 2) : answer = -1
    
    return answer
}
```

* Math.sqrt
* Number.isInteger
* Math.pow