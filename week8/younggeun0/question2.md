## [프로그래머스 > 코딩테스트 연습 > 완전 탐색 > 카펫](https://school.programmers.co.kr/learn/courses/30/lessons/42842)

- 입력 - brown, yellow격자의 개수
- 출력 - 가로 길이, 세로 길이를 담은 배열 `[가로, 세로]`

### 내 풀이 (JS)

- yellow 높이를 1부터 차례대로 증가시키면서 브라운값을 찾는 방식
    1. yellow 높이가 1인 경우 부터 시작
    2. yellow의 너비 높이값으로 카펫의 너비 높이를 구함 (yellow 기준으로 +2)
    3. 카펫 사이즈에서 옐로우 사이즈를 뺀 뒤 브라운 사이즈와 비교
        - 브라운 격자 값과 같다면 정답
        - 다르다면 yellow 높이를 증가시켜서 반복

```jsx
function solution(brown, yellow) {
    var answer = [];
    
    // 3x3(9) 이상, 
    // 8 <= brown <= 5000
    // 1 <= yellow <= 2000000
    // brown + yello = w * h
    // w >= h
    
    // yellow 격자 높이가 1부터 시작해 yellow 격자의 형태로 만들어지는 모든 경우의 수 확인
    let yellowW = yellow;
    let yellowH = 1;

    while (true) {
        // yellow + 2한 결과가 카펫의 사이즈
        const carpetW = yellowW + 2;
        const carpetH = yellowH + 2;
        
        const yellowSize = yellowW * yellowH;
        const carpetSize = carpetW * carpetH;
        
        // carpet사이즈에서 yellow 사이즈를 빼서 brown의 개수를 구함        
        // brown의 개수가 주어진 개수와 같으면 해당 carpet사이즈가 정답
        if (brown == carpetSize - yellowSize) {
            answer.push(carpetW);
            answer.push(carpetH);
            break;
        } else {
            // brown의 개수가 다를 경우 yellow의 높이를 키우고, yellow 너비값 수정
            yellowH++;
            yellowW = yellow / yellowH;
        }
    }
    
    return answer;
}
```

### 내 풀이 (Python)

```python
def solution(brown, yellow):
    answer = []
    
    yellow_width = yellow
    yellow_height = 1
    
    while True:
        carpet_width = yellow_width + 2
        carpet_height = yellow_height + 2
        
        yellow_size = yellow_width * yellow_height
        carpet_size = carpet_width * carpet_height
        
        if brown == carpet_size - yellow_size:
            answer = [carpet_width, carpet_height]
            break;
        else:
            yellow_height += 1
            yellow_width = yellow / yellow_height
    
    return answer
```

### 다른 사람의 풀이 (JS)

1. 최소 높이 3의 카펫의 너비(`w`) 높이(`h`)를 먼저 구함
    - brown, yellow를 더한 뒤 최소 높이 3으로 나눠 카펫의 너비 높이를 계산
2. 계산된 카펫의 너비, 높이에서 -2씩 줄이고 곱한 값이 yellow 격자의 값과 동일한지 비교
    - 같으면 구한 너비 높이 값이 맞으므로 반복문 종료 후 너비 높이 반환
    - 다르면 카펫의 높이를 증가시킨 후 위 카펫의 너비 계산과정 반복

```jsx
function solution(brown, yellow) {
    const answer = [];
    let w;
    for(var h = 3; h <= (brown + yellow) / h; h++) {
        w = Math.floor((brown + yellow) / h);
        if((w - 2) * (h - 2) === yellow) {
            break;
        }
    }

    return [w, h];
}
```

### 다른 사람의 풀이(Python)

```python
def solution(brown, yellow):
    for i in range(1, int(yellow**(1/2))+1):
        if yellow % i == 0 and 2*(i + yellow//i) == brown-4:
            return [yellow//i+2, i+2]
```
