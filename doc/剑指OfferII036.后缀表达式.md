### 题目
根据**逆波兰表示法**，求该后缀表达式的计算结果。

有效的算符包括 **+**、**-**、*****、**/** 。每个运算对象可以是整数，也可以是另一个逆波兰表达式。

说明：

- 整数除法只保留整数部分。
- 给定逆波兰表达式总是有效的。换句话说，表达式总会得出有效数值且不存在除数为 0 的情况。

来源：力扣（LeetCode）

链接：https://leetcode-cn.com/problems/8Zf90G

著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。



**示例**

```
输入：tokens = ["2","1","+","3","*"]
输出：9
解释：该算式转化为常见的中缀算术表达式为：((2 + 1) * 3) = 9
```
----
### 题解
**思路**
从前往后遍历，如果是数字就压入堆栈，如果是运算符就弹出堆栈的两个栈顶元素进行运算，当运算符为`-`,`/`时，需注意堆栈的先进后出原则。

**代码**
```python
class Solution:
    def evalRPN(self, tokens: List[str]) -> int:
        stack = []
        for tok in tokens:
            if tok not in {'+', '-', '*', '/'}:
                stack.append(int(tok))
            else:
                num1 = stack.pop()
                num2 = stack.pop()
                if tok == '+':num = num2 + num1
                elif tok == '-':num = num2 - num1
                elif tok == '*':num = num2 * num1
                elif num2 * num1 >= 0:num = num2 // num1
                else:num = -(abs(num2)//abs(num1))
                stack.append(num)
        return stack.pop()
```

**复杂度分析**
时间复杂度：`O(n)`

空间复杂度：`O(n)`

这里`n`是`token`的长度
