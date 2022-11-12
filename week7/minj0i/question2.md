## **[프로그래머스 > 코딩테스트 연습 > 연습문제 > 택배 상자](https://school.programmers.co.kr/learn/courses/30/lessons/131704)**

- 입력
    - order - 택배 기사님이 원하는 상자 순서를 담은 배열
- 출력
    - 영재가 실을 수 있는 상자의 개수

### **내 풀이

```js
function solution(order) {
    let count = 0;
    const stack = [];
    // 1부터 시작 (상자 0이 없으니까)
    for(let i = 1; i <= order.length; i++) {
        // 일단 stack에다 넣는다
        stack.push(i);
        // order랑 비교해서 stack의 마지막과 같은 거라면
        while(stack.length > 0 && stack[stack.length - 1] === order[count]) {
            // 빼고 카운트 올려준다
            stack.pop();
            count++;
        }
    }
    return count;
}
```