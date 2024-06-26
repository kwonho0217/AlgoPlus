# [Silver I] RGB거리 - 1149 

[문제 링크](https://www.acmicpc.net/problem/1149) 

### 분류

다이나믹 프로그래밍

### 문제 설명

<p>RGB거리에는 집이 N개 있다. 거리는 선분으로 나타낼 수 있고, 1번 집부터 N번 집이 순서대로 있다.</p>

<p>집은 빨강, 초록, 파랑 중 하나의 색으로 칠해야 한다. 각각의 집을 빨강, 초록, 파랑으로 칠하는 비용이 주어졌을 때, 아래 규칙을 만족하면서 모든 집을 칠하는 비용의 최솟값을 구해보자.</p>

<ul>
	<li>1번 집의 색은 2번 집의 색과 같지 않아야 한다.</li>
	<li>N번 집의 색은 N-1번 집의 색과 같지 않아야 한다.</li>
	<li>i(2 ≤ i ≤ N-1)번 집의 색은 i-1번, i+1번 집의 색과 같지 않아야 한다.</li>
</ul>

### 입력 

 <p>첫째 줄에 집의 수 N(2 ≤ N ≤ 1,000)이 주어진다. 둘째 줄부터 N개의 줄에는 각 집을 빨강, 초록, 파랑으로 칠하는 비용이 1번 집부터 한 줄에 하나씩 주어진다. 집을 칠하는 비용은 1,000보다 작거나 같은 자연수이다.</p>

### 출력 

 <p>첫째 줄에 모든 집을 칠하는 비용의 최솟값을 출력한다.</p>



#  🚀  오답노트 

```diff
-import java.io.BufferedReader;
-import java.io.IOException;
-import java.io.InputStreamReader;
-import java.util.StringTokenizer;
-
-public class Main {
-	public static void main(String[] args) throws NumberFormatException, IOException {
-		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
-		StringTokenizer st;
-		int N = Integer.parseInt(br.readLine());
-		int[][] houses = new int[N][3];
-		for (int i = 0; i < N; i++) {
-			st = new StringTokenizer(br.readLine());
-			houses[i][0] = Integer.parseInt(st.nextToken());
-			houses[i][1] = Integer.parseInt(st.nextToken());
-			houses[i][2] = Integer.parseInt(st.nextToken());
-		}
-		int[][] color = new int[N][3];
-		color[0][0] = houses[0][0];
-		color[0][1] = houses[0][1];
-		color[0][2] = houses[0][2];
-		for (int i = 1; i < N; i++) {
-			color[i][0] = Math.min(color[i - 1][1] + houses[i][0], color[i - 1][2] + houses[i][0]);
-			color[i][1] = Math.min(color[i - 1][0] + houses[i][1], color[i - 1][2] + houses[i][1]);
-			color[i][2] = Math.min(color[i - 1][0] + houses[i][2], color[i - 1][1] + houses[i][2]);
-		}
-		int ans = color[N - 1][0];
-		ans = Math.min(ans, color[N - 1][1]);
-		ans = Math.min(ans, color[N - 1][2]);
-		System.out.println(ans);
-	}

```


 ## 🏆 전체 코멘트 

