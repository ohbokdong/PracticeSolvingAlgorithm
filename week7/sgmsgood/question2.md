## **[프로그래머스 > 코딩테스트 연습 > 연습문제 > 택배 상자](https://school.programmers.co.kr/learn/courses/30/lessons/131704)**

- 입력
    - order - 택배 기사님이 원하는 상자 순서를 담은 배열
- 출력
    - 영재가 실을 수 있는 상자의 개수

### **내 풀이

```kotlin
import java.util.*

class Solution {
    fun solution(order: IntArray): Int {
        val container = ArrayDeque<Int>()
        val stack = Stack<Int>()
        for (ord in order) container.add(ord)

        var num = 1
        var cnt = 0
        while (num <= order.size + 1 && container.isNotEmpty()) {
            if (num == container.first) {
                container.removeFirst()
                cnt++
                num++
            } else if (stack.isNotEmpty() && stack.peek() == container.first) {
                container.removeFirst()
                cnt++
                stack.pop()
            } else
                stack.push(num++)
        }
        return cnt
    }
}
```