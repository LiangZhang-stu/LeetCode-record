### 题目
给定一个二叉树 根节点 `root` ，树的每个节点的值要么是 `0`，要么是 `1`。请剪除该二叉树中所有节点的值为 `0` 的子树。

节点 `node` 的子树为 `node` 本身，以及所有 `node` 的后代。

来源：力扣（LeetCode）

链接：https://leetcode-cn.com/problems/pOCWxh

著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。


**示例**

<img src="..\pic\剑指offer11047.二叉树减枝.png" style="zoom:50%;" />

```
输入: [1,null,0,0,1]
输出: [1,null,0,null,1] 
解释: 
只有红色节点满足条件“所有不包含 1 的子树”。
上图为返回的答案。
```

------------

### 题解

**思路**

用递归实现树的深度优先搜索，不断检查末端节点的值是否为`0`

**代码**

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def pruneTree(self, root: TreeNode) -> TreeNode:
        def check(node):
            return not node.left and not node.right \
            and node.val == 0

        def dfs(root):
            if not root:return
            if root.left:
                dfs(root.left)
                if check(root.left):root.left = None
            if root.right:
                dfs(root.right)
                if check(root.right):root.right = None
            return
        
        if check(root):return None
        else:
            dfs(root)
            if check(root):return None
            else:return root
```
**复杂度分析**

时间复杂度：`O(n)`

空间复杂度：`O(log(n))`

其中`n`为树的节点数量

