* 나의 풀이
    * 주어진 10진수(N)을 changeToReverseTernary() 메소드로 앞뒤 반전된 3진법 값을 구한다.
    * 앞 뒤가 반전된 3진법 String을 Split하여 리스트로 받은 뒤, map 함수로 int 리스트를 만든다.
    * 리스트의 요소를 하나씩 돌아가며, getValue로 각 인덱스에 맞는 값을 찾는다.
    * 값이 구해질 때마다 더해서 10진법 결과 값을 도출한다.
    
```kotlin
class Solution {
    fun solution(n: Int): Int {
        var answer: Int = 0
        
        var ternary = changeToReverseTernary(n)
        
        var list = ternary.split("").filter{it != ""}.map{it.toInt()}
            
        list.forEachIndexed{ i, e ->
            var value = getValue(((list.size-1) - i), 1)    
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
