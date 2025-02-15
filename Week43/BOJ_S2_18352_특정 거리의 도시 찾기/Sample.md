#   [2023.10.10] BOJ_S2_18352_특정 거리의 도시 찾기
https://www.acmicpc.net/problem/18352

<접근법>

```
1. bfs 이용해 각 도시마다 들러 K거리인 도시 리스트에 저장
```




```java
/**
 * 메모리  : 387044 KB
 * 시간   : 3460 ms
 */
import java.util.*;

public class BJ_18352 {
    public static void main(String[] args) {
        try (Scanner sc = new Scanner(System.in)) {
            String[] inps = sc.nextLine().split(" ");
            int N = Integer.parseInt(inps[0]);
            int M = Integer.parseInt(inps[1]);
            int K = Integer.parseInt(inps[2]);
            int X = Integer.parseInt(inps[3]);

            List<Integer>[] edges = new ArrayList[N + 1];
            for (int i = 0; i <= N; i++) {
                edges[i] = new ArrayList<>();
            }

            for (int i = 0; i < M; i++) {
                inps = sc.nextLine().split(" ");
                edges[Integer.parseInt(inps[0])].add(Integer.parseInt(inps[1]));
            }

            Queue<Node> que = new ArrayDeque<>();
            que.add(new Node(X, 0));
            Set<Integer> isVisited = new HashSet<>();
            isVisited.add(X);
            
            List<Integer> list = new ArrayList<>();
            // bfs 수행
            while (!que.isEmpty()) {
                Node cn = que.poll();

                if (cn.depth > K) {
                    break;
                }
                if (cn.depth == K) {
                    list.add(cn.num);
                }

                for (int next : edges[cn.num]) {
                    if (!isVisited.contains(next)) {
                        isVisited.add(next);
                        que.add(new Node(next, cn.depth + 1));
                    }
                }
            }

            Collections.sort(list);

            if (list.isEmpty()) {
                System.out.println(-1);
            } else {
                StringBuilder answer = new StringBuilder();
                for (int n : list) {
                    answer.append(n).append('\n');
                }
                System.out.print(answer);
            }
        }
    }

    static class Node {
        int depth;
        int num;

        Node(int num, int depth) {
            this.num = num;
            this.depth = depth;
        }
    }
}
```