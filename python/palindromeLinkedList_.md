## 判断单向链表是否为回文
---
判断单向链表是否为回文

**NOTE : 算法性能要求：空间复杂度O(1)，时间复杂度O(N)**

### python实现
#### Solution1
	# Definition for singly-linked list.
	class ListNode(object):
	    def __init__(self, x):
	        self.val = x
	        self.next = None
	class Solution(object):
	    def isPalindrome(self, head):
	        """
	        :type head: ListNode
	        :rtype: bool
	        """
	        list = []
	        while head:
	            list.append(head.val)
	            head = head.next
	        return True if list[-1::-1] == list[0:] else False

#### Solution2
	# Definition for singly-linked list.
	class ListNode(object):
	    def __init__(self, x):
	        self.val = x
	        self.next = None
	class Solution3(object):
	    def isPalindrome(self, head):
	        """
	        :type head: ListNode
	        :rtype: bool
	        """
	        if head == None or head.next == None:
	            return True
	       # O(N) time complexity O(1) space complexity
	        fast, slow = head, head
	        while fast != None and fast.next != None:
	            fast = fast.next.next
	            slow = slow.next
	
	        # even count
	        if fast == None:
	            pass
	        # odd count
	        else:
	            slow = slow.next
	
	        lastHalf = self.reverseList(slow)
	        flag = True
	        while lastHalf != None:
	            if lastHalf.val != head.val:
	                flag = False
	            lastHalf = lastHalf.next
	            head = head.next
	        return flag
	
	    def reverseList(self, head):
	        if head.next == None:
	            return head
	        res = self.reverseList(head.next)
	        head.next.next = head
	        head.next = None
	        return res

---
### 简单思路
- Solution1

	最先想到的，将链表元素放入数组进行判断。但是空间复杂度为O(N),无法达到要求

- Solution2
	
	声明两个游标，slow、fast。fast的移动速度为slow的两倍，当fast移动到链表尾部的时候，slow正好移动到链表中部。此时可以利用slow，将链表的一半进行反转，然后对比，判断是否为回文。此时满足题目要求，时间复杂度为O(N)，并且空间复杂度为O(1)。

### 疑惑

想到了对链表进行反转，但是如果链表进行反转的话，就会修改输入，在这种情况下，空间复杂度是否为O(N)。论坛中，大家满足要求的实现，均建立在链表反转的情况下。空间复杂度的定义：程序运行占用的空间，除去输入数据的空间，额外占用的空间，即为程序的空间复杂度，但是这个定义的先决条件是，输入为read-only，不能对修改输入。所以根据教材的定义，基于链表反转的实现方法，空间复杂度为O(N).....
 
