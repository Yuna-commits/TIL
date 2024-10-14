# Dijkstra Algorithm

> N x N 공간에서 각 칸마다 잃는 돈이 있을 때, 출구에 갈 때까지 잃을 수밖에 없는 최소 금액

> [문제](https://www.acmicpc.net/problem/4485)

### 가장 처음 생각한것 -> bfs
- 젤다가 잃을 수밖에 없는 금액==최단 거리로 이동했을 때의 금액으로 생각했기 때문에 바로 bfs를 떠올렸다.

```
void bfs() {
        queue<pair<int, int>> que;
        /*동굴입구*/
        que.push({ 0,0 });
        dist[0][0] = cave[0][0];
        while (!que.empty()) {
                int now_x = que.front().first;
                int now_y = que.front().second;
                que.pop();
                for (int i = 0; i < 4; i++) {
                        int next_x = now_x + dx[i];
                        int next_y = now_y + dy[i];
                        if (next_x >= 0 && next_x < N && next_y >= 0 && next_y < N) {
                                if (dist[next_x][next_y] > dist[now_x][now_y] + cave[next_x][next_y]) {
                                        dist[next_x][next_y]= dist[now_x][now_y] + cave[next_x][next_y];
                                        que.push({ next_x, next_y });
                                }
                        }
                }
        }
}
```