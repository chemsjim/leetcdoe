## 判断单向链表是否为回文
---
给出一个特殊链表，链表中每个节点中额外包含一个指针，随机指向链表中的任意节点（可以为空）。
将次链表进行deep copy

**NOTE：deep copy如字面意思，在内存中新建一个新的链表，与所给链表的值相同**

### Example:
输入: S = [-1, 0, 1, 2, -1, -4]

输出: Res = [-1, 0, 1, 2, -1, -4]

且Res != S

### python实现
	# Definition for singly-linked list with a random pointer.
	class RandomListNode(object):
	    def __init__(self, x):
	        self.label = x
	        self.next = None
	        self.random = None

	class Solution(object):
	    def copyRandomList(self, n1):
	        """
	        :type head: RandomListNode
	        :rtype: RandomListNode
	        """
	
	        randomIndexMap, index, head = {}, 0, n1
	        while head:
	            if head.random != None:
	                if head.random in randomIndexMap:
	                    randomIndexMap[head.random].append(index)
	                else:
	                    randomIndexMap[head.random] = [index]
	            head, index = head.next, index + 1
	        '''print "random index map"
	        for r in randomIndexMap:
	            print "%s : %s" % (r.label, randomIndexMap[r])'''
	        head, map, index = n1, {}, 0
	        while head:
	            if head in randomIndexMap:
	                for i in randomIndexMap[head]:
	                    map[i] = index
	                    #map[randomIndexMap[head][i]] = index
	            head, index = head.next, index + 1
	        '''print "map"
	        for m in map:
	            print "%s : %s" % (m, map[m])'''
	        index, head, resIndexMap = 0, n1, {}
	        reshead = res = RandomListNode(-1)
	        while head:
	            reshead.next = RandomListNode(head.label)
	            resIndexMap[index] = reshead.next
	            head, reshead, index = head.next, reshead.next, index + 1
	
	        index, reshead = 0, res.next
	        while reshead:
	            if index in map:
	                reshead.random = resIndexMap[map[index]]
	            else:
	                reshead.random = None
	            reshead, index = reshead.next, index + 1
	
	        return res.next

	if __name__ == '__main__':
	    n1 = RandomListNode(1)
	    n2 = RandomListNode(2)
	    n3 = RandomListNode(2)
	    n4 = RandomListNode(2)
	
	    n1.next = n2
	    n2.next = n3
	    n3.next = n4
	
	    n1.random = n1
	    n3.random = n3
	    n4.random = n3
	
	    solution = Solution()
	    res = solution.copyRandomList(n1)
	    while res:
	        print res.label
	        if res.random and res.next:
	            print "next:%s \t random:%s" % (res.next.label, res.random.label)
	        elif res.random and not res.next:
	            print "next:%s \t random:%s" % (None, res.random.label)
	        else:
	            print "next:%s \t random:%s" % (res.next.label, None)
	        res = res.next




---
### 简单思路

普通链表的copy非常简单，只需进行一遍遍历。难点在于如何建立父节点与随机子节点的映射关系，这里利用了一个Map，来存储这种映射关系。对链表进行编号，遍历两次，在遍历过程中，将附近点与随机子节点的编号映射存入map。在新建结果链表时，同样对链表节点进行编号，从map中得到随机子节点编号。
 
