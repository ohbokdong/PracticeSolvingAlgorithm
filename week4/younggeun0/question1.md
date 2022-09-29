### [프로그래머스 > 코딩테스트 연습 > 완전탐색 > 모의고사](https://school.programmers.co.kr/learn/courses/30/lessons/42840)

-   입력
  -   answers - 문제의 정답들
-   출력
  -   가장 많은 문제를 맞춘 수포자가 담긴 배열

### 내 풀이(이전 풀이)

1. 학생들의 패턴을 미리 배열에 담아둔 뒤 인덱스를 이용해서 문제를 순회하며 카운트
2. 가장 많이 맞춘 학생의 답 수(max)를 구하고 학생들이 맞춘값을 다시 순회하며 답 배열에 담아 반환

```js
function solution(answers) {
    var answer = [];

    // 학생들 패턴
    var student = [
        [1, 2, 3, 4, 5],
        [2, 1, 2, 3, 2, 4, 2, 5],
        [3, 3, 1, 1, 2, 2, 4, 4, 5, 5],
    ];

    var studentCnt = [0, 0, 0]; // 학생별 맞춘 문제 수

    for (var i in answers) {
        // for-in 으로 인덱스 사용
        if (student[0][i % 5] == answers[i]) {
            studentCnt[0]++;
        }
        if (student[1][i % 8] == answers[i]) {
            studentCnt[1]++;
        }
        if (student[2][i % 10] == answers[i]) {
            studentCnt[2]++;
        }
    }

    var max = Math.max(...studentCnt);

    for (var i in studentCnt) {
        if (studentCnt[i] == max) {
            answer.push(Number(i) + 1);
        }
    }

    return answer;
}
```

### 다시 푼 내 풀이

-   ES6로 리팩터링한 답

```js
function solution(answers) {
    const answer = [];
    const students = [
        [1, 2, 3, 4, 5],
        [2, 1, 2, 3, 2, 4, 2, 5],
        [3, 3, 1, 1, 2, 2, 4, 4, 5, 5],
    ];
    const cnts = Array(3).fill(0);

    answers.forEach((answer, idx) => {
        students[0][idx % students[0].length] === answer && cnts[0]++;
        students[1][idx % students[1].length] === answer && cnts[1]++;
        students[2][idx % students[2].length] === answer && cnts[2]++;
    });

    const max = Math.max(...cnts);

    cnts.forEach((cnt, idx) => {
        if (cnt === max) answer.push(idx + 1);
    });

    return answer;
}
```
