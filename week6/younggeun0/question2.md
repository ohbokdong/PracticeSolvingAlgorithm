### [프로그래머스 > 코딩테스트 연습 > 월간 코드 챌린지1 > 이진 변환 반복하기](https://school.programmers.co.kr/learn/courses/30/lessons/70129)

- 문제에서 정의한 이진 변환
  - 입력된 문자열에서 "0"제거
  - "0"이 제거된 문자열의 길이를 다시 2진수로 변환
  - 2진수로 변환 시 값이 "1"이 될 때까지 위 과정을 반복
- 입력
  - 이진변환할 이진수 문자열
- 출력
  - 이진변환 횟수와 0이 제거된 수를 담은 배열

### 내 풀이

1. 이진변환을 수행하는 재귀함수 생성(transform)
2. 기저 조건(base case) "1"이 될때까지 재귀 호출
3. 재귀를 돌며 카운트된 이진변환 횟수, 제거된 0의 개수 반환

```js
function solution(s) {
    var round = 0;
    var zeroCnt = 0;

    const transform = (strBinary) => {
        // base case - 입력된 binary 문자열이 "1"인 경우
        if (strBinary === "1") {
            return;
        }
            
        round++;
        
        // 2진 변환
        // 1. "0" 제거하며 제거된 0의 개수 카운트
        const arrBinary = [...strBinary].filter(v => {
           if (v === "0") {
               zeroCnt++;
               return false;
           }
           return true;
        });
    
        // 2. "1"로 구성된 배열의 길이를 구함
        const length = arrBinary.length;
    
        // 3. 배열의 길이를 다시 2진수로 변환
        const newStrBinary = length.toString(2);
    
        // 4. base case가 나올 때까지 재귀 호출
        transform(newStrBinary);
    };

    transform(s);
    return [round, zeroCnt];
}
```

### 남의 풀이

* 재귀 대신 while 반복으로 풂
1. 반복하며 answer[0] (round값)을 키움
2. 제거된 0의 개수는 [String.prototype.match](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/String/match) 메서드를 이용, 정규식으로 0에 해당하는 값을 배열로 변환(0이 없으면 빈 배열로 설정)
3. 기존 문자열에서 0을 제거하고 제거된 문자열의 길이의 값으로 2진수 문자열로 변환 후 기존 문자열 대치
4. 대치된 문자열이 1개 이상일 때까지 반복("1"이 남을 때까지 조건)


```js
function solution(s) {
    var answer = [0,0];
    while(s.length > 1) {
        answer[0]++;
        answer[1] += (s.match(/0/g)||[]).length;
        s = s.replace(/0/g, '').length.toString(2);
    }
    return answer;
}
```