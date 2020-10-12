

https://space.bilibili.com/9099840


https://bytedance.feishu.cn/docs/doccnCM2qmOtndpVjbOqYoEBVog



高可用普罗米修斯的常见问题



+ 监控是基础设施，目的是为了解决问题，不要往大而全去做
+ 需要处理的告警才发出来，发出来的告警必须得到处理
+ 简单的架构就是最好的架构，业务系统都挂了，监控也不能挂掉




452 射气球的问题

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
