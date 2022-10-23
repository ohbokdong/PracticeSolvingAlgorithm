# Lv1. [프로그래머스 > 코딩테스트 연습 > 탐욕법(greedy) > 체육복](https://school.programmers.co.kr/learn/courses/30/lessons/42862)

* 나의 풀이
    * 풀이 순서
        * 1. convertArrayToMap()으로 "key" = reserve[i] , "value" = 2 로 셋팅된 맵을 만든다.
        * 2. 총 학생 수 에서 lost 된 학생 수를 뺀다.
        * 3. lost 된 학생 수는, reserve에도 중복될 수 있으므로 2번에서 제외된 학생의 수를 다시 추가해준다.
        * 4. reserver 학생이 체육복을 빌려주면, value의 값을 1로 바꿔주고, 빌린 학생은 activeCount에 숫자가 추가된다.

```kotlin
class Solution {
    fun solution(n: Int, lost: IntArray, reserve: IntArray): Int {
        var lostMutableList = lost.toMutableList()
        // 1.
        var reserveMutableMap = convertArrayToMap(reserve)
        // 2.
        var activeCount = n - lost.size
        
        // 3.
        lostMutableList.sorted().forEach{ v ->
            if(reserveMutableMap.keys.any{it == v}) {
                activeCount++                
                reserveMutableMap[v] = 1
                lostMutableList.remove(v)
            }   
        }
    
        
        // 4.
        lostMutableList.sorted().forEach {
            if(reserveMutableMap[it - 1] == 2){
                activeCount++  
                reserveMutableMap[it - 1] = 1
            } else if(reserveMutableMap[it + 1] == 2) {
                activeCount++
                reserveMutableMap[it + 1] = 1
            }
        }
       
        return activeCount
    }
    
    fun convertArrayToMap(reserve: IntArray): MutableMap<Int, Int> {
        val reserveMap = mutableMapOf<Int, Int>()
        reserve.sorted().forEach{
            reserveMap.put(it, 2)   
        }
        return reserveMap
    }
}
```
* 다른 사람의 풀이
```kotlin
class Solution {
        fun solution(n: Int, lost: IntArray, reserve: IntArray): Int {
            var answer = n
            
            // reserve했는데 lost 한 학생을 리스트에서 제거한 lost 리스트 생성 (중복처리)
            var lostSet = lost.toSet() - reserve.toSet()

            // reserve했는데 lost 한 학생을 리스트에서 제거한 reserve 리스트 생성 (중복처리) -> 수정이 되어야 하므로 MutableSet으로 캐스팅
            var reserveSet = (reserve.toSet() - lost.toSet()) as MutableSet

            for (i in lostSet) {
                when {
                    i + 1 in reserveSet -> reserveSet.remove(i + 1)
                    i - 1 in reserveSet -> reserveSet.remove(i - 1)
                    else -> answer--
                }
            }
            return answer
        }
}
```
