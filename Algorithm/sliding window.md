
# sliding window 알고리즘

## 예제 

-  문자열에서 모음 문자가 가장 많이 등장하는 길이가 k인 부분 문자열 찾기
- 시간제한 : 1.000 sec  메모리제한 : 128 MB  
- 문제 설명
	- 영소문자로 구성된 문자열과 정수 k가 주어진다. 이 문자열 중 길이가 k인 부분 문자열 중에 모음 문자('a','e','i','o','u')가 가장 많이 등장하는 부분 문자열을 찾고, 그 부분 문자열에 있는 모음 수를 출력해 주세요
- 입력 설명
	- 첫 줄에는 테스트케이스 T(1<=T<=1,000)이 주어집니다. 각 테스트케이스는 두 줄로 구성되어 있습니다. 첫 줄에는 영소문자로 구성된 문자열 S(1<=len(S)<=100,000)가 주어집니다. 둘째 줄에는 정수 k(1<=k<=len(S))가 주어집니다.
- 출력 설명
	- 각 테스트케이스마다 길이가 k인 부분 문자열 중에 모음 문자가 가장 많이 등장하는 부분 문자열을 찾고, 찿은 부분 문자열에 있는 모음 문자의 수를 출력해 주세요.
-  입력 예시
```
3
abciiidef
3
aeiou
2
koreatech
3
```
- 출력 예시
```
3
2
2
```


- 아예 처음부터 -'a' 로 색인값을 바꾸고 계산
- 문자열 수정 필요없으면 `string_view  이용
- for문으로 두 구간으로 나눠서 해봐라