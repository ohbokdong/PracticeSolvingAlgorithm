# [프로그래머스 > 코딩테스트 연습 > 완전 탐색 > 카펫](https://https://school.programmers.co.kr/learn/courses/30/lessons/42842)

* 입력 - (brown, yellow)
* 출력 - [가로, 세로]

### 내 풀이

* brown = 가로*2 + (세로 - 2)*2
* yellow = (가로 - 2)*(세로 - 2)
* 따라서 가로의 최댓값은 brown / 2 - 1의 값과 같다('최댓값'이므로 세로를 1이라고 생각하는 것)
* 가로의 최댓값부터 --
* 세로의 값이 가능한 경우는 yellow / (가로 - 2)를 한 나머지가 0인 경우의 + 2 한 값
* if문 안에서 brown과 yellow 값으로 나오는지를 판단

```js
function solution(brown, yellow) {
    var answer = [];
    
    for(let width = brown/2 - 1; width>0; width--) {
        if(yellow/(width - 2) % 1 === 0) {
            let height = yellow/(width-2) + 2
            if(width*2 + 2*(height-2) === brown && (width - 2)*(height - 2) === yellow) {
                // 여기에서 바로 return 해주지 않으면 width < height인 경우가 생길수도 있으므로 바로 해준다.
                return [width, height]   
            }
        }
    }
    return answer
}
```