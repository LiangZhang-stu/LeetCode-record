### 题目

路径 被定义为一条从树中任意节点出发，沿父节点-子节点连接，达到任意节点的序列。同一个节点在一条路径序列中 **至多出现一次** 。该路径 **至少包含一个** 节点，且不一定经过根节点。

**路径和** 是路径中各节点值的总和。

给定一个二叉树的根节点 `root` ，返回其 **最大路径和**，即所有路径上节点值之和的最大值。

来源：力扣（LeetCode）

链接：https://leetcode-cn.com/problems/jC7MId

著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。


**示例**

<img src="../pic/剑指OfferII051.节点之和最大的路径.jpg" style="zoom:50%;">

```
输入：root = [-10,9,20,null,null,15,7]
输出：42
解释：最优路径是 15 -> 20 -> 7 ，路径和为 15 + 20 + 7 = 42
```

------------

### 题解

**思路**

1. 利用深度优先搜索算法，对`root`进行遍历；
2. 在遍历时，比较左子树的最大路径和（路径一定要包含左子节点）和右子树的最大路径和（路径一定要包含右子节点），
   然后选择大于0的最大的路径和父节点求和，否则只返回父节点的值作为当前的最大路径和；
3. 同时记录当前由左子树最大路径和、父节点值以及右子树最大路径和的和是否最大；


**代码**

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def maxPathSum(self, root: TreeNode) -> int:
        ans = -float(inf)
        def dfs(root: TreeNode) -> int:
            nonlocal ans
            if not root.left and not root.right:
                ans = max(ans, root.val)
                return root.val
            if root.left:l_tmp = dfs(root.left)
            else:l_tmp = -float('inf')
            if root.right:r_tmp = dfs(root.right)
            else:r_tmp = -float('inf')
            rec = max(0, max(l_tmp, r_tmp)) + root.val
            ans = max(ans, rec)
            ans = max(ans, l_tmp + root.val + r_tmp)
            return rec
        dfs(root)
        return ans
```

**复杂度分析**

时间复杂度：`O(n)`

空间复杂度：`O(n)`