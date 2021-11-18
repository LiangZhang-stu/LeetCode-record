### 题目
请根据每日**气温**列表**temperatures**，重新生成一个列表，要求其对应位置的输出为：要想观测到更高的气温，至少需要等待的天数。如果气温在这之后都不会升高，请在该位置用`0`来代替。

来源：力扣（LeetCode）

链接：https://leetcode-cn.com/problems/8Zf90G

著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

**示例**
```
输入: temperatures = [73,74,75,71,69,72,76,73]
输出: [1,1,4,2,1,1,0,0]
```
------------
### 题解
**思路**
从后往前遍历`temperatures`，利用单调栈存储元素的下标

**代码**
```python
class Solution:
    def dailyTemperatures(self, temperatures: List[int]) -> List[int]:
        stack = []
        ans = []
        temp = lambda x:temperatures[x]
        for idx in range(len(temperatures)-1, -1, -1):
            while stack and temp(idx) >= temp(stack[-1]):
                stack.pop()
            if not stack:
                ans.append(0)
                stack.append(idx)
            else:
                ans.append(stack[-1]-idx)
                stack.append(idx)
        return ans[::-1]
```
**复杂度分析**
时间复杂度：`O(n)`
空间复杂度：`O(n)`
其中`n`为`temperatures`的长度
