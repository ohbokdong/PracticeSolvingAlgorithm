# [프로그래머스 > 코딩테스트 연습 > 삼총사](https://school.programmers.co.kr/learn/courses/30/lessons/131705)

* 입력 - 숫자 배열
* 출력 - 세 숫자를 더해서 합이 0이 되는 경우의 수

### 내 풀이

* 간지 안나는 삼중for문
* 값을 하나 입력받고 나머지 배열 중 두 합이 그 값의 * -1 뭐 이런식으로 구해볼까 했으나 방법이 생각 안남

```js
function solution(number) {
    var answer = 0;

    for(let i = 0; i<number.length - 2; i++) {
        for(let j = i+1; j<number.length - 1; j++) {
            for(let k = j+1; k<number.length; k++) {
                if(number[i]+number[j]+number[k] === 0) {
                    answer++
                }
            }
        }
    }
    return answer;
}
```