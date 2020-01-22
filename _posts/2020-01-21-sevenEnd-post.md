---
title: "2020.01.21 스터디 7회차 마무리하며"
excerpt: "백준 복습 및 문제 풀이 + 회화"

categories:
  - Blog
tags:
  - Blog
last_modified_at: 2019-01-14
---
오늘은 백준 두문제를 풀었습니다.  

가장 긴 바이토닉 부분수열 (11054번)  
풀이 : 이 문제는 수열이 주어졌을때 그 수열의 바이토닉 부분 수열 중에서 가장 긴 것을 구하는 문제입니다.  
D[i]=i에서 끝나는 가장 긴 증가하는 부분수열과 D2[i]=i에서 시작하는 가장 긴 감소하는 부분 수열의 합을 구해 겹치는 부분 -1을 해주고 그 중 최댓값을 구하면 됩니다.  
D[i]의 점화식은 max(d[i] < d[j] + 1)이며 j의 조건은 j<i,a[j]<a[i]입니다.  
D2[i]의 점화식은 max(d[i] < d[j] + 1)이며 j의 조건은 j>i,a[j]<a[i]입니다.  
위 점화식을 아래의 코드로 나타낼 수 있습니다.  
~~~java
int[] d = new int[n];

for (int i = 0; i < n; i++) { //D[i]=i에서 끝나는 가장 긴 증가하는 부분수열
  d[i] = 1;
  for (int j = 0; j < i; j++) {
    if (a[i] > a[j] && d[i] < d[j] + 1) {
      d[i] = d[j] + 1;
    }
  }
}
int[] d2 = new int[n];

for (int i = n - 1; i >= 0; i--) { //D2[i]=i에서 시작하는 가장 긴 감소하는 부분 수열의 합을 구해 겹치는 부분
  d2[i] = 1;
  for (int j = i + 1; j < n; j++) {
    if (a[i] > a[j] && d2[i] < d2[j] + 1) {
      d2[i] = d2[j] + 1;
    }
  }
}
int ans = d[0] + d2[0] - 1; //겹치는 부분에 대해서 -1 을 해야합니다.
for (int i = 0; i < n; i++) {
  if (ans < d[i] + d2[i] - 1) {
    ans = d[i] + d2[i] - 1;
  }
}
System.out.println(ans);

~~~  


연속합 (13398번)  
풀이 : 수열의 연속합 중 가장 큰 합을 구하는 문제입니다. 수는 하나 제거하거나 하지 않아도 됩니다. 점화식을 먼저 세우면 D[i] = i번쨰에서 끝나는 연속합, D2[i] = i번째에서 시작하는 연속합 을 구한 후 임의의 수 하나를 제거한 후의 식은 D[k-1] + D[k+1]가 됩니다. D[i]의 최댓값과 D[k-1] + D[k+1]의 최댓값을 비교하여 큰 값이 답이 됩니다.  

~~~java
for (int i = 0; i < n; i++) { // D[i] = i번쨰에서 끝나는 연속합
			d[i] = a[i];
			if (i == 0) {
				continue;
			}
			if (a[i] < d[i - 1] + a[i]) {
				d[i] = d[i - 1] + a[i];
			}
		}

		for (int i = n - 1; i >= 0; i--) { //D2[i] = i번째에서 시작하는 연속합
			d2[i] = a[i];
			if (i + 1 == n) {
				continue;
			}
			if (a[i] < d2[i + 1] + a[i]) {
				d2[i] = d2[i + 1] + a[i];
			}
		}
    // D[i]의 최댓값과 D[k-1] + D[k+1]의 최댓값을 비교하여 큰 값이 답
		int ans = d[0];
		for (int i = 1; i < n; i++) {
			if (ans < d[i]) {
				ans = d[i];
			}
		}
		for (int i = 1; i < n - 1; i++) { //임의의 수 하나를 제거한 후의 식은 D[k-1] + D[k+1]
			if (ans < d[i - 1] + d2[i + 1]) {
				ans = d[i - 1] + d2[i + 1];
			}
		}
		System.out.println(ans);

~~~
