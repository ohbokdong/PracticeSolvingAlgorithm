### [프로그래머스 > 코딩테스트 연습 > 완전탐색 > 모의고사](https://school.programmers.co.kr/learn/courses/30/lessons/42840)

- 입력
  - answers - 문제의 정답들
- 출력
  - 가장 많은 문제를 맞춘 수포자가 담긴 배열

### 내 풀이
```js
function solution(answers) {
    const supo1 = [1,2,3,4,5]
    const supo2 = [2,1,2,3,2,4,2,5]
    const supo3 = [3,3,1,1,2,2,4,4,5,5]
    let suposScore = [0, 0, 0]
    let answer = []
    
    for(let i = 0; i < answers.length; i++) {
        if(answers[i] === supo1[i%5]) suposScore[0]++
        if(answers[i] === supo2[i%8]) suposScore[1]++
        if(answers[i] === supo3[i%10]) suposScore[2]++
    }

    const max = Math.max(...suposScore);
    
    for(let j = 0; j < 3; j++) {
        if(suposScore[j] === max) {
            answer.push(j+1)
        }
    }
    
    return answer;
}
```