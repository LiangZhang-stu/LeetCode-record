### 题目
给定一个整数数组**asteroids**，表示在同一行的小行星。

对于数组中的每一个元素，其绝对值表示小行星的大小，正负表示小行星的移动方向（正表示向右移动，负表示向左移动）。每一颗小行星以相同的速度移动。

找出碰撞后剩下的所有小行星。碰撞规则：两个行星相互碰撞，较小的行星会爆炸。如果两颗行星大小相同，则两颗行星都会爆炸。两颗移动方向相同的行星，永远不会发生碰撞。

来源：力扣（LeetCode）

链接：https://leetcode-cn.com/problems/XagZNi

著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。



**示例**：
```
输入：asteroids = [5,10,-5]
输出：[5,10]
解释：10 和 -5 碰撞后只剩下 10 。 5 和 10 永远不会发生碰撞。
```
### 题解
**思路**
创建栈`stack`，从前往后遍历`asteroids`的元素`num`，分情况讨论：
1. 当`stack`为空或`num`为正数时，压入`num`；
2. 当`stack`不为空，且`num`为负数时：
	- 如果栈顶元素为负数，直接压入`num`；
	- 如果栈顶元素`stack[-1]`为正数，如果`stack[-1]+num`为正数

**代码**
```python
class Solution:
    def asteroidCollision(self, asteroids: List[int]) -> List[int]:
        stack = []
        for num in asteroids:
            if stack and stack[-1] < 0:stack.append(num)
            elif len(stack) == 0:stack.append(num)
            else:
                flag = True
                while stack and num < 0 and stack[-1] > 0 and flag:
                    if -num > stack[-1]:stack.pop()
                    elif -num == stack[-1]:stack.pop();flag = False
                    else:flag = False
                if flag:stack.append(num)
        return stack
```
**复杂度分析**
时间复杂度：`O(n)`
空间复杂度：`O(n)`
这里`n`是`asteroids`的长度
