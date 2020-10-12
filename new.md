

https://space.bilibili.com/9099840


https://bytedance.feishu.cn/docs/doccnCM2qmOtndpVjbOqYoEBVog



高可用普罗米修斯的常见问题



监控是基础设施，目的是为了解决问题，不要往大而全去做
需要处理的告警才发出来，发出来的告警必须得到处理
简单的架构就是最好的架构，业务系统都挂了，监控也不能挂掉




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
