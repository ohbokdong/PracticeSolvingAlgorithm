## **[프로그래머스 > 코딩테스트 연습 > 월간 코드 챌린지 시즌2 > 음양 더하기](https://school.programmers.co.kr/learn/courses/30/lessons/76501)**

- 입력
    - absolutes - 정수값을 담은 배열
    - signs - 정수값의 부호를  boolean 값으로 담은 배열
- 출력
    - 부호가 적용된 정수들의 합

### **내 풀이**

1. map을 돌려서 계산

```js
function solution(absolutes, signs) {
    var answer = 0;
    
    absolutes.map((v, i) => {
        if(signs[i]) {
            answer += v
        } else {
            answer -= v   
        }
    })
    return answer;
}
```