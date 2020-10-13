

https://space.bilibili.com/9099840


https://bytedance.feishu.cn/docs/doccnCM2qmOtndpVjbOqYoEBVog


https://www.v2ex.com/t/712932#reply0

https://cloud.tencent.com/developer/article/1032911





高可用普罗米修斯的常见问题



+ 监控是基础设施，目的是为了解决问题，不要往大而全去做
+ 需要处理的告警才发出来，发出来的告警必须得到处理
+ 简单的架构就是最好的架构，业务系统都挂了，监控也不能挂掉




452 射气球的问题

描述：射气球，给定气球的放置范围[x_start, x_end]，问至少用多少箭，可以把气球都射掉
链接：https://leetcode.com/problems/minimum-number-of-arrows-to-burst-balloons/

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
链接：https://leetcode.com/problems/remove-duplicate-letters/
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
链接：https://leetcode.com/problems/combination-sum/
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
链接：https://leetcode.com/problems/number-of-recent-calls/
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


链表的旋转


描述：对链表进行旋转，规则如下，k=2，给定链表5->3->2->NULL, k=2,  则 2-5-3->NULL
链接：https://leetcode.com/problems/rotate-list/
类别：链表
特点：成环
思路：
1. 对于链表的旋转，我们可以理解为是重新定义了链表的Head与Tail，同时需要注意，如果我们知道了旋转后链表的Tail，那么其Head为Tail->next。因此，对于该题目，第一步将链表成环、第二步对tail指针进行(len-k)次循环，得到旋转后链表的结尾，则newHead=tail->next，tail->next = NULL。
2. 另一种办法则为对链表中的所有node进行重排序。


```


# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def rotateRight(self, head: ListNode, k: int) -> ListNode:
        
        if not head:
            return None
        
        lastElement = head
        length = 1
        # get the length of the list and the last node in the list
        while ( lastElement.next ):
            lastElement = lastElement.next
            length += 1

        # If k is equal to the length of the list then k == 0
        # ElIf k is greater than the length of the list then k = k % length
        k = k % length
            
        # Set the last node to point to head node
        # The list is now a circular linked list with last node pointing to first node
        lastElement.next = head
        
        # Traverse the list to get to the node just before the ( length - k )th node.
        # Example: In 1->2->3->4->5, and k = 2
        #          we need to get to the Node(3)
        tempNode = head
        for _ in range( length - k - 1 ):
            tempNode = tempNode.next
        
        # Get the next node from the tempNode and then set the tempNode.next as None
        # Example: In 1->2->3->4->5, and k = 2
        #          tempNode = Node(3)
        #          answer = Node(3).next => Node(4)
        #          Node(3).next = None ( cut the linked list from here )
        answer = tempNode.next
        tempNode.next = None
        
        return answer


```



https://github.com/EZLippi/practical-programming-books#python



611

描述：给定数组[1,2,3,4,5,6]任意选择3个数字，可以组成多个三角形
链接：https://leetcode.com/problems/valid-triangle-number/
类别：数组
特点：双指针，核心在于减少不必要的判断
思路：
1. 朴素的想法，可以直接三层循环暴力计算，复杂度为O(N^3)
2. 进一步优化，当任意三个数字满足A[i]<A[j]<A[k]，仅判断A[i]+A[j] > A[k]即可，因此可以将原数组排序，在确定k后，在[i,j]中判断满足A[i]+A[j] > A[k]的个数。整体复杂度优化为O(N^2 + NlogN)


```

class Solution:
    def triangleNumber(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        
        c = 0
        n = len(nums)
        nums.sort()
        for i in range(n-1,1,-1):
            lo = 0
            hi = i - 1
            while lo < hi:
                if nums[hi]+nums[lo] > nums[i]:
                    c += hi-lo
                    hi -= 1
                else:
                    lo += 1
        return c
```

描述：给定数组[1,2,3,4,5,6]，统计所有子数组和为奇数的个数
链接：https://leetcode.com/problems/number-of-sub-arrays-with-odd-sum/
类别：数组
特点：前缀和的运用
思路：
1. 朴素的想法，计算所有滑动窗口下的子数组和，判断奇偶后统计结果
2. 进一步优化，任意一个子数组等于两个前缀和相减，因此可以实时统计奇/偶前缀和的个数，相加求和即可。


```

class Solution:
    def numOfSubarrays(self, arr: List[int]) -> int:
        res = odd = even = 0
        for x in arr:
            even += 1
            if x & 1:
                odd, even = even, odd
            res = (res + odd) % 1000000007             
        return res            
```


98


```

# -*- coding: utf-8 -*-

# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

# https://zh.wikipedia.org/wiki/%E4%BA%8C%E5%85%83%E6%90%9C%E5%B0%8B%E6%A8%B9
# case1. 对于叶子结点, 返回True
# case2. 对于非叶子结点, root.val > 左侧最大值, root.val < 右侧最小值
# 这里需要考虑一下:
#	1. 在第一层是不需要min, max的
#   2. 树的left_node, 永远没有min, 同样的, 树的right_node, 永远没有max
class Solution(object):
    def isValidBST(self, root):
        """
        :type root: TreeNode
        :rtype: bool
        """
        #
        return self.helper(root, None, None)
    

    def helper(self, node, min, max):
    	"""
    	:rtype: (bool, min, max)
    	"""
    	# 当前点
    	if node is None:
    		return True
    	if min is not None and node.val <= min: 
    		return False
    	if max is not None and node.val >= max:
    		return False
    	# 站在当前点, 考虑当前点对左右子树的影响.
    	# left_tree, max(left_tree) < cur_node.val
    	# right_tree, min(right_tree) > cur_node.val
    	return self.helper(node.left, min, node.val) and self.helper(node.right, node.val, max)

```


859


```

    def buddyStrings(self, A, B):
        if len(A) != len(B): 
            return False
        if A == B and len(set(A)) < len(A): 
            return True
        dif = [(a, b) for a, b in zip(A, B) if a != b]
        return len(dif) == 2 and dif[0] == dif[1][::-1]
```



1143


```

#include<iostream>
#include<vector>


using namespace std;

class Solution {
public:
    int longestCommonSubsequence(string text1, string text2) {
        vector<vector<int>> dp(text1.length(), vector<int>(text2.length()));
    

        int max_seq = 0;
        for (int i = 0; i < text1.length(); i++)
            for (int j = 0; j < text2.length(); j++) {
                int incr = text2[j] == text1[i] ? 1 : 0;
                if (i == 0 && j == 0) {
                    dp[i][j] = incr;
                    continue;
                }
                if (i == 0){
                    dp[i][j] = max(dp[i][j-1], incr);
                } else if (j == 0) {
                    dp[i][j] = max(dp[i-1][j], incr);
                } else {
                    if (incr == 0)
                        dp[i][j] = max(dp[i-1][j], dp[i][j-1]);
                    else
                        dp[i][j] = max(max(dp[i-1][j], dp[i][j-1]), dp[i-1][j-1]+1);
                }
                if (dp[i][j] > max_seq)
                    max_seq = dp[i][j];
            }
        for (int i = 0; i < text1.length(); i++) {
            for (int j = 0; j < text2.length(); j++) {
                cout << dp[i][j] << "  ";
            }

            cout << endl;
        }
        return max_seq;
    }
};

int main() {
    Solution s;
    cout << s.longestCommonSubsequence("abcde", "ace") << endl;
    cout << s.longestCommonSubsequence("abc", "abc") << endl;
    cout << s.longestCommonSubsequence("abc", "def") << endl;

    cout << s.longestCommonSubsequence("bsbininm", "jmjkbkjkv") << endl;

    cout << s.longestCommonSubsequence("xybrgc", "bgcrcbh") << endl;

    return 0;
}
```
