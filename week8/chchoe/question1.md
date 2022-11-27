## [프로그래머스 > 코딩테스트 연습 > 삼총사](https://school.programmers.co.kr/learn/courses/30/lessons/131705)

* 입력 - 숫자 배열
* 출력 - 세 숫자를 더해서 합이 0이 되는 경우의 수

### 내 풀이(cpp)

```c++
int solution(vector<int> number) {
	int answer = 0;
	int numberMaxSize = number.size();
	for (int firstIndex = 0; firstIndex < numberMaxSize - 2; ++firstIndex)
	{
		for (int secondIndex = firstIndex + 1; secondIndex < numberMaxSize - 1; ++secondIndex)
		{
			for (int thirdIndex = secondIndex + 1; thirdIndex < numberMaxSize; ++thirdIndex)
			{
				int value = number.at(firstIndex) + number.at(secondIndex) + number.at(thirdIndex);
				if (value == 0)
					++answer;
			}
		}
	}
	return answer;
}
```
