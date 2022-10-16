
# Lv2. [프로그래머스 > 코딩테스트 연습 > summer/winter Coding (2019) > 멀쩡한 사각형](https://school.programmers.co.kr/learn/courses/30/lessons/62048)

* 입력 - 
* 출력 - 

### 내 풀이

* 내 풀이 내용
    * 규칙을 찾아내고자 했지만 찾을수 없어서 다른 사람들의 풀이만 참조함 

```kotlin
-
```

### 남의 풀이

* 남의 풀이 내용


```kotlin
class Solution {
    fun gcd(a: Int, b: Int): Long {
        if (a==0) return b.toLong()
        return gcd(b%a,a)
    }

    fun solution(w: Int, h: Int): Long {
        var wl = w.toLong()
        var hl = h.toLong()
        return wl*hl-wl-hl+gcd(w,h)
    }
}
```
