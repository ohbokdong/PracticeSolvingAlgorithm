* 나의 풀이
```kotlin
class Solution {
    fun solution(n: Int): Int {
        var answer: Int = 0
        
        var ternary = changeToReverseTernary(n)
        
        var list = ternary.split("").filter{it != ""}.map{it.toInt()}
            
        list.forEachIndexed{ i, e ->
            var value = getValue(((list.size-1) - i), 1)
            
            print("${value * e} / ")
            
            answer += value * e
        }
        
        return answer
    }
    
    fun changeToReverseTernary(n: Int): String {
        var start = n
        var ternary = ""
        
        do {
            ternary += (start % 3).toString()
            start /= 3
        } while(start >= 1)
        
        return ternary
    }
    
    fun getValue(n: Int, result: Int): Int {
        if(n == 0) {
            return result
        } 
        
        return getValue(n - 1, result * 3)
    }
}
```
* 다른 사람의 풀이
```kotlin
class Solution {
    fun solution(n: Int): Int {
        return n.toString(3).reversed().toInt(3)
    }
}
```
