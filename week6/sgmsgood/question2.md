# Lv2. [프로그래머스 > 코딩테스트 연습 > 월간 코드 챌린지 시즌1 > 이진 변환 반복하기](https://school.programmers.co.kr/learn/courses/30/lessons/70129)

* 나의 풀이
    * 1. String을 ""로 split하여 리스트로 변환
    * 2. filter로 "0"의 개수를 구하고 루프가 돌 때마다 zeroCount에 add
    * 3. 다시 filter로 "1"의 개수를 찾고, 2진법으로 변환하여 editS에 대입
    * 4. editS가 "1"이 될 때까지 반복
    * 5. 각 항목을 배열에 넣음
    
```kotlin
class Solution {
    fun solution(s: String): IntArray {
        var answer: IntArray = intArrayOf(0, 0)
        var zeroCount = 0
        var loopCount = 0
        
        var editS = s
        
        while(editS != "1") {
            var splitString = editS.split("")
            zeroCount += splitString.filter{it == "0"}.size
            editS = splitString.filter{it == "1"}.size.toString(2)
            loopCount++
        }
        
        answer[0] = loopCount
        answer[1] = zeroCount
    
        return answer
    }
}
```
* 다른 사람의 풀이
```kotlin
class Solution {
    fun solution(s: String): IntArray {
        var copiedS = s
        var removedZero = 0
        var count = 0

        while (copiedS != "1") {
            removedZero += copiedS.replace("1", "").count()
            copiedS = Integer.toBinaryString(copiedS.replace("0", "").count())
            count++
        }
        return intArrayOf(count, removedZero)
    }
}
```
