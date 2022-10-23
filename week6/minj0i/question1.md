### [프로그래머스 > 코딩테스트 연습 > 탐욕법 > 체육복](https://school.programmers.co.kr/learn/courses/30/lessons/42862)

- 입력
  - n : 전체 학생의 수
  - lost : 체육복을 도난당한 학생들의 번호가 담긴 배열 
  - reserve : 여벌의 체육복을 가져온 학생들의 번호가 담긴 배열
- 출력
  - 체육수업을 들을 수 있는 학생의 최댓값

### 이전 내 풀이

```js
function solution(n, lost, reserve) {
    // 여벌 체육복을 가져온 학생이 체육복을 도난당했을 수 있습니다를 제외하기
    var realLost = lost.filter(a => !reserve.includes(a));
    var realReserve = reserve.filter(a => !lost.includes(a));
    
    return n - realLost.filter(a => {
      //Math.abs 절대값을 사용함
        var b = realReserve.find(r => Math.abs(r-a) <= 1);
        if(!b) return true;
        realReserve = realReserve.filter(r => r !== b);
    }).length;
}
```

- 정렬이 되어있다는 보장이 없을 수 있다는 힌트 덕분에 바로 고쳐서 풀이
```js
function solution(n, lost, reserve) {
    var realLost = lost.sort((a, b) => a - b).filter(a => !reserve.includes(a));
    var realReserve = reserve.sort((a, b) => a - b).filter(a => !lost.includes(a));
    
    return n - realLost.filter(a => {
        var b = realReserve.find(r => Math.abs(r-a) <= 1);
        if(!b) return true;
        realReserve = realReserve.filter(r => r !== b);
    }).length;
}
```
