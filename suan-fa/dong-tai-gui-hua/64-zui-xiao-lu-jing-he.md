# 64 最小路径和

给定一个包含非负整数的 m x n 网格，请找出一条从左上角到右下角的路径，使得路径上的数字总和为最小。

说明：每次只能向下或者向右移动一步。

```text
示例:
输入: [ [1,3,1], [1,5,1], [4,2,1] ] 
输出: 7 
解释: 因为路径 1→3→1→1→1 的总和最小。
```

```java
/**
 时间复杂度O(mn)
 空间复杂度 O(1)
*/
class Solution {
    public int minPathSum(int[][] grid) {
        int len = grid.length;
        if (len == 0) return 0;
        int height = grid[0].length;

        for (int i = 0; i < len; i++) {
            for (int j = 0; j < height; j++) {
                if (i == 0 && j == 0) {
                    continue;
                } else if (i == 0) {
                    grid[i][j] += grid[i][j - 1];
                } else if (j == 0) {
                    grid[i][j] += grid[i - 1][j];
                } else {
                    grid[i][j] += Math.min(grid[i - 1][j], grid[i][j - 1]);
                }
            }
        }
        return grid[len - 1][height - 1];
    }
}
```

