### 题目
给定一个由`0`和`1`组成的矩阵`matrix`，找出只包含`1`的最大矩形，并返回其面积。

注意：此题`matrix`输入格式为一维`01`字符串数组。

来源：力扣（LeetCode）

链接：https://leetcode-cn.com/problems/PLYXKQ/

著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

**示例**

<img src="..\pic\maximal.jpg" style="zoom:50%;" />

```
输入：matrix = ["10100","10111","11111","10010"]
输出：6
解释：最大矩形如上图所示。
```

------------
### 题解
**解法**

[**思路**](https://leetcode-cn.com/problems/PLYXKQ/solution/jian-zhi-offer-ii-040-ju-zhen-zhong-zui-v3wg2/)

结合[剑指 OfferII 039. 直方图最大矩形面积](剑指OfferII039.直方图最大矩形面积.md)的思路，将`matrix`中的每一行当作一个直方图，

并且，下一行直方图的高度需要结合上一行直方图的高度来考虑

**代码**

```python
class Solution:
    def largestRectangleArea(self, heights: List[int]) -> int:
        stack = [-1]
        ans = 0
        for idx in range(len(heights)):
            while stack[-1] != -1 and heights[idx] <= heights[stack[-1]]:
                h = heights[stack.pop()]
                ans = max(ans, h * (idx - stack[-1] - 1))
            stack.append(idx)
        last_idx = stack[-1] + 1
        while stack[-1] != -1:
            h = heights[stack.pop()]
            ans = max(ans, h * (last_idx - stack[-1] - 1))
        return ans

    def maximalRectangle(self, matrix: List[str]) -> int:
        if not matrix:return 0
        height = [0]*len(matrix[0])
        ans = 0
        for i in range(len(matrix)):
            for j in range(len(matrix[i])):
                if matrix[i][j] == '0':height[j] = 0
                else:height[j] += 1
            ans = max(ans, self.largestRectangleArea(height))
        return ans
```

**复杂度分析**

时间复杂度：`O(n^2)`

空间复杂度：`O(n)`