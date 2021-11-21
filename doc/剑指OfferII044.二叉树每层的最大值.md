### 题目
给定一棵二叉树的根节点 `root` ，请找出该二叉树中每一层的最大值。

来源：力扣（LeetCode）

链接：https://leetcode-cn.com/problems/hPov7L/

著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。


**示例**


```
输入: root = [1,3,2,5,3,null,9]
输出: [1,3,9]
解释:
          1
         / \
        3   2
       / \   \  
      5   3   9 
```

------------
### 题解

**思路**

用队列实现对`root`进行层序遍历，在遍历每一层的时候记录当前层的最大值

**代码**

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def largestValues(self, root: TreeNode) -> List[int]:
        if not root:return []
        queue = deque([root])
        answer = []
        while queue:
            max_num = -float('inf')
            for _ in range(len(queue)):
                cur_node = queue.popleft()
                max_num = max(max_num, cur_node.val)
                if cur_node.left:queue.append(cur_node.left)
                if cur_node.right:queue.append(cur_node.right)
            answer.append(max_num)
        return answer
```

**复杂度分析**

时间复杂度：`O(n)`

空间复杂度：`O(log(n))`

其中`n`为树的节点数量