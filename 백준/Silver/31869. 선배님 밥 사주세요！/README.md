# [Silver III] 선배님 밥 사주세요! - 31869 

[문제 링크](https://www.acmicpc.net/problem/31869) 

### 분류

자료 구조, 해시를 사용한 집합과 맵, 구현

### 문제 설명

<p>24학번 신입생 정민이는 밥을 사준다는 선배들의 약속을 모두 메모장에 기록해 둔다. 메모장의 각 줄에는 선배 이름 $S$, 약속 주차 $W$, 요일 $D$, 밥 약속에 드는 비용 $P$가 기록돼 있다. 선배 이름은 문자열, 나머지는 정수로 기록한다. 또, 한 선배는 두 번 이상 밥을 사주지 않으며 모든 선배의 이름은 다르다.</p>

<p>정민이는 컴퓨터학부답게 요일을 $0$과 $6$ 사이의 정수로 기록한다. 예를 들어 월요일은 $0$이고 목요일은 $3$이다.</p>

<p>정민이의 착한 선배들은 밥을 사줄 수 있는 충분한 돈이 있다면 귀여운 후배와의 밥 약속을 무를 수 없다. 정민이의 기록과 선배들이 지닌 돈을 보고 정민이가 최대 며칠 연속으로 밥을 얻어먹을 수 있는지 구해보자!</p>

### 입력 

 <p>첫 번째 줄에는 기록의 수 $N$이 주어진다. ($0 \leq N \leq 100$)</p>

<p>두 번째 줄부터 $N$개의 줄에 걸쳐 기록의 정보가 주어진다. 기록의 정보는 $S$ $W$ $D$ $P$와 같은 형식으로 주어지며, 이는 $S$선배가 $W$주차 $D$번째 요일에 $P$원이 필요한 밥 약속을 잡았음을 뜻한다. 기록에 있는 선배의 이름은 모두 정확히 한 번씩만 주어진다. $(1 \leq W \leq 10; 0 \leq D \leq 6; 0 \leq P \leq 100\,000)$</p>

<p>그다음 줄부터 $N$개의 줄에 걸쳐 앞서 주어진 선배 이름과 선배가 소지한 돈 $M$이 공백을 사이에 두고 주어진다. 여기서 주어지는 선배 이름의 순서는 앞서 주어진 선배 이름의 순서와 다를 수 있다. $(0 \leq M \leq 100\,000)$</p>

<p>선배 이름은 $12$글자 이내의 영어 대소문자로 이뤄진 문자열로 주어진다.</p>

### 출력 

 <p>정민이가 최대 며칠 연속으로 밥을 얻어먹을 수 있는지 출력한다.</p>



#  🚀  오답노트 

```diff
import java.util.*;
import java.io.*;

public class Main {
    static StringTokenizer st;
    static int N;
    static boolean[][] arr;
    static HashMap<String, int[]> hmap = new HashMap<>(); 
    
    public static void main(String[] args) throws Exception{
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        N = Integer.parseInt(br.readLine());
-        arr = new boolean[5][7];
+        arr = new boolean[10][7];
        
        for(int i=0; i<N; i++){
            st = new StringTokenizer(br.readLine());
            String name = st.nextToken();
            int[] tmp = new int[3];
            tmp[0] = Integer.parseInt(st.nextToken());
            tmp[1] = Integer.parseInt(st.nextToken());
            tmp[2] = Integer.parseInt(st.nextToken());
            hmap.put(name, tmp);
        }
        
        for(int i=0; i<N; i++){
            st = new StringTokenizer(br.readLine());
            String target = st.nextToken();
            if(hmap.containsKey(target) && hmap.get(target)[2]>Integer.parseInt(st.nextToken())) hmap.remove(target);
        }
        
        for(int[] days : hmap.values()){
            int x = days[0]-1;
            int y = days[1];
            arr[x][y] = true;
        }
        
        int ans=0;
        int cnt=0;
-        for(int i=0; i<5; i++){
+        for(int i=0; i<10; i++){
            for(int j=0; j<7; j++){
                if(arr[i][j]) cnt++;
                else cnt=0;
                ans = Math.max(cnt, ans);
            }
        }
        System.out.print(ans);
    }
}

```


 ## 🏆 전체 코멘트 

