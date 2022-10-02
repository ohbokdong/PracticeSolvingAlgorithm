```kotlin
class Solution {
    fun solution(answers: IntArray): IntArray {
        val patternMap: Map<Int, IntArray> = mapOf(1 to intArrayOf(1, 2, 3, 4, 5), 2 to intArrayOf(2, 1, 2, 3, 2, 4, 2, 5), 3 to intArrayOf(3, 3, 1, 1, 2, 2, 4, 4, 5, 5))
        val answerMap: MutableMap<Int, Int> = mutableMapOf(1 to 0, 2 to 0, 3 to 0)
        
        var questionIndex = 0
        var maxCount = 0
        
        patternMap.forEach {
            var answerCount = getCompareAnswerCount(answers, it.value)
            questionIndex++
            answerMap.put(questionIndex, answerCount)
        }
        
        answerMap.forEach{
            if(maxCount < it.value) {
                maxCount = it.value
            }
        }
        
        return answerMap.filter{it.value == maxCount}.keys.toIntArray()
    }
    
    fun getCompareAnswerCount(answers: IntArray, patternList: IntArray): Int {
        var count = 0
        
        answers.forEachIndexed { i, e ->
            var index = 0
            if(i == 0) {
                index = 0
            } else {
                index = i % patternList.size
            }
            
            if(e == patternList.get(index)) {
                count++
            }
        }
        
        return count
    }
}
```
