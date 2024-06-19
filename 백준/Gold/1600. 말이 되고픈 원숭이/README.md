# [Gold III] 말이 되고픈 원숭이 - 1600 

[문제 링크](https://www.acmicpc.net/problem/1600) 

### 분류

너비 우선 탐색, 그래프 이론, 그래프 탐색

### 문제 설명

<p>동물원에서 막 탈출한 원숭이 한 마리가 세상구경을 하고 있다. 그 녀석은 말(Horse)이 되기를 간절히 원했다. 그래서 그는 말의 움직임을 유심히 살펴보고 그대로 따라 하기로 하였다. 말은 말이다. 말은 격자판에서 체스의 나이트와 같은 이동방식을 가진다. 다음 그림에 말의 이동방법이 나타나있다. x표시한 곳으로 말이 갈 수 있다는 뜻이다. 참고로 말은 장애물을 뛰어넘을 수 있다.</p>

<table class="table table-bordered" style="width: 15%;">
	<tbody>
		<tr>
			<td style="width: 3%; text-align: center;"> </td>
			<td style="width: 3%; text-align: center;">x</td>
			<td style="width: 3%; text-align: center;"> </td>
			<td style="width: 3%; text-align: center;">x</td>
			<td style="width: 3%; text-align: center;"> </td>
		</tr>
		<tr>
			<td style="width: 3%; text-align: center;">x</td>
			<td style="width: 3%; text-align: center;"> </td>
			<td style="width: 3%; text-align: center;"> </td>
			<td style="width: 3%; text-align: center;"> </td>
			<td style="width: 3%; text-align: center;">x</td>
		</tr>
		<tr>
			<td style="width: 3%; text-align: center;"> </td>
			<td style="width: 3%; text-align: center;"> </td>
			<td style="width: 3%; text-align: center;">말</td>
			<td style="width: 3%; text-align: center;"> </td>
			<td style="width: 3%; text-align: center;"> </td>
		</tr>
		<tr>
			<td style="width: 3%; text-align: center;">x</td>
			<td style="width: 3%; text-align: center;"> </td>
			<td style="width: 3%; text-align: center;"> </td>
			<td style="width: 3%; text-align: center;"> </td>
			<td style="width: 3%; text-align: center;">x</td>
		</tr>
		<tr>
			<td style="width: 3%; text-align: center;"> </td>
			<td style="width: 3%; text-align: center;">x</td>
			<td style="width: 3%; text-align: center;"> </td>
			<td style="width: 3%; text-align: center;">x</td>
			<td style="width: 3%;"> </td>
		</tr>
	</tbody>
</table>

<p>근데 원숭이는 한 가지 착각하고 있는 것이 있다. 말은 저렇게 움직일 수 있지만 원숭이는 능력이 부족해서 총 K번만 위와 같이 움직일 수 있고, 그 외에는 그냥 인접한 칸으로만 움직일 수 있다. 대각선 방향은 인접한 칸에 포함되지 않는다.</p>

<p>이제 원숭이는 머나먼 여행길을 떠난다. 격자판의 맨 왼쪽 위에서 시작해서 맨 오른쪽 아래까지 가야한다. 인접한 네 방향으로 한 번 움직이는 것, 말의 움직임으로 한 번 움직이는 것, 모두 한 번의 동작으로 친다. 격자판이 주어졌을 때, 원숭이가 최소한의 동작으로 시작지점에서 도착지점까지 갈 수 있는 방법을 알아내는 프로그램을 작성하시오.</p>

### 입력 

 <p>첫째 줄에 정수 K가 주어진다. 둘째 줄에 격자판의 가로길이 W, 세로길이 H가 주어진다. 그 다음 H줄에 걸쳐 W개의 숫자가 주어지는데, 0은 아무것도 없는 평지, 1은 장애물을 뜻한다. 장애물이 있는 곳으로는 이동할 수 없다. 시작점과 도착점은 항상 평지이다. W와 H는 1이상 200이하의 자연수이고, K는 0이상 30이하의 정수이다.</p>

### 출력 

 <p>첫째 줄에 원숭이의 동작수의 최솟값을 출력한다. 시작점에서 도착점까지 갈 수 없는 경우엔 -1을 출력한다.</p>



#  🚀  오답노트 

```diff
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.Arrays;
import java.util.LinkedList;
import java.util.Queue;
import java.util.StringTokenizer;

public class Main {
	static int K, W, H, ans;
	static int[][] map;
	static boolean[][][] visited;
	static int[] dx = { 0, 0, -1, 1, -2, -2, -1, -1, 1, 1, 2, 2 };
	static int[] dy = { -1, 1, 0, 0, -1, 1, -2, 2, -2, 2, -1, 1, };

	public static void main(String[] args) throws NumberFormatException, IOException {
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		StringTokenizer st;

		K = Integer.parseInt(br.readLine());
		st = new StringTokenizer(br.readLine());
		W = Integer.parseInt(st.nextToken());
		H = Integer.parseInt(st.nextToken());
		map = new int[H][W];
		visited = new boolean[H][W][K + 1];

		for (int i = 0; i < H; i++) {
			st = new StringTokenizer(br.readLine());
			for (int j = 0; j < W; j++) {
				map[i][j] = Integer.parseInt(st.nextToken());
			}
		}
-		if(W==1 && H==1) {
-			System.out.println(-1);
-			System.exit(0);
-		}
		ans = -1;
		bfs(0, 0, 0);
		System.out.println(ans);
	}

	static void bfs(int x, int y, int k) {
		Queue<int[]> q = new LinkedList<>();
		for (int i = 0; i < K + 1; i++) {
			visited[x][y][i] = true;
		}
		q.offer(new int[] { x, y, k });
		int cnt = 0;
		while (!q.isEmpty()) {
			int size = q.size();
			cnt++;
			for (int i = 0; i < size; i++) {
				int[] now = q.poll();
				if (now[0] == H - 1 && now[1] == W - 1) {
-					cnt--;
+					ans=0;
					return;
				}
				for (int j = 0; j < 12; j++) {
					if (j == 4 && now[2] == K)
						break;
					int nx = now[0] + dx[j];
					int ny = now[1] + dy[j];
					if (nx < 0 || ny < 0 || nx >= H || ny >= W || map[nx][ny] == 1) {
						if (cnt == 0)
							ans = -1;
						continue;
					}
					if (j < 4 && visited[nx][ny][now[2]])
						continue;
					if (j >= 4 && visited[nx][ny][now[2] + 1])
						continue;
					if (nx == H - 1 && ny == W - 1) {
						ans = cnt;
						return;
					}
					if (j < 4) {
						visited[nx][ny][now[2]] = true;
						q.offer(new int[] { nx, ny, now[2] });
					} else {
						visited[nx][ny][now[2] + 1] = true;
						q.offer(new int[] { nx, ny, now[2] + 1 });
					}
				}
			}
		}
	}
}
```


 ## 🏆 전체 코멘트 

1234