# [프로그래머스 > 코딩테스트 연습 > 2022 KAKAO TECH INTERNSHIP > 두 큐 합 같게 만들기](https://school.programmers.co.kr/learn/courses/30/lessons/118667)

* 입력 - 임의의 수가 들어있는 두 큐(배열)
* 출력 - 큐의 합이 같아질 때까지 한 작업의 최소값
    * pop과 insert를 묶어 하나의 작업으로 셈

### 내 풀이
* 두 큐의 크기를 비교해서 큰 쪽의 원소를 빼서 작은 쪽에 넣는 작업을 반복함
* 원소의 합을 같게 만들 수 없는 경우를 반복하던 중 큐의 크기가 0이 되는 경우라 생각하여 이 때 -1을 반환하도록 함
* 시간 초과로 인해 `63.0/100` 점수만 받고 풀지 못 함

```js
function solution(queue1, queue2) {
    let jobCnt = 0;
    let isEmpty = false;

    const getQueueSum = (queue) => {
        return queue.reduce((a, b) => (a + b), 0);
    };
    
    const checkEmpty = (queue1, queue2) => {
        isEmpty = queue1.length === 0 || queue2.length === 0;
        return isEmpty;
    };
    
    let queueSum1 = getQueueSum(queue1);
    let queueSum2 = getQueueSum(queue2);
    
    // 두 큐의 합을 비교하고 큰 쪽의 값을 꺼내 적은 쪽에 넣음
    while(!checkEmpty(queue1, queue2) && queueSum1 !== queueSum2) {
        if (queueSum1 > queueSum2) {
            queue2.push(queue1[0]);
            queue1 = queue1.slice(1);
        } else {
            queue1.push(queue2[0]);
            queue2 = queue2.slice(1);
        }
        queueSum1 = getQueueSum(queue1);
        queueSum2 = getQueueSum(queue2);
        jobCnt++;
    }
    
    if (isEmpty) return -1;
    
    return jobCnt;
}
```

### 남의 풀이

* [다중 포인터를 이용한 풀이](https://gurtn.tistory.com/179)
* 큐의 FIFO 성질을 이용해서 실제로 매번 배열 생성과 합을 구하지 않고 포인터를 이동하며 window의 값을 변경하는 문제
    * multi pointers + sliding window 패턴

```js
function solution(queue1, queue2) {
    const getQueueSum = (arr) => arr.reduce((acc, v) => acc + v, 0);

    let sumQ1 = getQueueSum(queue1);
    let sumQ2 = getQueueSum(queue2);
    
    let p1 = 0;
    let p2 = queue1.length;
    
    const target = (sumQ1 + sumQ2) / 2;
    const queue = [...queue1, ...queue2];
    //  p1 ->    p2 ->
    //  |        | 
    // [3, 2, 7, 2, 4, 6, 5, 1]

    // 작업의 최대 경우의 수가 왜 queue1의 길이 * 3일까?
    // - q1과 q2를 맞바뀐 경우 queue1.length * 2
    // - q1과 q2가 맞바뀐 후 다시 찾는 경우 queue1.length * 3 
    //  p1 ->    p2 ->
    //  |        | 
    // [4, 6, 5, 1, 3, 2, 7, 2]
    const end = queue1.length * 3;
    
    for (let count = 0; count < end; count++) {
        if (sumQ1 === target) return count;
        
        if (sumQ1 > target) {
            sumQ1 -= queue[p1++];
        } else {
            sumQ1 += queue[p2++];
        }
    }
    
    return -1;
}

solution([3, 2, 7, 2], [4, 6, 5, 1]);
```