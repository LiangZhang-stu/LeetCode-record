### 题目
给定一个二叉搜索树，请将它的每个节点的值替换成树中大于或者等于该节点值的所有节点值之和。

提醒一下，二叉搜索树满足下列约束条件：

- 节点的左子树仅包含键 小于 节点键的节点。
- 节点的右子树仅包含键 大于 节点键的节点。
- 左右子树也必须是二叉搜索树。

来源：力扣（LeetCode）

链接：https://leetcode-cn.com/problems/w6cpku

著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。


**示例**

<img src="..\pic\剑指OfferII054.所有大于等于节点的值之和.png" style="zoom:50%;" />

```
输入：root = [4,1,6,0,2,5,7,null,null,null,3,null,null,null,8]
输出：[30,36,21,36,35,26,15,null,null,null,33,null,null,null,8]
```

------------

### 题解

**思路**

结合**二叉搜索树**的特性，采用`dfs`对它进行后序遍历，并记录后缀和

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
class Solution {
int accu = 0;
public:
    TreeNode* convertBST(TreeNode* root) {
        dfs(root);
        return root;
    }
private:
    void dfs(TreeNode* root){
        if (root == nullptr) return;
        dfs(root -> right);
        accu = accu + root -> val;
        root -> val = accu;
        dfs(root -> left);
        return;
    }
};
```
**复杂度分析**

时间复杂度：`O(n)`

空间复杂度：`O(log(n))`

其中`n`为树的节点数量

