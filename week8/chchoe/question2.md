# [프로그래머스 > 코딩테스트 연습 > 완전 탐색 > 카펫](https://https://school.programmers.co.kr/learn/courses/30/lessons/42842)

* 입력 - (brown, yellow)
* 출력 - [가로, 세로]

### 내 풀이(cpp)

```c++
vector<int> solution(int brown, int yellow) {
	vector<int> answer;
	int total = brown + yellow;
	
	if (yellow == 1)
	{
		answer.push_back(3);
		answer.push_back(3);
		return answer;
	}
    
	for (int yellowY = 1; yellowY <= yellow; ++yellowY)
	{
		int yellowX = yellow / yellowY;
		int yellowMax = yellowX * yellowY;
		if (yellow != yellowMax)
			continue;

		int tempTotalX = yellowX + 2;
		int tempTotalY = yellowY + 2;

		int tempTotal = tempTotalX * tempTotalY;
		if (total == tempTotal)
		{
			answer.push_back(tempTotalX);
			answer.push_back(tempTotalY);
			break;
		}
	}

	return answer;
}

```