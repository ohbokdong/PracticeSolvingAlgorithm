*  내가 푼 코드
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