### 题目
写一个 `RecentCounter` 类来计算特定时间范围内最近的请求。

请实现 `RecentCounter` 类：

- `RecentCounter()` 初始化计数器，请求数为 0 。
- `int ping(int t)` 在时间 `t` 添加一个新请求，其中 `t` 表示以毫秒为单位的某个时间，并返回过去 3000 毫秒内发生的所有请求数（包括新请求）。确切地说，返回在 `[t-3000, t]` 内发生的请求数。
- 保证 每次对 `ping` 的调用都使用比之前更大的 `t` 值。

来源：力扣（LeetCode）

链接：https://leetcode-cn.com/problems/H8086Q

著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。


**示例 **

```
输入：
inputs = ["RecentCounter", "ping", "ping", "ping", "ping"]
inputs = [[], [1], [100], [3001], [3002]]
输出：
[null, 1, 2, 3, 3]

解释：
RecentCounter recentCounter = new RecentCounter();
recentCounter.ping(1);     // requests = [1]，范围是 [-2999,1]，返回 1
recentCounter.ping(100);   // requests = [1, 100]，范围是 [-2900,100]，返回 2
recentCounter.ping(3001);  // requests = [1, 100, 3001]，范围是 [1,3001]，返回 3
recentCounter.ping(3002);  // requests = [1, 100, 3001, 3002]，范围是 [2,3002]，返回 3

```

------------
### 题解
**解法**

**思路**
利用队列先进先出的特性，当新的请求时间`t`出现时，从队列的队首元素开始判断，如果小于`t-3000`，那么就需要出队，直到队首元素大于等于`t-3000`

**代码**

```python
class RecentCounter:

    def __init__(self):
        self.queue = deque()


    def ping(self, t: int) -> int:
        while self.queue:
            last_t = self.queue.popleft()
            if last_t >= t - 3000:
                self.queue.appendleft(last_t)
                break
            else:continue
        self.queue.append(t)
        return len(self.queue)


# Your RecentCounter object will be instantiated and called as such:
# obj = RecentCounter()
# param_1 = obj.ping(t)
```

**复杂度分析**

时间复杂度：`O(n)`

空间复杂度：`O(1)`

其中，`n`为`ping`方法调用次数，由于每时刻的`t`都会大于前一时刻，所以队列长度最长为`3000`。