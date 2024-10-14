# Dijkstra Algorithm

> N x N 공간에서 각 칸마다 잃는 돈이 있을 때, 출구에 갈 때까지 잃을 수밖에 없는 최소 금액

> [문제](https://www.acmicpc.net/problem/4485)

## 가장 처음 생각한것 -> BFS
- 젤다가 잃을 수밖에 없는 금액==최단 거리로 이동했을 때의 금액으로 생각했기 때문에 바로 BFS를 떠올렸다.
- 상하좌우로 4방향을 탐색하는데, (현재 위치의 루피(가중치)+다음 위치의 루피)와 (다음 위치의 루피) 비교해서 더 작은 값을 dist[next]에 저장한다. 최종적으로 dist[N-1][N-1]에 출구까지의 최단 거리, 즉 최소로 소모된 루피가 저장된다.
- 기본 BFS는 (지금까지 저장된 경로 + 1)을 하며 최단 거리를 갱신하는데 이것을 가중치를 더하는 것으로 대신해서 풀었다.
- 알고리즘 분류를 보니 다익스트라 알고리즘을 사용한다 적혀있어서 둘의 차이점이 무엇인지 궁금했다.

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

## 💡BFS vs DIJKSTRA
### BFS
- BFS는 가중치가 없는 그래프에서 한 정점에서 나머지 정점으로의 최단 경로를 찾는다.
### DIJKSTRA
- 다익스트라는 그래프의 각 간선의 가중치가 다르고 음수 간선이 없을 때 사용한다.
- 아래의 그래프에서 0번 정점에서 2번 정점으로 가는 최단 경로는 0->1->3->2이다.
  <p align="left"><img src="https://velog.velcdn.com/images%2Fkasterra%2Fpost%2Fd8c6f97d-f000-496b-98c5-fa21f1658572%2Fimage.png">
        
    - 하지만 BFS의 방문순서는 0 -> (1, 2번 정점 방문) -> 3이기 때문에 최단 경로를 BFS로는 찾을 수 없다.
    - BFS와 다익스트라 둘 다 그래프에서 쓸 수 있는 탐색 알고리즘이지만, BFS로 해결할 수 없는 문제가 있을 때 다익스트라 알고리즘을 사용할 수 있다.
    - 하지만 다익스트라 알고리즘도 간선의 가중치에 음수가 있을 경우 올바르게 동작하지 않기 때문에 주의해야 한다.
    - 더 자세한 내용은 나중에 작성


## 다익스트라로 다시 푼 것
- 다익스트라는 BFS와 달리 우선순위 큐(Priority Queue)를 사용한다.
- 최대 힙 상태일 때, 가중치를 음수로 만들어서 가장 작은 값에 우선순위를 두도록 만든 것이 신기했다.
- C++의 pair 클래스 사용이 아직도 어색하다. 처음에 만들었던 BFS 구조에서 어떻게 다익스트라로 바꿀지 잘 안떠올랐다.

```
void dijkstra() {
        priority_queue<pair<int, pair<int, int>>> que;
        que.push({ -1 * cave[0][0], {0,0} });
        dist[0][0] = cave[0][0];
        while (!que.empty()) {
                int now_x = que.top().second.first;
                int now_y = que.top().second.second;
                que.pop();
                for (int i = 0; i < 4; i++) {
                        int next_x = now_x + dx[i];
                        int next_y = now_y + dy[i];
                        int next_cost = cave[next_x][next_y];
                        if (next_x >= 0 && next_x < N && next_y >= 0 && next_y < N) {
                                int before = dist[next_x][next_y];
                                int after = next_cost + dist[now_x][now_y];
                                if (before > after) {
                                        dist[next_x][next_y] = after;
                                        que.push({ -1 * after, {next_x, next_y} });
                                }
                        }
                }
        }
}

```
    
