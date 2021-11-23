### 题目

给你一棵二叉搜索树，请 **按中序遍历** 将其重新排列为一棵递增顺序搜索树，使树中最左边的节点成为树的根节点，并且每个节点没有左子节点，只有一个右子节点。

来源：力扣（LeetCode）

链接：https://leetcode-cn.com/problems/NYBBNL/

著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。


**示例**

<img src="../pic/剑指OfferII052.展平二叉搜索树.jpg" style="zoom:50%;">

```
输入：root = [5,3,6,2,4,null,8,1,null,null,null,7,9]
输出：[1,null,2,null,3,null,4,null,5,null,6,null,7,null,8,null,9]
```

------------

### 题解

**思路**

对`root`进行中序遍历，并用`list`储存节点，然后依次修改节点的`left`指针和`right`指针


**代码**

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def increasingBST(self, root: TreeNode) -> TreeNode:
        rec = []
        def in_traver(root):
            nonlocal rec
            if not root:return
            in_traver(root.left)
            rec.append(root)
            in_traver(root.right)
            return
        in_traver(root)
        for idx in range(len(rec)):
            rec[idx].left = None
            if idx < len(rec) - 1:rec[idx].right = rec[idx+1]
            else:rec[idx].right = None
        return rec[0]
```

**复杂度分析**

时间复杂度：`O(n)`

空间复杂度：`O(n)`