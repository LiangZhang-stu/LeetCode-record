### 题目
给定非负整数数组`heights`，数组中的数字用来表示柱状图中各个柱子的高度。每个柱子彼此相邻，且宽度为`1`。

求在该柱状图中，能够勾勒出来的矩形的最大面积。

来源：力扣（LeetCode）

链接：https://leetcode-cn.com/problems/binary-tree-tilt

著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

**示例 **

<img src="..\pic\histogram.jpg" style="zoom:50%;" />

```
输入：heights = [2,1,5,6,2,3]
输出：10
解释：最大的矩形为图中红色区域，面积为 10
```

------------
### 题解
**解法1**

**思路**
动态规划

**代码**

```python
class Solution:
    def largestRectangleArea(self, heights: List[int]) -> int:
        length = len(heights)
        dp = [[0]*length for _ in range(length)]
        ans = 0
        for i in range(length - 1, -1, -1):
            for j in range(i, length):
                if j == i:
                    dp[i][j] = heights[i]
                else:
                    dp[i][j] = min(dp[i+1][j] // (j - i), heights[i]) * (j - i + 1)
                ans = max(ans, dp[i][j])
        return ans
```
**复杂度分析**
时间复杂度：`O(n^2)`
空间复杂度：`O(n^2)`

**解法2**

[**思路**](https://leetcode-cn.com/problems/0ynMMM/solution/jian-zhi-offer-2-mian-shi-ti-39-shu-zhon-qzaw/)
1. 从左往右遍历，用单调栈存储`heights`的下标，保证单调栈中的引索对应的元素是单调递增的；
2. 当遇到更大的元素，把它的引索压入栈，遇到小于等于栈顶值的元素就弹出栈顶元素，并计算以它为矩阵高度的面积；
3. 计算以出栈元素为高的矩形的面积即计算以它为中心向两边出发直到遇到小于它的元素的宽度，这里结合单调栈的特性可以很轻松的找到；

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
```

**复杂度分析**

时间复杂度：`O(n)`

空间复杂度：`O(n)`