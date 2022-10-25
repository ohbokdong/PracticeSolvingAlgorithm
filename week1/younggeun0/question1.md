# [프로그래머스 > 코딩테스트 연습 > 완전탐색 > 최소직사각형](https://school.programmers.co.kr/learn/courses/30/lessons/86491)

* 입력 - 명합 사이즈([w, h])가 담긴 배열
* 출력 - 모든 명함을 담을 수 있는 최소 명함 지갑의 사이즈

### 내 풀이
* 가로 길이보다 세로가 긴 경우 회전시키고 명함의 가장 긴 가로, 세로 길이를 구함

```js
function solution(sizes) {
    let longestWidth = 0;
    let longestHeight = 0;
    
    sizes.forEach(size => {
        if (size[1] > size[0]) { // 세로가 더 길면
            [size[1], size[0]] = [size[0], size[1]]; // swap
        }
        longestWidth = Math.max(longestWidth, size[0]);
        longestHeight = Math.max(longestHeight, size[1]);
    });
    
    return longestWidth * longestHeight;
}
```
