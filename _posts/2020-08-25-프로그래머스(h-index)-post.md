---
title: "h-index(정렬응용)"
excerpt: "프로그래머스 코딩테스트 고득점kit 정렬편"

categories:
  - 코딩연습
tags:
  - 알고리즘
  - 코딩연습
  - 정렬

last_modified_at: 2020-08-25
---
## h-index(정렬)
---
오늘은 프로그래머스 고득점kit 정렬파트에 있는 문제입니다. level2문제입니다.

**문제 설명**

> H-Index는 과학자의 생산성과 영향력을 나타내는 지표입니다. 어느 과학자의 H-Index를 나타내는 값인 h를 구하려고 합니다. 위키백과1에 따르면, H-Index는 다음과 같이 구합니다.
>
>어떤 과학자가 발표한 논문 n편 중, h번 이상 인용된 논문이 h편 이상이고 나머지 논문이 h번 이하 인용되었다면 h의 최댓값이 이 과학자의 H-Index입니다.
>
>어떤 과학자가 발표한 논문의 인용 횟수를 담은 배열 citations가 매개변수로 주어질 때, 이 과학자의 H-Index를 return 하도록 solution 함수를 작성해주세요.
>
> 제한사항
> - 과학자가 발표한 논문의 수는 1편 이상 1,000편 이하입니다.
> - 논문별 인용 횟수는 0회 이상 10,000회 이하입니다.

입출력 예

|citations|return|
|-------|------|
|\[3,0,6,1,5]|3|


***
문제를 이해하는데 시간이 오래걸렸던 문제입니다.

**나의 첫번째 풀이**
```python
import statistics

def solution2(citations):
    citations.sort(reverse=True)
    answer = statistics.median(citations)
    return answer
```

처음에는 그저 리스트를 정렬한 뒤 가운데에 있는 인덱스라고 생각했습니다. 지문의 <i>어떤 과학자가 발표한 논문 n편 중, h번 이상 인용된 논문이 h편 이상이고 나머지 논문이 h번 이하 인용되었다면 h의 최댓값이 이 과학자의 H-Index입니다.</i> 이 부분을 잘못이해한 결과입니다.

---

**나의 두번째 풀이**
```python
def solution(citations):
    citations.sort(reverse=True)
    answer = 0
    for i in range(len(citations)):
        if citations[i] < i+1:
            a = citations.index(citations[i-1])
            answer = a+1
            break
    return answer

```
<br>

<img width="259" alt="hindex세번째시도" src="https://user-images.githubusercontent.com/59010218/91116376-2dd47480-e6c7-11ea-97c0-9852165041cc.PNG"><br>


피인용을 내림차순으로 정렬후 인덱스를 1부터 시작하여 두 숫자를 비교하여 내려갑니다. 이때, 두 숫자가 같아지거나 피인용수가 더작아지기 시작하는 직전의 인덱스를 찾아냅니다.

출처 : https://postechlibrary.tistory.com/489

틀린 테스트9,테스트16에 대한 내용을 찾아보니 [22,24]인 경우와 [0] * 1000 에 대한 경우 였습니다. 두 테스트 오류에 대해 처리하지 못하여 다른 사람의 풀이를 보며 공부했습니다.

---

**다른 사람의 첫번째 풀이**
```python
def a_solution1(citations):
  sorted_citations = sorted(citations, reverse=True)
  for i in range(len(sorted_citations)):
    if sorted_citations[i] <= i:
      return i
  return len(sorted_citations)
```
<br>
[22,24]인 경우와 [0] * 1000에 대한 테스트케이스를 해결하는 제 코드와 근접한 풀이입니다. 제 코드와 다른점은 제 코드는 for문안에서 인덱스를 +1 해주었다는 점과 이 분의 코드에서는 for문에서 return되지 않는 경우 citations의 길이 즉, 논문의 수를 return한다는 점 입니다.

---

**다른 사람의 두번째 풀이**
```python
def solution(citations):
    citations.sort(reverse=True)
    answer = max(map(min, enumerate(citations, start=1)))
    return answer
```
enumerate(citations,start1)에서 예를 들면 (1,6), (2,5), (3,3), (4,1), (5,0) 이런식으로 나오게 되며 min함수로 1,2,3,1,0 처럼작은 값들만 나오게 됩니다. 최대값으로 3을 출력하는 풀이입니다.

[위키백과 h-index참고하기](https://en.wikipedia.org/wiki/H-index)
