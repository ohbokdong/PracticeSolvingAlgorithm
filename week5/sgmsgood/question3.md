
# [프로그래머스 > 코딩테스트 연습 > 무슨 문제](https://school.programmers.co.kr/learn/challenges?levels=1%2C2)

* 입력 - 
* 출력 - 

### 내 풀이

* 내 풀이 내용
    * 규칙을 찾고자 노력했지만 찾을 수 없어서 다른 사람의 풀이로 대체

```kotlin
-
```

### 남의 풀이

* 남의 풀이 내용
    * 총 정사각형의 개수 - (세로 개수 + 가로 개수) + 가로&세로의 최대 공약수
    * ![solution](https://github.com/ohbokdong/PracticeSolvingAlgorithm/blob/main/week5/sgmsgood/sol3.png)

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
