## 求出数组中所有和为0的3-tuple
---
给出一个整数数组S，取出数组中的3个元素a,b,c，使得 a+b+c=0，找出所有的满足这个条件的3-tuple

**NOTE:结果中不应改包含重复tuple**

### Example:
输入: S = [-1, 0, 1, 2, -1, -4]

输出:
 
[
  [-1, 0, 1],
  [-1, -1, 2]
]


	class Solution(object):
	    def threeSum(self, nums):
	        res = []
	        nums.sort()
	        for i in xrange(len(nums) - 2):
	            if i > 0 and nums[i] == nums[i - 1]:
	                continue
	            l, r = i + 1, len(nums) - 1
	            while l < r:
	                s = nums[i] + nums[l] + nums[r]
	                if s < 0:
	                    l += 1
	                elif s > 0:
	                    r -= 1
	                else:
	                    res.append((nums[i], nums[l], nums[r]))
	                    while l < r and nums[l] == nums[l + 1]:
	                        l += 1
	                    while l < r and nums[r] == nums[r - 1]:
	                        r -= 1
	                    l += 1;
	                    r -= 1
	        return res

	if __name__ == '__main__':
    	solution = Solution()
  	  	S = [-1, 0, 1, 2, -1, -4]
    	print solution.threeSum(S);

---
### 简单思路

1、最暴力的方式，通过穷举方式求出所有的情况，时间复杂度为O(n^3)

2、更好的解决方式，通过对输入数组S进行升序排序，得到时间复杂度为O(n^2）的solution。对数据进行遍历，以数组第一个元素为例：将当前元素作S[0]为3-tuple的第一个元素，第二个元素取数组剩余元素的最小值S[1]，第三个元素取最大值S[n-1],此时3-tuple的和sum=S[0]+S[1]+S[n-1]，如果sum的值大于0，则左移第三个元素，选取S[n-2]
 
