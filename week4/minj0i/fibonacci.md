
### [프로그래머스 > 연습문제 > 피보나치 수](https://school.programmers.co.kr/learn/courses/30/lessons/12945)

- 입력
    - 2이상 100,000이하 n 임의의 수
- 출력
    - n번째 피보나치 수를 1234567로 나눈 나머지를 리턴하는 함수

```js
// time out
function solution(n) {
    var answer = 0;
    
    function fibonacci(n) {
      if (n <= 1) {
        return n;
      } else {
        return fibonacci(n - 1) + fibonacci(n - 2);
      }
    }
    
    answer = fibonacci(n) % 1234567
    
    return answer;
}
```

```js
// all fail - why?
function solution(n) {
    var answer = 0;
    
    function fibonacci(n) {

      let fibList = [];
      let [a, b] = [0, 1];

      while (a < n) {
        fibList.push(a);
        [a, b] = [b, a + b];
      }

      return fibList;
    }
    
    let finalFibList = fibonacci(n+1)
    answer = finalFibList[n] % 1234567
    
    return answer;
}
```

```js
// half success, half fail
function solution(n) {
    var answer = 0;
    
    function listFibonacci(n) {
      for (var fibonacci = [0, 1], i = 1; i < n; i++) 
        fibonacci.push(fibonacci[i] + fibonacci[i - 1])

      return fibonacci
    }
    
    let finalFibList = listFibonacci(n+1)
    answer = finalFibList[n] % 1234567
    
    return answer;
}
```

```js
function solution(n) {
    var answer = 0;
    
    function listFibonacci(n) {
      for (var fibonacci = [0, 1], i = 1; i < n; i++) 
        fibonacci.push(fibonacci[i]%1234567 + fibonacci[i - 1]%1234567)

      return fibonacci
    }
    
    let finalFibList = listFibonacci(n+1)
    answer = finalFibList[n] % 1234567
    
    return answer;
}
```