## **[프로그래머스 > 코딩테스트 연습 > 월간 코드 챌린지 시즌2 > 음양 더하기](https://school.programmers.co.kr/learn/courses/30/lessons/76501)**

- 입력
    - absolutes - 정수값을 담은 배열
    - signs - 정수값의 부호를  boolean 값으로 담은 배열
- 출력
    - 부호가 적용된 정수들의 합

### **내 풀이**

```kotlin
class Solution {
    fun solution(absolutes: IntArray, signs: BooleanArray): Int {
        var answer: Int = 0
        absolutes.forEachIndexed { i, e ->
            if(signs[i]) {
                answer += e
            } else {
                answer -= e
            }
        }
        return answer
    }
}
```