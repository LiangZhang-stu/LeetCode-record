### 题目
完全二叉树是每一层（除最后一层外）都是完全填充（即，节点数达到最大，第 `n` 层有 `2n-1` 个节点）的，并且所有的节点都尽可能地集中在左侧。

设计一个用完全二叉树初始化的数据结构 `CBTInserter`，它支持以下几种操作：

- `CBTInserter(TreeNode root)` 使用根节点为 `root` 的给定树初始化该数据结构；
- `CBTInserter.insert(int v)`  向树中插入一个新节点，节点类型为 `TreeNode`，值为 `v` 。使树保持完全二叉树的状态，并返回插入的新节点的父节点的值；
- `CBTInserter.get_root()` 将返回树的根节点。

来源：力扣（LeetCode）

链接：https://leetcode-cn.com/problems/NaqhDT

著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

**示例**

```
输入：inputs = ["CBTInserter","insert","get_root"], inputs = [[[1]],[2],[]]
输出：[null,1,[1,2]]
```

------------
### 题解

**思路**

对`root`进行层序遍历，将未完全填充的节点按层序顺序存储在队列中，当由新的`insert()`方法调用时，创建一个新的树节点给队首元素做子节点：

- 当队首元素已经由左子节点时，将新的节点赋予它作为右子节点，然后让队首元素出队；
  
- 当队首元素没有左子节点，那么将新节点赋予它作为左子节点，并继续保留它在队首；

**代码**

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class CBTInserter:

    def __init__(self, root: TreeNode):
        self.queue = deque()
        self.root = root
        tmp = deque([root])
        while tmp:
            flag = 0
            node = tmp.popleft()
            if node.left:tmp.append(node.left);flag += 1
            if node.right:tmp.append(node.right);flag += 1
            if flag < 2:self.queue.append(node)


    def insert(self, v: int) -> int:
        node = self.queue.popleft()
        if not node.left:
            node.left = TreeNode(val=v)
            self.queue.appendleft(node)
            self.queue.append(node.left)
        else:
            node.right = TreeNode(val=v)
            self.queue.append(node.right)
        return node.val


    def get_root(self) -> TreeNode:
        return self.root
```
**复杂度分析**
时间复杂度：`O(n)`
空间复杂度：`O(log(n))`
其中`n`为树的节点数量

