

https://space.bilibili.com/9099840


https://bytedance.feishu.cn/docs/doccnCM2qmOtndpVjbOqYoEBVog



高可用普罗米修斯的常见问题



+ 监控是基础设施，目的是为了解决问题，不要往大而全去做
+ 需要处理的告警才发出来，发出来的告警必须得到处理
+ 简单的架构就是最好的架构，业务系统都挂了，监控也不能挂掉




452 射气球的问题

描述：射气球，给定气球的放置范围[x_start, x_end]，问至少用多少箭，可以把气球都射掉
链接：https://leetcode.com/problems/minimum-number-of-arrows-to-burst-balloons/，ACCode
类别：数组、排序、贪心
特点：区间覆盖
思路：
注意涉及区间覆盖的问题，首先先要界定区间覆盖的范围，观察这道题目的描述我们可以发现，若给定的两个区间存在交叉与重叠，那么我们将可以用一根箭破坏多个气球。举一个栗子，给定区间[0,6]、[3,7]，由于存在overlap[3,6]，因此我们可以在覆盖区间中任意选择一点，即可同时破坏这两个气球；另一种重叠情况，给定[0,6]、[2,3]，我们同样可以在[2,3]任意选择一点，同时破坏这两个气球。基于上述的讨论，我们对给定的区间进行排序，规则如下，按照x_start升序排列，当x_start相同时，按照x_end升序排列。而后从前向后扫描一次，当满足区间交叉与重叠时，数量减1。不满足时，以当前区间作为起点，重新判定。

PS：为何贪心是有效的，可以利用反证法，当我们选定[a,b]中的b作为射击点时，存在另外一点[x, c]使得可包含更多的区间，我们分情况讨论，当[x,c]与[a,b]左相交时，x < a < c < b，若希望新增区间，则存在区间[d,e]与[x,c]相交但与[a,b]不相交，则满足 x < d < c < e 不满足 x < a < c < b，由于[d,e]与[a,b]均包含c，因此假设条件不成立。同理，当[x,c]为[a,b]子区间时，不提供新信息、当与[a,b]右相交时，也不提供新信息。

```
class Solution:
    def findMinArrowShots(self, points):
        points.sort(key = lambda x: x[1])
        n, count = len(points), 1
        if n == 0: 
            return 0
        curr = points[0]
        for i in range(n):
            if curr[1] < points[i][0]:
                count += 1
                curr = points[i]
                
        return count  

```


员工可以通过职级的提升来了解到自己的成长情况，有意识的去学习和调整自己的工作状态来获得进步。当然这个也可能会带来一定的副作用，就是有可能会让员工变成提职驱动，只挑选那些有助于个人提升职级的事情做，而不一定是对企业有利的事情。管理者可以视公司的发展阶段逐步将职级信息开放。



316

描述：给定字符串S，移除多余字符，并保证字典序
链接：https://leetcode.com/problems/remove-duplicate-letters/，ACCode
类别：字符串
特点：
思路：
1. 由于字符串中仅含有26个小写字母，因此，可以利用数组，统计每个字符的出现次数。其次，由于需要保存字典序，即当idx1 < idx2 and s[idx1] > s[idx2] and count[s[idx1]] > 1时，我们要优先采用s[idx2]因为s[idx1]可以在后面找到。因此我们需要利用到的信息有a.元素的出现次数 b. 元素是否已经被使用 c. 字典序的保持。a、b两点使用数组即可，c使用stack。


```

class Solution:
    def removeDuplicateLetters(self, s):
        last_occ = {c: i for i, c in enumerate(s)}
        stack = ["!"]
        Visited = set()
        
        for i, symbol in enumerate(s):
            if symbol in Visited: continue
            
            while (symbol < stack[-1] and last_occ[stack[-1]] > i):
                Visited.remove(stack.pop())
           
            stack.append(symbol)
            Visited.add(symbol)        
        return "".join(stack)[1:]
```



38

描述：给定数组A，数组中无重复元素，给定目标数字Target，使用A中的元素（任意次数）构造和为Target的组合数，输出所有组合。
链接：https://leetcode.com/problems/combination-sum/，ACCode
类别：动态规划，DFS
特点：背包问题、线性规划

```

class Solution:
    def combinationSum(self, candidates: List[int], target: int) -> List[List[int]]:
        res = []
        candidates.sort()
        self.backtrack(candidates, target, [], res)
        return res
    
    def backtrack(self, candidates, target, path, res):
  
        if target == 0: # check if solution can be accepted
            res.append(path)
            return
        
        for i, c in enumerate(candidates):
            if target-c < 0: break # prune the tree
            self.backtrack(candidates[i:], target-c, path+[c], res)
```


933


描述：计算给定时间窗口内，请求的数量
链接：https://leetcode.com/problems/number-of-recent-calls/，ACCode
类别：队列
特点：
思路：
1. 队列的基础题目，给定时间窗口下，统计时间窗口下事件数量，由于题目是单增调用Ping函数，因此利用队列的特性，淘汰队列中时间窗口外的事件即可。


```

class RecentCounter:

    def __init__(self):
        self.pingTimes = []

    def ping(self, t: int) -> int:
        self.pingTimes.append(t)
        i = 0
        while self.pingTimes[i] < t - 3000:
            self.pingTimes.pop(i)
        
        return len(self.pingTimes)
```


数组的旋转


描述：把一个数组最开始的若干个元素搬到数组的末尾，我们称之为数组的旋转。输入一个递增排序的数组的一个旋转，输出旋转数组的最小元素。
链接：
类别：数组，二分查找
特点：边界情况
思路：



```
class Solution:
    def rotate(self, nums, k):
        """
        :type nums: List[int]
        :type k: int
        :rtype: void Do not return anything, modify nums in-place instead.
        """
        n = len(nums)
        k %= n
        nums[:] = nums[n-k:] + nums[:n-k]
```
