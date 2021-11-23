### 题目

给定一个二叉树的根节点 `root` ，和一个整数 `targetSum` ，求该二叉树里节点值之和等于 `targetSum` 的 路径 的数目。

路径 不需要从根节点开始，也不需要在叶子节点结束，但是路径方向必须是向下的（只能从父节点到子节点）。

来源：力扣（LeetCode）

链接：https://leetcode-cn.com/problems/6eUYwP

著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。


**示例**

<img src="../pic/剑指OfferII050.向下的路径节点之和.jpg" style="zoom:50%;">

```
输入：root = [10,5,-3,3,2,null,11,3,-2,null,1], targetSum = 8
输出：3
解释：和等于 8 的路径有 3 条，如图所示。
```

------------

### 题解

[**思路**](https://leetcode-cn.com/problems/6eUYwP/solution/xiang-xia-de-lu-jing-jie-dian-zhi-he-by-a1iyy/)

1. 利用深度优先搜索算法，对`root`进行遍历；
2. 在遍历时用一个`hashmap`记录当前的路径和（前缀和）`cur`，并判断`hashmap`中之前是否有路径和为`cur-target`的路径，返回数量；


**代码**

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def pathSum(self, root: TreeNode, targetSum: int) -> int:
        sum_dict = defaultdict(int)
        sum_dict[0] = 1
        def dfs(root: TreeNode, cur: int) -> int:
            nonlocal targetSum, sum_dict
            rec = 0
            if not root:return rec
            cur += root.val
            rec += sum_dict[cur - targetSum]
            sum_dict[cur] += 1
            rec += dfs(root.left, cur)
            rec += dfs(root.right, cur)
            sum_dict[cur] -= 1
            return rec

        return dfs(root, 0)
```

**复杂度分析**

时间复杂度：`O(n)`

空间复杂度：`O(n)`