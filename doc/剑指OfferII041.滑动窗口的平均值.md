### 题目
给定一个整数数据流和一个窗口大小，根据该滑动窗口的大小，计算滑动窗口里所有数字的平均值。

实现`MovingAverage`类：

- `MovingAverage(int size)`用窗口大小`size`初始化对象。
- `double next(int val)`成员函数`next`每次调用的时候都会往滑动窗口增加一个整数，请计算并返回数据流中最后`size`个值的移动平均值，即滑动窗口里所有数字的平均值。

来源：力扣（LeetCode）

链接：https://leetcode-cn.com/problems/qIsx9U

著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。


**示例**

```
输入：
inputs = ["MovingAverage", "next", "next", "next", "next"]
inputs = [[3], [1], [10], [3], [5]]
输出：
[null, 1.0, 5.5, 4.66667, 6.0]

解释：
MovingAverage movingAverage = new MovingAverage(3);
movingAverage.next(1); // 返回 1.0 = 1 / 1
movingAverage.next(10); // 返回 5.5 = (1 + 10) / 2
movingAverage.next(3); // 返回 4.66667 = (1 + 10 + 3) / 3
movingAverage.next(5); // 返回 6.0 = (10 + 3 + 5) / 3

```

------------
### 题解
**解法**

**思路**
1. 利用广度优先搜索算法，对`n`进行操作，直到操作`n`变为1时，返回操作的次数；

2. 这里可以结合状态压缩来节省搜索时间，即用一个`hashset`存储已经出现过的值，避免重复搜索

**代码**

```python
class MovingAverage:

    def __init__(self, size: int):
        """
        Initialize your data structure here.
        """
        self.size = size
        self.accu = 0
        self.queue = deque()


    def next(self, val: int) -> float:
        if len(self.queue) < self.size:
            self.queue.append(val)
            self.accu += val
        else:
            self.accu -= self.queue.popleft() - val
            self.queue.append(val)
        return self.accu / len(self.queue)
```

**复杂度分析**

时间复杂度：`O(n)`

空间复杂度：`O(m)`

其中，`n`为`next`方法调用次数，`m`为`size`的大小