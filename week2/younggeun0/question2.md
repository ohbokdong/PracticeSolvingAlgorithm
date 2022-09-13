# [프로그래머스 > 코딩테스트 연습 > 연습문제 > 최댓값과 최솟값](https://school.programmers.co.kr/learn/courses/30/lessons/12939)

* 입력 - 공백으로 구분된 숫자들이 저장된 문자열
* 출력 - "(최솟값) (최대값)" 형태의 문자열

### 내 풀이
1. 공백을 구분자로 문자열을 배열로 변경
2. 문자열 값을 숫자로 변경
3. 숫자의 배열을 오름차순으로 정렬
4. 처음 수와 마지막 수를 템플릿 리터럴을 이용해서 반환

```js
function solution(s) {
    const sorted = s.split(" ").map(s => parseInt(s)).sort((a, b) => a - b);
    
    return `${sorted[0]} ${sorted[sorted.length-1]}`;
}
```

### 남의 풀이

* 자동형변환과 스프레드 연산자를 이용해서 Math.min, Math.max로 최소 최대 값을 구함

```js
function solution(s) {
    const arr = s.split(' ');

    return Math.min(...arr)+' '+Math.max(...arr);
}
```