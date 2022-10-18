### [프로그래머스 > 코딩테스트 연습 > 탐욕법 > 체육복](https://school.programmers.co.kr/learn/courses/30/lessons/42862)

- 입력
  - n : 전체 학생의 수
  - lost : 체육복을 도난당한 학생들의 번호가 담긴 배열 
  - reserve : 여벌의 체육복을 가져온 학생들의 번호가 담긴 배열
- 출력
  - 체육수업을 들을 수 있는 학생의 최댓값

### 이전 내 풀이

* 이전에 풀렸으나 안풀리는 테스트 케이스가 존재해서 확인해보니 정렬되지 않은 lost, reserve값이 입력되는 케이스가 추가된듯함 => 정렬 후 기존 로직 수행하도록 수정
* 뭔가 풀이가 장황함...

1. 입력값 정렬(lost, reserve)
2. 여분 체육복을 갖고 있으나 잃어버린 경우 제외 (lost, reserve 중복 제거)
3. 체육복 나눠줌(reserve 순회하며 lost 항목 제거)
4. 전체 학생수에서 체육복 없는 학생 수 뺀 값을 반환


```js
function solution(n, lost, reserve) {
    var answer = 0;

    // 정렬되지 않은 테스트케이스용, 미리 정렬하고 시작
    lost.sort();
    reserve.sort();
    
    // 1. 여분 가져온 학생들도 도난 당했을 수 있음
    //    reserve에서 lost와 곂치는 번호는 제거
    var enableReserve = [];
    var bLost = false;
    var i,j, nNum;
    for (i=0; i<reserve.length; i++) {
        nNum = reserve[i];
        for (j=0; j<lost.length; j++) {
            if (nNum == lost[j]) {          // reserve인데 도난당한 경우
                bLost = true;
                lost.splice(j, 1);
                break;
            }
        }
        if (bLost) {
            bLost = false;
            continue;
        }
        
        enableReserve.push(nNum);
    }
    
    // 3. 체육복 빌려줄 수 있는 인원 수 추가
    for (i=0; i<enableReserve.length; i++) {
        nNum = enableReserve[i];
        var nBeside1 = nNum - 1;
        var nBeside2 = nNum + 1;
        
        for (j=0; j<lost.length; j++) {
            if (lost[j] == nBeside1 || lost[j] == nBeside2) {
                lost.splice(j, 1);
                break;
            }
        }
    }
    
    // 체육수업을 들을 수 있는 학생의 최댓값 반환
    return n - lost.length;
}
```

### 개선한 내 풀이

1. 입력값 정렬(lost, reserve)
2. 여분 체육복을 갖고 있으나 잃어버린 경우 제외 (lost, reserve 중복 제거)
3. 체육복 나눠줌(reserve 순회하며 lost 항목 제거)
4. 전체 학생수에서 체육복 없는 학생 수 뺀 값을 반환

```js
function solution(n, lost, reserve) {
    // 입력값 정렬
    lost.sort();
    reserve.sort();
    
    // 여분 체육복을 갖고 있으나 잃어버린 경우 제외
    const distinctLost = lost.filter(l => !reserve.includes(l));
    const distinctReserve = reserve.filter(r => !lost.includes(r));

    // 여분 갖고 있는 학생이 잃어버린 학생들에게 나눠줌
    distinctReserve.forEach(r => {
        for (let i=0; i<distinctLost.length; i++) {
            if (canBorrow(distinctLost[i], r)) {
                distinctLost.splice(i, 1);
                break;
            }
        }
    });

    return n - distinctLost.length;


    function canBorrow(lost, reserve) {
        return lost === reserve-1 || lost === reserve+1;
    }
}
```

### 남의 풀이

1. 전체 학생 수에 대한 배열 생성, 학생번호별 체육복 수를 1로 초기화
2. lost 배열을 순회하며 학생번호별 체육복 수를 --1
3. reserve 배열을 순회하며 학생번호별 체육복 수를 ++1
4. 체육복 수가 2인 학생의 앞 뒤에 체육복이 없는 경우 체육복을 줌
5. 체육복의 수가 1이상인 경우만 카운트해서 반환

```js
function solution(n, lost, reserve) {
    const students = [];
    for(let i = 0; i < n; i++){
        students[i] = 1;
    }

    lost.forEach(number => students[number-1] -= 1);
    reserve.forEach(number => students[number-1] += 1);

    for(let i = 0; i < n; i++){
        if(students[i] === 2) {
            if (students[i-1] === 0){
                students[i-1]++;
                students[i]--;
            } else if(students[i+1] === 0){
                students[i+1]++;
                students[i]--;
            }
        }
    }

    return students.reduce((acc, cnt) => cnt > 0 ? ++acc : acc, 0);
}
```