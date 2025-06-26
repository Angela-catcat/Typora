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
