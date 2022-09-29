### [프로그래머스 > 연습문제 > 피보나치 수](https://school.programmers.co.kr/learn/courses/30/lessons/12945)

- 입력
    - 2이상 100,000이하 n 임의의 수
- 출력
    - n번째 피보나치 수를 1234567로 나눈 나머지를 리턴하는 함수

### 내 풀이(이전 풀이)

1. n까지 반복하며 피보나치 수를 구하고 answer배열에 담음
2. answer배열에서 n번째 인덱스를 갖는 값 반환

```js
function solution(n) {
    var answer = [0, 1];
    
    for(var i=2; i<n+1; i++) {
        answer.push((answer[i-2] + answer[i-1]) % 1234567);
    }
    
    return answer[n];
}
```

### 다시 푼 내 풀이

- 재귀로 다시 풀어보려고 했는데 13,14번 케이스에서 자꾸 에러 발생
    - [확인결과 재귀한도가 정해져 있어서 발생한 이슈같음](https://school.programmers.co.kr/questions/15243)
        
        ⇒ 반복문으로 구하는게 더 나을 수도 있다…

```js
function solution(n) {
    const answer = [0, 1]; // n은 2이상의 수
    
    // 피보나치 수를 구하는 재귀 함수로 n번째 피보나치 수를 구할 때까지 재귀호출
    const addFibonacciNum = (i) => {
        if (answer.length === n + 1) return;

        answer.push((answer[i-1] + answer[i-2]) % 1234567);
        addFibonacciNum(++i);
    };
    addFibonacciNum(2);
    
    return answer[n];
}
```