# [프로그래머스 > 코딩테스트 연습 > 연습문제 > 최댓값과 최솟값](https://school.programmers.co.kr/learn/courses/30/lessons/12939)

```js
function solution(s) {
    var answer = '';
    const arr = s.split(" ")
    // using Number.MAX_SAFE_INTEGER / Number.MIN_SAFE_INGEGER for initialize
    let min = Number.MAX_SAFE_INTEGER
    let max = Number.MIN_SAFE_INTEGER

    arr.map((v) => {
        if(parseInt(v) > max) max = v
        if(parseInt(v) < min) min = v
    })
    answer = `${min} ${max}`
    return answer;
}
```