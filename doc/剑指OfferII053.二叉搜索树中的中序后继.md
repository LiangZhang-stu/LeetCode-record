### 题目
给定一棵二叉搜索树和其中的一个节点 `p` ，找到该节点在树中的中序后继。如果节点没有中序后继，请返回 `null` 。

节点 `p` 的后继是值比 `p.val` 大的节点中键值最小的节点，即按中序遍历的顺序节点 `p` 的下一个节点。


来源：力扣（LeetCode）

链接：https://leetcode-cn.com/problems/P5rCT8

著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。


**示例**

<img src="..\pic\剑指OfferII053.二叉搜索树中的中序后继.png" style="zoom:50%;" />

```
输入：root = [5,3,6,2,4,null,null,1], p = 6
输出：null
解释：因为给出的节点没有中序后继，所以答案就返回 null 了。
```

------------

### 题解

**思路**

结合**二叉搜索树**的特性，即*左子树的所有节点值 < 根节点值 < 右子树所有节点值*，

采用二分查找的思想来搜索刚好大于`p.val`的节点，即为`p`的后继节点

**代码**

```cpp
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
class Solution {
public:
    TreeNode* inorderSuccessor(TreeNode* root, TreeNode* p) {
        TreeNode* cur = root;
        TreeNode* result = nullptr;
        while (cur != nullptr){
            if (cur -> val > p -> val){
                result = cur;
                cur = cur -> left;
            }else{
                cur = cur -> right;
            }
        }
        return result;
    }
};
```
**复杂度分析**

时间复杂度：`O(log(n))`

空间复杂度：`O(1)`

其中`n`为树的节点数量

