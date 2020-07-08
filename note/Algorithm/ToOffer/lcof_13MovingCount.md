>[剑指 Offer 13. 机器人的运动范围](https://leetcode-cn.com/problems/ji-qi-ren-de-yun-dong-fan-wei-lcof/)
>
>地上有一个m行n列的方格，从坐标 [0,0] 到坐标 [m-1,n-1] 。一个机器人从坐标 [0, 0] 的格子开始移动，它每次可以向左、右、上、下移动一格（不能移动到方格外），也不能进入行坐标和列坐标的数位之和大于k的格子。例如，当k为18时，机器人能够进入方格 [35, 37] ，因为3+5+3+7=18。但它不能进入方格 [35, 38]，因为3+5+3+8=19。请问该机器人能够到达多少个格子？
>
>**示例1**
```
输入：
  m = 2, n = 3, k = 1
输出：
  3
```
>**示例2**
```
输入：
  m = 3, n = 1, k = 0
输出：
  1
```

```java
// Java版 - BFS
class Solution {
    public int movingCount(int m, int n, int k) {
        if(m <= 0 || n <= 0){
            return 0;
        }
        Deque<Integer> queue = new LinkedList<>();
        int res = 0;
        int[][] dir = new int[][]{{1,0},{0,1}};
        boolean[][] visited = new boolean[m][n];
        queue.offerLast(0);
        res = 1;
        visited[0][0] = true;
        while(queue.size() > 0){
            int id = queue.pollFirst();
            // 注意这里对于坐标的映射
            int x = id/n;
            int y = id%n;
            for(int i = 0; i < dir.length; i++){
                int xi = x + dir[i][0];
                int yi = y + dir[i][1];
                int sum = get(xi) + get(yi);
                if(xi < 0 || xi >= m || yi < 0 || yi >= n || visited[xi][yi] || sum > k) {
                    continue;
                }
                visited[xi][yi] = true;
                res++;
                queue.offerLast(xi*n + yi);
            }
        }
        return res;
    }

    int get(int x){
        int res = 0;
        while(x != 0) {
            res += x%10;
            x /= 10;
        }
        return res;
    }
}
```
```java
// Java版 - DFS
class Solution {
    public int movingCount(int m, int n, int k) {
        if(m <= 0 || n <= 0) {
            return -1;
        }
        boolean[][] visited = new boolean[m][n];
        return dfs(0, 0, visited, m, n, k);
    }
    
    int dfs(int a, int b, boolean[][] visited, int m, int n, int k){
        int sum = get(a) + get(b);
        if(a < 0 || a >= m || b < 0 || b >= n || visited[a][b] || sum > k) {
            return 0;
        }
        visited[a][b] = true;
        return 1 + dfs(a+1,b,visited,m,n,k) + dfs(a,b+1,visited,m,n,k);
    }


    int get(int x){
        int res = 0;
        while(x != 0){
            res += x%10;
            x /= 10;
        }
        return res;
    }
}
```