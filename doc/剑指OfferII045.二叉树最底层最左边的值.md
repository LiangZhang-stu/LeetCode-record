### 题目

给定一个二叉树的 根节点 root，请找出该二叉树的 最底层 最左边 节点的值。

假设二叉树中至少有一个节点。

来源：力扣（LeetCode）

链接：https://leetcode-cn.com/problems/LwUNpT/

著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。


**示例**

<img src="../pic/剑指OfferII045.二叉树最底层最左边的值.jpg" style="zoom:50%;">

```
输入: [1,2,3,4,null,5,6,null,null,7]
输出: 7
```

------------
### 题解

**思路**

用队列实现对`root`进行层序遍历，在遍历每一层的时候记录当前层最左边的值

**代码**

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def findBottomLeftValue(self, root: TreeNode) -> int:
        if not root:return []
        queue = deque([root])
        while queue:
            left_val = None
            for _ in range(len(queue)):
                cur_node = queue.popleft()
                if left_val is None:left_val = cur_node.val
                if cur_node.left:queue.append(cur_node.left)
                if cur_node.right:queue.append(cur_node.right)
        return left_val
```

**复杂度分析**

时间复杂度：`O(n)`

空间复杂度：`O(log(n))`

其中`n`为树的节点数量