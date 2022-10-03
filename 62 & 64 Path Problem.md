#### 62. Unique Paths (Medium)

There is a robot on an m x n grid. The robot is initially located at the top-left corner (i.e., grid[0][0]). The robot tries to move to the bottom-right corner (i.e., grid[m - 1][n - 1]). The robot can only move either down or right at any point in time.

Given the two integers m and n, return the number of possible unique paths that the robot can take to reach the bottom-right corner.

The test cases are generated so that the answer will be less than or equal to 2 * 109

写得略繁琐。

````
class Solution:
    def uniquePaths(self, m: int, n: int) -> int: 
            c = [[1 for x in range(m)] for y in range(n)]
            if not m or not n:
                return 0
            if not (m>=2 and n>=2):
                return 1      
            elif m>=2 and n>=2:
                for i in range(n):
                    for j in range(m):
                        fst = 0 if i<1 else c[i-1][j]
                        scd = 0 if j<1 else c[i][j-1]                          
                        c[i][j] = fst+scd 
                        c[0][0],c[1][0],c[0][1] = 1,1,1
                        # print((i,j),c[i][j])
                return c[n-1][m-1]
````

#### 64. Minimum Path Sum (Medium)

Given a m x n grid filled with non-negative numbers, find a path from top left to bottom right, which minimizes the sum of all numbers along its path.

Note: You can only move either down or right at any point in time.

````
class Solution:
    def minPathSum(self, grid: List[List[int]]) -> int:
        r,c = len(grid),len(grid[0]) 
        count = [[20000 for x in range(c)] for y in range(r)]
        if r==0 or c==0:
            return 0    
        for i in range(r):
            for j in range(c):
                if i<1 and j>=1:
                    count[i][j] = min(count[i][j], grid[i][j]+count[i][j-1])
                elif i>=1 and j<1:
                    count[i][j] = min(count[i][j], grid[i][j]+count[i-1][j])
                elif i>=1 and j>=1:
                    count[i][j] = min(count[i][j], grid[i][j]+min(count[i][j-1],count[i-1][j]))
                else:
                    count[i][j] = min(count[i][j], grid[i][j])
        return count[r-1][c-1]
````
