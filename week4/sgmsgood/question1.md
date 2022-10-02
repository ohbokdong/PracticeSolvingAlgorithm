* 나의 풀이
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
* 다른 사람의 풀이
```kotlin
class Solution {
    fun solution(answers: IntArray): IntArray {
        var supo1 = intArrayOf(1,2,3,4,5)
        var supo2 = intArrayOf(2,1,2,3,2,4,2,5)
        var supo3 = intArrayOf(3,3,1,1,2,2,4,4,5,5)
        var x = 0; var y = 0; var z = 0

        var map = mutableMapOf<Int,Int>(Pair(1,0),Pair(2,0),Pair(3,0))
        for(i in answers) {
            if(i == supo1[x]) map.put(1,map[1]!! + 1)
            if(i == supo2[y]) map.put(2,map[2]!! + 1)
            if(i == supo3[z]) map.put(3,map[3]!! + 1)
            x = if(x < 4) x + 1 else 0
            y = if(y < 7) y + 1 else 0
            z = if(z < 9) z + 1 else 0
        }

        var max = map.maxBy({it.value})?.value
        for(i in 1..map.size) if(map[i] != max) map.remove(i)
        var answer = map.toList().sortedWith(compareBy({it.second})).toMap().keys.toIntArray()

        return answer
    }
}
```
