### 题目
给定一个二叉树的根节点 `root` ，树中每个节点都存放有一个 `0` 到 `9` 之间的数字。

每条从根节点到叶节点的路径都代表一个数字：

- 例如，从根节点到叶节点的路径 `1 -> 2 -> 3` 表示数字 `123` 。

计算从根节点到叶节点生成的 所有数字之和 。

叶节点 是指没有子节点的节点。

来源：力扣（LeetCode）

链接：https://leetcode-cn.com/problems/3Etpl5

著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。


**示例**

<img src='..\pic\剑指OfferII049.从根节点到叶节点的路径数字之和.jpg' style="zoom:50%;">

```
输入：root = [1,2,3]
输出：25
解释：
从根到叶子节点路径 1->2 代表数字 12
从根到叶子节点路径 1->3 代表数字 13
因此，数字总和 = 12 + 13 = 25
```

------------
### 题解

**思路**

对`root`进行深度优先遍历，不断向下进行搜索，并将此时求得的路径和放大并向下传递，直到遇到叶节点，将这个路径和进行累加；

**代码**

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def sumNumbers(self, root: TreeNode) -> int:
        if not root:return 0
        ans = 0
        def dfs(root, val):
            nonlocal ans
            if not root.left and not root.right:
                ans += val*10 + root.val
                return
            if root.left:dfs(root.left, val*10 + root.val)
            if root.right:dfs(root.right, val*10 + root.val)
        dfs(root, 0)
        return ans
```

**复杂度分析**

时间复杂度：`O(n)`

空间复杂度：`O(log(n))`

其中`n`为树的节点数量