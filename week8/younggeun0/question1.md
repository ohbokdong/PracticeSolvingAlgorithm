## [프로그래머스 > 코딩테스트 연습 > 삼총사](https://school.programmers.co.kr/learn/courses/30/lessons/131705)

* 입력 - 숫자 배열
* 출력 - 세 숫자를 더해서 합이 0이 되는 경우의 수

### 내 풀이(JS)

* 풀이 생각 안나서 검색해서 3중 for문 풀이 보는 순간 다르게 풀 생각을 접음...

```js
function solution(number) {
    let answer = 0;
    
    // number 배열 요소중에서 3개를 선택했을 때 0인 모든 경우의 수를 구해 반환하는 문제
    for(let i=0; i<number.length-2; i++) {
        for (let j=i+1; j<number.length-1; j++) {
            for (let k=j+1; k<number.length; k++) {
                answer += number[i] + number[j] + number[k] === 0 ? 1 : 0
            }
        }
    }
    
    return answer;
}
```

### 내 풀이(Python)

* 파이썬에 익숙해지고자 로직은 그대로 포팅

```Python
def solution(number):
    answer = 0
    length = len(number)
    for i in range(length-2):
        for j in range(i+1, length-1):
            for k in range(j+1, length):
                if number[i] + number[j] + number[k] == 0:
                    answer += 1
    
    return answer
```


### 다른 사람의 풀이(JS)

* 재귀 함수를 만들어서 재귀호출로 풂
  1. 빈 배열과 시작 인덱스 0을 입력받아 재귀적으로 배열에 3개의 요소가 포함되는 모든 경우의 수를 구함
  2. 배열에 3개의 요소가 포함된 경우 누적합을 구하고 값이 0인 경우만 카운트해서 값을 구함

```js
function solution(number) {
    let result = 0;

    const combination = (arr, start) => {
        if (arr.length === 3) {
            // 배열에 요소가 3개가 되면 합을 구해서 0인 경우 result++
            if (sumUp(arr) === 0)
                result++
            return;
        }

        for (let i = start; i < number.length; i++) {
            combination([...arr, number[i]], i + 1);
        }
    }
    combination([], 0);
    return result;


    function sumUp(array) {
        return array.reduce((acc, cur) => acc + cur, 0)
    }
}
```

### 다른 사람 풀이(Python)

* itertools 모듈의 combinations란 함수를 임포트해서 사용...(파이썬 사기네;;)
    1. 배열에서 3개를 조합한 튜플을 담는 리스트를 만듦
    2. sum함수를 이용해서 튜플의 합이 0인 경우만 0이란 합을 리스트에 담음
    3. 0이 담긴 배열의 길이를 반환

```python
from itertools import combinations

def solution(number):    
    """
        list(combinations(number, 3))의 결과 :
            (-2, 3, 0), (-2, 3, 2), (-2, 3, -5), (-2, 0, 2),
            (-2, 0, -5), (-2, 2, -5), (3, 0, 2), (3, 0, -5),
            (3, 2, -5), (0, 2, -5)
    """
    num_combinations = [sum(comb) for comb in list(combinations(number, 3)) if sum(comb) == 0]
    
    return len(num_combinations)
```
