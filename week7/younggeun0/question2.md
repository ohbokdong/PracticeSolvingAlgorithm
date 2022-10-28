## **[프로그래머스 > 코딩테스트 연습 > 연습문제 > 택배 상자](https://school.programmers.co.kr/learn/courses/30/lessons/131704)**

- 입력
    - order - 택배 기사님이 원하는 상자 순서를 다은 배열
- 출력
    - 영재가 실을 수 있는 상자의 개수

### **내 풀이1 ⇒ 런타임 에러 + 시간 초과(20.0 / 100.0)**

- shift 메서드로 실제로 배열을 조작해서 그런지 런타임 에러 + 시간 초과가 발생
- Pseudo code
    1. 기존 컨테이너, 보조 컨테이너 역할을 할 배열과 실은 상자 수를 담을 변수 생성
    2. 택배 기사님이 원하는 순서대로 실을 수 있는지 탐색
        1. 실을 수 없다면 보조 컨테이너에 보관(stack)
        2. 실을 수 있다면 반환할 실은 상자 수를 증가시키고 기존 컨테이너에서 상자 제거
        3. 보조 컨테이너에서 최상단 상자와 기존 컨테이너 제일 앞의 상자가 택배 기사가 원하는 상자가 아니라면 종료
    3. 계산된 실은 상자 수 반환

```js
function solution(order) {
    // 컨테이너, 보조컨테이너 생성
    const container = order.map((_, i) => {
        return i + 1;
    });
    const subcontainer = [];
    // 실은 상자 수를 저장할 변수 생성
    let loadableBoxes = 0;
    
    // 택배 기사가 요청한 상자 순서대로 순회
    for (let i=0; i<order.length; i++) {
        if (!loadBox(container[0], order[i])) {
            break;   
        }
    }
    
    return loadableBoxes;
    
    
    function loadBox(boxOnContainer, box) {
        if (boxOnContainer == null || boxOnContainer > box) {
            if (boxOnSubContainer() === box) {
                loadableBoxes++;
                subcontainer.pop();
                return true;
            }
            return false;
        } else if (boxOnContainer === box) {
            loadableBoxes++;
            container.shift();
            return true;
        }
        
        subcontainer.push(boxOnContainer);
        container.shift();
        
        return loadBox(container[0], box);
    }
    
    function boxOnSubContainer() {
        return subcontainer[subcontainer.length - 1];
    }
}
```

### 내 풀이2 ⇒ 런타임 에러 (50.0/ 100.0)

- shift로 container 배열을 조작하던 걸 pointer p를 두고 이동시키도록 수정
- 런타임 에러가 계속 발생, 재귀 콜스택 제한 때문에 걸린 듯 함

```js
function solution(order) {
    // 컨테이너, 보조컨테이너 생성
    let p = 0;
    const container = order.map((_, i) => {
        return i + 1;
    });
    const subcontainer = [];
    // 실은 상자 수를 저장할 변수 생성
    let loadableBoxes = 0;
    
    // 택배 기사가 요청한 상자 순서대로 순회
    for (let i=0; i<order.length; i++) {
        if (!loadBox(container[p], order[i])) {
            break;   
        }
    }
    
    return loadableBoxes;
    
    
    function loadBox(boxOnContainer, box) {
        if (boxOnContainer == null || boxOnContainer > box) {
            if (boxOnSubContainer() === box) {
                loadableBoxes++;
                subcontainer.pop();
                return true;
            }
            return false;
        } else if (boxOnContainer === box) {
            loadableBoxes++;
            p++;
            return true;
        }
        
        subcontainer.push(boxOnContainer);
        p++;
        
        return loadBox(container[p], box);
    }
    
    function boxOnSubContainer() {
        return subcontainer[subcontainer.length - 1];
    }
}
```

### 내 풀이3

- 재귀 방식에서 반복 방식으로 변경하니 풀림

```js
function solution(order) {
    // 컨테이너, 보조컨테이너 생성
    let p = 0;
    const container = order.map((_, i) => {
        return i + 1;
    });
    const subcontainer = [];
    // 실은 상자 수를 저장할 변수 생성
    let load = 0;
    
    // 택배 기사가 요청한 상자 순서대로 순회
    for (let i=0; i<order.length; i++) {
        if (!loadBox(order[i])) {
            break;
        }
    }
    
    return load;

    
    // nested helper functions
    function loadBox(box) {
        let loadable = true;
        
        // 재귀 방식 -> 반복 방식
        while(loadable) {
            if (boxOnContainer() == null || boxOnContainer() > box) {
                if (boxOnSubContainer() === box) {
                    load++;
                    subcontainer.pop();
										break;
                }
                loadable = false;
                break;
            } else if (boxOnContainer() === box) {
                load++;
                p++;
                break;
            }

            subcontainer.push(boxOnContainer());
            p++;
        }
        return loadable;
    }

    function boxOnContainer() {
        return container[p];
    }
    
    function boxOnSubContainer() {
        return subcontainer[subcontainer.length - 1];
    }
}
```