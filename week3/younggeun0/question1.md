# [프로그래머스 > 코딩테스트 연습 > 연습문제 > 정수 제곱근 판별](https://school.programmers.co.kr/learn/courses/30/lessons/12934)

* 입력 - 임의의 양의 정수 n
* 출력
  * n이 양의 정수 x의 제곱이라면 x+1의 제곱을 리턴
  * 양의정수 x의 제곱이 아니라면 -1을 리턴

### 내 풀이
* 변수 i를 1부터 n까지 선형 탐색하며 n을 i로 나눴을 때 나머지가 0인 경우의 i값을 누적합, 누적한 약수값을 반환

```js
function solution(n) {
    const x = Math.sqrt(n);

    if (x % 1 !== 0)
        // 양의정수 x의 제곱이 아니라면 -1을 리턴
        return -1;
    else
        //  n이 양의 정수 x의 제곱이라면 x+1의 제곱을 리턴
        return Math.pow(x + 1, 2);
}
```
