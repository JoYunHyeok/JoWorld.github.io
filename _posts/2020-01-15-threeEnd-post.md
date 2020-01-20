---
title: "2020.01.14 스터디 3회차 마무리하며"
excerpt: "백준 복습 및 문제 풀이 + 회화"

categories:
  - Blog
tags:
  - Blog
last_modified_at: 2019-01-14
---

모각코 세번째 스터디를 마무리하며 백준 과제 리뷰와 3문제를 풀었습니다.  

연속합 (1912번)  
<문제>  
n개의 정수로 이루어진 임의의 수열이 주어집니다. 이 중 연속된 몇개의 수를 선택해서 구할 수 있는 합 중 가장 큰합을 구해야하며 단, 수는 한개 이상을 선택해야 합니다.  
예를 들어 10, -4, 3, 1, 5, 6, -35, 12, 21, -1 이라는 수열이 주어졌을때 여기서 정답은 12 + 31 = 33 이 됩니다.  

<이해>
먼저 이 문제를 이해할때 음수를 기준으로 (10), (3,1,5,6), (12,21)로 구분하여 더하면 답이 나오지만 3, -1, 3 이라는 임의의 수열이라면 답이 5가 나오며 음수도 의미가 있을때가 있는 예외가 있었습니다.

<해결>
이 문제를 해결하려면 각각의 수에 대해 연속합을 구해야하며 앞에있는 수와 연속하는 경우와 연속하지 않는 경우로 나누어 구해야합니다.

A배열은 입력되는 수열을 위해 생성합니다.
D배열은 i번째 수로 끝나는 가장 큰 연속합을 위해 생성하는 배열 입니다.
1.앞에 있는 수와 연속하는 경우 : D[i-1] + A[i]
2.연속하지 않는 경우 : A[i]

이 문제의 핵심부분을 코딩한다면 아래와 같은 코드가 나옵니다.
for(int i = 0; i < n; i++){
  d[i] = a[i]; //연속하지 않는 경우
  if(i == 0){
    continue;//0이면 바로 반복문으로
  }
  if(d[i] < d[i-1] + a[i]) // 앞에있는 수와 연속하는 경우
     d[i] = d[i-1] + a[i]
}

<느낀점>
문제를 이해하는 부분에서 시간을 많이 소비했고 핵심부분을 코딩하는 부분에서도 많이 막혀 풀지 못했지만 문제를 푼 조원의 설명과 백준에서 제공하는 답을 보고 이해하게 되었습니다.





제곱수의 합 (1699번)
<문제>
어떤 자연수 N은 그보다 작거나 같은 제곱수들의 합으로 나타낼 수 있습니다. 예를 들면 11 = 3^2 + 1^2 + 1^2(3개항), 11 = 2^2 + 2^2 + 1^2 + 1^2 + 1^2(5개항)도 가능합니다. 이 경우, 수학자 숌크라테스는 "11은 3개 항의 제곱수 합으로 표현할 수 있다."라고 말합니다. 또한 11은 그보다 적은 항의 제곱수 합으로 표현할 수 없으므로, 11을 그 합으로써 표현할 수 있는 제곱수 항의 최소 개수는 3입니다.
주어진 자연수 N을 이렇게 제곱수들의 합으로 표현할 떄에 그 항의 최소개수를 구하는 프로그램을 작성하세요.

<이해>
? + ? + ''' + ? + ? = N이 된다고 했을때 마지막 ? 값을 알면 되는 문제이며 이 자리에 올 수 있는 값은 제곱수들입니다. 제곱수들은 무수히 많기 때문에 i라는 변수를 두어 i^2으로 둡니다. i^2을 제외한 나머지는 N-i^2이 되고 정리한다면 (N-i^2) + i^2 = N이 됩니다.  
점화식으로 정의하면 D[N] = min(D[N-i^2]) + 1 이 됩니다.(1^2 <= i^2 <= N)

<해결>
이해 단계에서 세운 점화식을 코딩으로 옮겨 본다면 아래와 같은 코드가 나옵니다.
~~~java
for(int i = 0; i <= n; i++){
  d[i] = i; // 최솟값을 구하는 문제이므로 올수있는 최댓값으로 초기화 시켜줍니다.
  for(int j = 1; j*j <= i; j++){
    if(d[i] > d[i-j*j] + 1){
      d[i] = d[i-j*j] + 1;
    }
  }
}
~~~
<느낀점>
처음에 단순히 입력받은 N에 루트를 씌어준후 내림하여 얻은 값으로 N을 나누고 몫과 나머지를 구하는 방식으로 코딩하였지만 숫자가 커지면 이상한 값이 나왔습니다. 이 문제를 풀고 점화식을 이용한 다이나믹 프로그래밍을 조금 더 이해하였습니다.




합분해 (2225번)
<문제>
0부터 N까지의 정수 K개를 더해서 그 합이 N이 되는 경우의 수를 구하는 프로그램을 작성하시오.
덧셈의 순서가 바뀐 경우는 다른 경우로 센다.(1+2와 2+1은 서로 다른 경우). 또한 한 개의 수를 여러번 쓸 수도 있다.

<이해>
먼저, 점화식을 세우면
D[K][N] = 0부터 N까지의 정수 K개를 더해서 그 합이 N이 되는 경우의 수
? + ? + ''' + ? + ?(K개) = N 이 경우도 마찬가지로 마지막에 올 수있는 수에 변수를 둔다. L이라고 둔다면 (N-L) + L = N  (N-L)의 갯수는 K-1이 된다.
즉, D[K][N] = D[k-1][N-L] (0<=L<=N) 식이 나오게 됩니다.

<해결>
점화식을 코딩으로 옮겨본다면 아래와 같습니다. 변수가 세개라서 for문을 세개를 써주었습니다.
for(int i = 1; i <= k; i++){
  for(int j = 0; j <= n; j++){
    for(int l = 0; l <= j; l++){
      d[k][n] += d[k-1][j-l];
    }
  }
}

<느낀점>
백준 다이나믹 프로그래밍 파트를 풀기에 다 비슷한 방법으로 풀었지만 아직 익숙치가 않아 연습문제를 더 풀어야 겠다고 느꼇습니다.