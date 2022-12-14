# [프로그래머스 > 코딩테스트 연습 > 연습문제 > 약수의 합](https://school.programmers.co.kr/learn/courses/30/lessons/12928)

* 입력 - 임의의 수 n
* 출력 - 임의의 수의 약수의 합

### 내 풀이
* 변수 i를 1부터 n까지 선형 탐색하며 n을 i로 나눴을 때 나머지가 0인 경우의 i값을 누적합, 누적한 약수값을 반환

```js
function solution(n) {
    var answer = 0;
    
    for (var i=1; i<=n; i++) {
        if (n % i === 0) {
            answer += i;
        }
    }
    
    return answer;
}
```

### 남의 풀이

* 재귀, 삼항연산자를 써서 푼게 특이했음
* base case를 만족시키기 위해서 n이 아닌 2n까지 반복을 해서 성능은...

```js
function solution(n, a = 0, b = 0) {
    return n <= a / 2 ? b : solution(n, a+1, b += n%a ? 0 : a);
}

// 현기증 나는 풀이
function solution(n, a = 0, b = 0) {
    if (n <= a / 2) { // base case
        return b;
    } else {
        if (n % a) { // a가 0인 경우 NaN
            b += 0;
        } else {
            b += a;
        }

        return solution(n, a + 1, b);
    }
}
```