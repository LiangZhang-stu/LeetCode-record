### 题目
给你一个整数数组 `nums` 和两个整数 `k` 和 `t` 。请你判断是否存在 **两个不同下标** `i` 和 `j`，使得 `abs(nums[i] - nums[j]) <= t` ，同时又满足 `abs(i - j) <= k` 。

如果存在则返回 `true`，不存在返回 `false`。

来源：力扣（LeetCode）

链接：https://leetcode-cn.com/problems/7WqeDu

著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

**示例**


```
输入：nums = [1,2,3,1], k = 3, t = 0
输出：true
```

------------

### 题解

#### [方法1](https://leetcode-cn.com/problems/7WqeDu/solution/aiera-tu-jie-hua-dong-chuang-kou-you-xu-89r1i/)

**思路**

滑动窗口+有序集合+二分查找

**代码**

```python
from sortedcontainers import SortedSet
class Solution:
    def containsNearbyAlmostDuplicate(self, nums: List[int], k: int, t: int) -> bool:
        sst = SortedSet()
        for i in range(len(nums)):
            if i > k:sst.remove(nums[i - k - 1])
            l_idx = sst.bisect_left(nums[i] - t)
            r_idx = sst.bisect_left(nums[i] + t)
            if l_idx < r_idx:return True
            elif r_idx < len(sst) and \
            sst[r_idx] == nums[i] + t:return True
            else:pass
            sst.add(nums[i])
        return False
```
**复杂度分析**

时间复杂度：`O(n*log(k))`

空间复杂度：`O(k)`


#### [方法2](https://leetcode-cn.com/problems/7WqeDu/solution/zhi-he-xia-biao-zhi-chai-du-zai-gei-ding-94ei/)

**思路**

桶排序方法（主要用到了分治的思想）

**代码**

```python
class Solution:
    def containsNearbyAlmostDuplicate(self, nums: List[int], k: int, t: int) -> bool:
        get_id = lambda x: x // (t + 1)
        bucket = defaultdict(int)
        for i in range(len(nums)):
            if i > k:bucket.pop(get_id(nums[i-k-1]))
            num_id = get_id(nums[i])
            if num_id in bucket:return True
            elif num_id - 1 in bucket and \
            abs(bucket[num_id - 1] - nums[i]) <= t:return True
            elif num_id + 1 in bucket and \
            abs(bucket[num_id + 1] - nums[i]) <= t:return True
            bucket[num_id] = nums[i]
        return False
```
**复杂度分析**

时间复杂度：`O(n)`

空间复杂度：`O(min(n, k))`