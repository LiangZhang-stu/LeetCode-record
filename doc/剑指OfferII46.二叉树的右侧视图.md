### 题目

给定一个二叉树的 根节点 root，想象自己站在它的右侧，按照从顶部到底部的顺序，返回从右侧所能看到的节点值。

来源：力扣（LeetCode）

链接：https://leetcode-cn.com/problems/WNC0Lk/

著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。


**示例**

<img src="../pic/剑指OfferII46.二叉树的右侧视图.jpg" style="zoom:50%;">

```
输入: [1,2,3,null,5,null,4]
输出: [1,3,4]
```

------------
### 题解

**思路**

用队列实现对`root`进行层序遍历，在遍历每一层的时候记录当前层最右边的节点的值

**代码**

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def rightSideView(self, root: TreeNode) -> List[int]:
        if not root:return []
        queue = deque([root])
        answer = []
        while queue:
            for _ in range(len(queue)):
                cur_node = queue.popleft()
                if cur_node.left:queue.append(cur_node.left)
                if cur_node.right:queue.append(cur_node.right)
            answer.append(cur_node.val)
        return answer
```

**复杂度分析**

时间复杂度：`O(n)`

空间复杂度：`O(log(n))`

其中`n`为树的节点数量