# 🌊 泛洪算法（Flood Fill）&& DFS BFS

------

## 📌 一、什么是泛洪算法？

泛洪算法（Flood Fill）是一种用于**区域填充**或**连通区域标记**的经典算法，类似于“油漆桶工具”从某个点开始填充一片区域。

它的核心思想是：

> **从一个起点出发，将所有与起点在某种规则下连通的点找出来，并进行处理。**

------

## 🧠 二、应用场景

- 图像处理（例如颜色填充）
- 二维迷宫中连通区域计数
- DFS/BFS 模板题
- 判断封闭区域、淹没岛屿问题
- 经典例题：Leetcode 200、417、695、733

------

## 🚀 三、实现方式对比

| 方法 | 核心思想 | 空间复杂度                     | 易错点               |
| ---- | -------- | ------------------------------ | -------------------- |
| DFS  | 递归深搜 | O(h)，h 为最大递归深度         | 注意访问标记与边界   |
| BFS  | 队列广搜 | O(w×h)，最坏情况下所有节点入队 | 队列操作、避免死循环 |

------

## 🔧 四、常规模板代码（DFS / BFS）

### ✅ DFS 实现

```cpp
const int dx[] = {0, 0, 1, -1};
const int dy[] = {1, -1, 0, 0};
bool vis[N][N];
char grid[N][N];
int n, m;

void dfs(int x, int y, char target) {
    vis[x][y] = true;
    for (int i = 0; i < 4;i++) {
        int nx = x + dx[i];
        int ny = y + dy[i];
        if (nx >= 0 && nx < n && ny >= 0 && ny < m && !vis[nx][ny] && grid[nx][ny] == target) {
            dfs(nx, ny, target);
        }
    }
}
```

### ✅ BFS 实现

```cpp
struct Point { int x, y; };
queue<Point> q;

void bfs(int sx, int sy, char target) {
    vis[sx][sy] = true;
    q.push({sx, sy});
    while (!q.empty()) {
        Point p = q.front(); q.pop();
        for (int i = 0; i < 4;i++) {
            int nx = p.x + dx[i];
            int ny = p.y + dy[i];
            if (nx >= 0 && nx < n && ny >= 0 && ny < m && !vis[nx][ny] && grid[nx][ny] == target) {
                vis[nx][ny] = true;
                q.push({nx, ny});
            }
        }
    }
}
```

## 🪄 五、小技巧与扩展

- 避免重复搜索：用 `vis[x][y]` 或直接改值标记
- 支持 8 个方向：加上对角线偏移数组 dx, dy
- 多源 BFS：初始化时将多个起点同时入队
- 模板封装：写成 `flood_fill()` 函数复用

------

## ❤️ 六、一句话总结

> **Flood Fill = 从一个点出发，蔓延扩张，直到无法继续。既可以递归也可以用队列。竞赛中常用于图像填充、连通区域判断等题。**
