### [프로그래머스 > 코딩 테스트 연습 > Summer/Winter Coding(2019) > 멀쩡한 사각형](https://school.programmers.co.kr/learn/courses/30/lessons/62048)

- 입력
    - 가로(w), 세로(h) 길이 - 1억 이하의 자연수
- 출력
    - 대각선 꼭지점 2개를 잇는 방향으로 잘려 있을 때, 사용할 수 있는 1cm * 1cm 정사각형의 개수

### 내 풀이

* 1차 함수를 이용하면 풀 수 있을 것 같았으나 수학 지식이 0에 수렴하여 남의 풀이를 참고...🫠

### [남의 풀이1 - 1차 함수를 이용한 풀이](https://non-stop.tistory.com/248)

1. `y = (h/w)*x`와 같은 1차 함수로 표현 가능
2. x가 0일 때 y도 0이기 때문에 1부터 대각선 밑에 존재하는 사각형의 개수를 구함
3. x가 1일 때, y는 1.5, 정사각형의 높이를 구해야 하므로 y를 정수로 바꾼 값이 정사각형으로 채울 수 있는 최대 높이이자 최대 개수
4. w-1까지 대각선 밑에 있는 정사각형의 개수를 누적합
5. 직사각형은 직각삼각형 두개로 나눠져 있기 때문에 *2 해서 총 개수를 구함

```js
function solution(w, h) {
    var answer = 0;

    for (let i=1; i<w; i++) {
        // (h/w) * i로 계산 시 6번 테스트 실패, 부동 소수점 곱하기 연산이 부정확해 발생한 현상이라고 함, 때문에 나누고 곱하는 대신 곱하고 나누도록 변경하면 통과됨
        answer += Math.floor(h * i / w);
    }
    answer *= 2;

    return answer;
}
```

### 남의 풀이2 - 최대 공약수를 이용한 풀이

* `최대공약수(Greatest Common Divisor, GCD)`
  * `공약수(Common Divisor)` - 두 수 이상의 여러 수의 공통된 약수
  * `최대공약수(GCD)`란 두 수 이상의 여러 수의 공약수 중 최대인 수
* [`서로소(Coprime)`](https://ko.wikipedia.org/wiki/%EC%84%9C%EB%A1%9C%EC%86%8C) - 공약수가 1뿐인 두 정수나, 공약수가 0이 아닌 상수뿐인 두 다항식이나, 환 전체를 생성하는 두 아이디얼의 관계
* `가로 + 세로 - 최대공약수`가 대각선을 지나는 사각형의 갯수가 됨

[풀이 참고1](https://velog.io/@ajufresh/%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%A8%B8%EC%8A%A4-%EB%A9%80%EC%A9%A1%ED%95%9C-%EC%82%AC%EA%B0%81%ED%98%95-%EB%AC%B8%EC%A0%9C%ED%92%80%EC%9D%B4-Java)

1. 대각선으로 직사각형이 나뉘는 패턴을 분석
2. h, w의 최대공약수로 나눈 만큼 h, w가 증가되는 것을 발견
3. 패턴 직사각형의 크기 === `2(w/gcd) * 3(h/gcd)`
4. 사용 못하는 정사각형은 `총 정사각형의 개수 - (가로길이 + 세로길이 - 1)`이 되는 것을 발견
5. 직사각형 패턴은 최대 공약수만큼 반복되는 것을 발견
6. 전체 크기 - 한 패턴 직사각형 당 사용하지 못하는 정사각형 크기 * 반복 횟수 === `(w * h) - (((w/gcd) + (h/gcd) - 1) * gcd)`

[풀이 참고2](https://school.programmers.co.kr/learn/courses/30/lessons/62048/solution_groups?language=javascript&type=all)

1. 사각형의 w와 h가 서로소(두 수 사이의 관계가 1 이외의 공약수가 없는 수)인 경우 잘린 정사각형의 갯수 === `w + h - 1`
2. 사각형에서 서로소 관계의 사각형의 갯수 === 최대 공약수(gcd)
3. 잘린 정사각형의 개수는 `gcd * ((w / gcd) + (h / gcd) - 1)` === `w + h - gcd`

```js
function solution(w,h){
    const gcd = (a, b) => {
        return b === 0 ? a : gcd(b, a % b);
    };

    return w * h - (w + h - gcd(w, h));
}
```
