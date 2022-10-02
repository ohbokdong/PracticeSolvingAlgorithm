
# [프로그래머스 > 코딩테스트 연습 > 무슨 문제](https://school.programmers.co.kr/learn/challenges?levels=1%2C2)

* 입력 - 
* 출력 - 

### 내 풀이

* 내 풀이 내용

```kotlin
class Solution {
    fun solution(n: Int): Int {
        var answer = 0
        var answerList: MutableList<Int> = mutableListOf()
  
        answerList.add(0)
        answerList.add(1)
        
        for(i in 2..n) {
           var element = (answerList.get(i-1) % 1234567) + (answerList.get(i-2) % 1234567)
           answerList.add(element)
        }
        
        return answerList.last() % 1234567
    }
}
```

* 재귀를 사용해서 풀어야겠다는 직감적인 직감은 들었지만 재귀를 만들어 낼 코드를 짜지 못함..
* 앞의 수와 뒤의 수가 합쳐진 값을 리스트에 순차적으로 추가해서 정답을 내뱉는 코드를 짬........... 

### 남의 풀이

* 남의 풀이 내용

```kotlin
class Solution {
    fun solution(n: Int): Int = if(n == 1 || n == 2) 1 else fib(n, 1, 1)  
    tailrec fun fib(n: Int, a: Int, b: Int): Int = if(n == 1) a else fib(n - 1, b % 1234567, (a + b) % 1234567)
}
```
