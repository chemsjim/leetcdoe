## 求出下雨后，凹陷处存储的水量
---
给出n个非负正数，代表一个海拔图，每个bar的宽度为1，计算下雨后，凹陷处可以存储的水量

### Example:
输入: [0,1,0,2,1,0,1,3,2,1,2,1]

输出: 6

海拔图如下：

![example](http://www.leetcode.com/static/images/problemset/rainwatertrap.png)

蓝色达标下雨后的储水

---
### python实现如下：
	class Solution(object):
	    def getNormalWater(self,list):
	        refer = list[0]
	        referIndex = 0
	        antiWater = 0
	        water = 0
	        for i in range(1, len(list)):
	            if list[i] >= refer:
	                if i - referIndex <= 1:
	                    pass
	                else:
	                    all = refer * (i - referIndex - 1)
	                    water = water + (all - antiWater)
	                    antiWater = 0
	                refer = list[i]
	                referIndex = i
	            else:
	                antiWater = list[i] + antiWater
	        return water
	
	    def getSplit(self, list):
	        max = list[0]
	        index = 0
	        for i in range(1, len(list)):
	            if list[i] >= max:
	                index = i
	                max = list[i]
	
	        return index
	
	    def trap(self, list):
	        """
	        :type height: List[int]
	        :rtype: int
	        """
	        if len(list) == 0:
	            return 0
	        maxIndex = self.getSplit(list)
	        water = self.getNormalWater(list[0:maxIndex + 1]) + self.getNormalWater(list[-1:maxIndex - len(list) - 1:-1])
	        return water
	
	if __name__ == '__main__':
	    list = [1]
	    solution = Solution()
	    print solution.trap(list)

---

### 简单思路

这道题不知道考点是什么，考归纳能力么，新推出的题目评价系统，这道题居然罕见的，点赞的人远远超过了踩的人。是因为这道题很巧妙，还是因为考点很巧妙。我的实现方法，使用最简单粗暴的方法， 时间复杂度为O(N)，代码运行时间超过90%的人......

1、无论怎样的海拔图，最终总能转化为两个最传统的、坡度向上的海拔图,因为这种方式最好容水量。

![all](http://note.youdao.com/yws/public/resource/43867fd5c9b1fadcb1cf03c8dab67ca3/xmlnote/37CEFFCB3DE645C3BBED01A4ACCED699/29978)

有色处为等高线，白色处为可存水处。上图可以转化为如下两个坡度向上的海拔图

![splist](http://note.youdao.com/yws/public/resource/43867fd5c9b1fadcb1cf03c8dab67ca3/xmlnote/2CF88288F9AB4439AC11AAA766E498D9/29982)

2、思考中发现，左边的这种形式等高图的储水量最好计算，遍历左边等高图，以最开始的等高线A作为pivot，遍历至直到发现比pivot高的等高线B，那么两条线构成凹陷，此时将中间较低等高线占用的空间减掉，即min(A,B)*(index(B)-index(A)),即为最终储水量

3、因为第二种凹陷，直接计算储水量很麻烦，所以我开始对整体list进行遍历的时候，直接将第二个凹陷进行了reverse，使其转换成与左边的凹陷类似的，坡度由向下转化为向上

4、将两个凹陷的储水量进行累加



