### 题目
序列化是将一个数据结构或者对象转换为连续的比特位的操作，进而可以将转换后的数据存储在一个文件或者内存中，同时也可以通过网络传输到另一个计算机环境，采取相反方式重构得到原数据。

请设计一个算法来实现二叉树的序列化与反序列化。这里不限定你的序列 / 反序列化算法执行逻辑，只需要保证一个二叉树可以被序列化为一个字符串并且将这个字符串反序列化为原始的树结构。

来源：力扣（LeetCode）

链接：https://leetcode-cn.com/problems/h54YBf

著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。


**示例**

<img src='..\pic\剑指OfferII048.序列化与反序列化二叉树.jpg' style="zoom:50%;">

```
输入：root = [1,2,3,null,null,4,5]
输出：[1,2,3,null,null,4,5]
```

------------
### 题解

**思路**

- `serialize()`：利用`dfs`算法对`root`进行先序遍历，并把`None`也做为叶节点记录，以`1001`作为标记；
- `deserialize()`：利用`dfs`算法在先序序列上构造二叉树，当左右节点都为`None`时，才返回；

**代码**

```python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Codec:

    def serialize(self, root):

        """Encodes a tree to a single string.
        
        :type root: TreeNode
        :rtype: str
        """
        order = []
        def _preorder(root):
            nonlocal order
            if not root:order.append('1001')
            else:
                order.append(str(root.val))
                _preorder(root.left)
                _preorder(root.right)
                return
        
        _preorder(root)
        return ','.join(order)
        

    def deserialize(self, data):
        """Decodes your encoded data to tree.
        :type data: str
        :rtype: TreeNode
        """
        order = list(map(int, data.split(',')))
        idx = 0
        def get_tree():
            nonlocal idx
            if idx >= len(order):return None
            elif order[idx] > 1000:
                idx += 1
                return None
            else:
                root = TreeNode(order[idx])
                idx += 1
                root.left = get_tree()
                root.right = get_tree()
                return root
        return get_tree()
```

**复杂度分析**

- `serialize()`和`deserialize()`方法的时间复杂度：

时间复杂度：`O(n)`

空间复杂度：`O(n)`

其中`n`为树的节点数量