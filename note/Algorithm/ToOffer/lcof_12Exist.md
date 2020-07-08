>[剑指 Offer 12. 矩阵中的路径](https://leetcode-cn.com/problems/ju-zhen-zhong-de-lu-jing-lcof/)
>
>请设计一个函数，用来判断在一个矩阵中是否存在一条包含某字符串所有字符的路径。路径可以从矩阵中的任意一格开始，每一步可以在矩阵中向左、右、上、下移动一格。如果一条路径经过了矩阵的某一格，那么该路径不能再次进入该格子。例如，在下面的3×4的矩阵中包含一条字符串“bfce”的路径（路径中的字母用加粗标出）。
```
 [["a","b","c","e"],
  ["s","f","c","s"],
  ["a","d","e","e"]]
```
>但矩阵中不包含字符串“abfb”的路径，因为字符串的第一个字符b占据了矩阵中的第一行第二个格子之后，路径不能再次进入这个格子。
>
>**示例1**
```
输入：
  board = [["A","B","C","E"],["S","F","C","S"],["A","D","E","E"]], word = "ABCCED"
输出：
  true
```
>**示例2**
```
输入：
  board = [["a","b"],["c","d"]], word = "abcd"
输出：
  false
```

```java
// Java版
class Solution {

    boolean[][] mark;

    public boolean exist(char[][] board, String word) {
        if(board.length <= 0 || board[0].length <= 0){
            return false;
        }
        int m = board.length;
        int n = board[0].length;
        mark = new boolean[m][n];
        for(int i = 0; i < m; i++){
            for(int j = 0; j < n; j++){
                if (existDfs(board, 0, i, j, word)) {
                    return true;
                }
            }
        }
        return false;
    }

    public boolean existDfs(char[][] board, int start, int a, int b, String word){
        if(start == word.length()-1){
            return board[a][b] == word.charAt(start);
        }
        if(word.charAt(start) == board[a][b]){
            // 回溯
            mark[a][b] = true;
            int[][] dir = {{0,1},{0,-1},{1,0},{-1,0}};
            for(int i=0; i<dir.length; i++){
                int x = a+dir[i][0];
                int y = b+dir[i][1];
                if(x >= 0 && x < board.length && y >= 0 && y < board[0].length && !mark[x][y]){
                    if(existDfs(board, start+1, x, y, word)){
                        return true;
                    }
                }
            }
            // 回溯
            mark[a][b] = false;
        }
        return false;
    }
}
```