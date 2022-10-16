# Lv1. [코딩테스트 연습 > 코딩테스트 입문 > 옹알이](https://school.programmers.co.kr/learn/courses/30/lessons/120956)

* 나의 풀이
    * 풀이 순서
        * 1. nonDoubleWordList: 1) 같은 단어가 연속적으로 반복되지 않고, 2) 발음 가능한 단어가 하나라도 들어있는 리스트를 새로 얻는다.
        * 2. 위에서 얻은 list에서 발음할 수 있는 단어를 "" 로 replace 한다.
        * 3. 이렇게 수정한 결과값이 empty인 단어만 찾아서 answer++한다.

    * 다른 사람의 수식 참조
        * String.repeat(숫자) -> 숫자만큼 같은 string이 반복됨
        * iterable.count{}: 주어진 predicate를 만족하는 원소의 개수를 반환해줌 (참조: https://tourspace.tistory.com/111)
        * run{} (범위 지정 연산자): 공부 필요해... 
```kotlin
class Solution {
    fun solution(babbling: Array<String>): Int {
        var answer: Int = 0
        val ableList = arrayOf("aya", "ye", "woo", "ma")
        
        var nonDoubleWordList = getComparableWordList(babbling, ableList)
        
        nonDoubleWordList.forEach {v ->
            var removed = v
            ableList.forEach {       
                removed = removed.replace(it, "")
            }
            
            if(removed.length == 0) {
                answer++
            }
        }
        
        
        return answer
    }
    
    fun getComparableWordList(babbling: Array<String>, ableList: Array<String>): List<String> {
         return babbling.filter{ v ->
            var isExist = false
            isExist = ableList.any{ e ->
               v.contains(e) && !isContinueSameWord(v)
            }
            isExist
        }.toList()
    }
    
    fun isContinueSameWord(babblingWord: String): Boolean {
        val doubleList = arrayOf("ayaaya", "yeye", "woowoo", "mama")
        var isDouble = false
        
        return doubleList.any{ babblingWord.contains(it) }
    }
}
```
* 다른 사람의 풀이
```kotlin
class Solution {
    fun solution(babbling: Array<String>): Int {
        val pronounces = listOf("aya", "ye", "woo", "ma")
        return babbling.count {
            var word = it
            run {
                pronounces.forEach { pronounce ->
                    if (it.contains(pronounce.repeat(2))) return@run false
                    word = word.replace(pronounce, "")
                }
                word.isEmpty()
            }
        }
    }
}
```
