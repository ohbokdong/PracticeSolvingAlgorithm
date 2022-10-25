## **[프로그래머스 > 코딩테스트 연습 > 월간 코드 챌린지 시즌2 > 음양 더하기](https://school.programmers.co.kr/learn/courses/30/lessons/76501)**

- 입력
    - absolutes - 정수값을 담은 배열
    - signs - 정수값의 부호를  boolean 값으로 담은 배열
- 출력
    - 부호가 적용된 정수들의 합

### **내 풀이**

1. true, false가 담긴 signs 배열을 1과 -1로 맵핑
2. reduce 함수로 부호를 맵핑한 정수를 구하고 누적합 후 반환

```jsx
function solution(absolutes, signs) {
    signs = signs.map(sign => sign ? 1 : -1);
    return absolutes.reduce((acc, absolute, idx) => {        
        return acc + absolute * signs[idx];
    }, 0);
}
```

### **남의 풀이1**

- 내 풀이 1단계를 생략하고 reduce 콜백 함수의 매개변수로 전달된 인덱스를 이용하여 부호를 누적합 하는 시점에서 계산

```jsx
function solution(absolutes, signs) {
    return absolutes.reduce((acc, val, i) => acc + (val * (signs[i] ? 1 : -1)), 0);
}
```

### 남의풀이2

- forEach문을 이용하여 누적합을 구함