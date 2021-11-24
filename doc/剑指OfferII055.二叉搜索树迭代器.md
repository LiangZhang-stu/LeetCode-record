### 题目
实现一个二叉搜索树迭代器类`BSTIterator` ，表示一个按中序遍历二叉搜索树`（BST）`的迭代器：

`BSTIterator(TreeNode root)` 初始化 `BSTIterator` 类的一个对象。`BST` 的根节点 `root` 会作为构造函数的一部分给出。指针应初始化为一个不存在于 BST 中的数字，且该数字小于 `BST` 中的任何元素。
`boolean hasNext()` 如果向指针右侧遍历存在数字，则返回 `true` ；否则返回 `false` 。
`int next()`将指针向右移动，然后返回指针处的数字。
注意，指针初始化为一个不存在于 `BST` 中的数字，所以对 `next()` 的首次调用将返回 `BST` 中的最小元素。

可以假设 `next()` 调用总是有效的，也就是说，当调用 `next()` 时，`BST` 的中序遍历中至少存在一个下一个数字。

来源：力扣（LeetCode）

链接：https://leetcode-cn.com/problems/kTOapQ

著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。


**示例**

<img src="..\pic\剑指OfferII055.二叉搜索树迭代器.png" style="zoom:50%;" />

```
输入
inputs = ["BSTIterator", "next", "next", "hasNext", "next", "hasNext", "next", "hasNext", "next", "hasNext"]
inputs = [[[7, 3, 15, null, null, 9, 20]], [], [], [], [], [], [], [], [], []]
输出
[null, 3, 7, true, 9, true, 15, true, 20, false]

解释
BSTIterator bSTIterator = new BSTIterator([7, 3, 15, null, null, 9, 20]);
bSTIterator.next();    // 返回 3
bSTIterator.next();    // 返回 7
bSTIterator.hasNext(); // 返回 True
bSTIterator.next();    // 返回 9
bSTIterator.hasNext(); // 返回 True
bSTIterator.next();    // 返回 15
bSTIterator.hasNext(); // 返回 True
bSTIterator.next();    // 返回 20
bSTIterator.hasNext(); // 返回 False

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/kTOapQ
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。
```

------------

### 题解

**思路**

结合**二叉搜索树**的特性，采用`dfs`对它进行中序遍历，用`list`存储节点的`val`

**代码**

```cpp
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
class BSTIterator {
vector<int> rec;
int idx = 0;
public:
    BSTIterator(TreeNode* root) {
        dfs(root);
    }
    
    int next() {
        idx++;
        return rec[idx-1];
    }
    
    bool hasNext() {
        return idx < rec.size();
    }

private:
    void dfs(TreeNode* root) {
        if (root == nullptr) return;
        dfs(root -> left);
        rec.push_back(root -> val);
        dfs(root -> right);
        return;
    }
};

/**
 * Your BSTIterator object will be instantiated and called as such:
 * BSTIterator* obj = new BSTIterator(root);
 * int param_1 = obj->next();
 * bool param_2 = obj->hasNext();
 */
```
**复杂度分析**

时间复杂度：`O(n)`

空间复杂度：`O(log(n))`

其中`n`为树的节点数量

