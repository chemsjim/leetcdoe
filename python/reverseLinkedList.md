## 链表反转
---
将单向链表进行反转

**NOTE : 分别使用递归、非递归的方式实现**

### Example:
输入 : 1>2>3>4>5

输出 : 5>4>3>2>1

链表节点类：

	class ListNode():
	    def __init__(self, x):
	        self.val = x
	        self.next = None

非递归方式：

	class Solution(object):
	    def reverseList(self, head):
	        """
	        :type head: ListNode
	        :rtype: ListNode
	        """
	        res = None
	        while head:
	            tmp = head.next
	            head.next = res
	            res = head
	            head = tmp
	        return res

递归方式1：

	class Solution2(object):
	    def reverseList(self, head):
	        if head.next == None or head == None:
	            return head
	        if head.next:
	            res = self.reverseList(head.next)
	            head.next.next = head
	        head.next = None
	        return res
	
递归方式2：

	class Solution3(object):
	    res, tail = None, None
	    count = 0
	    def recursive(self, head):
	        self.count = self.count + 1
	        if not head.next:
	            self.res = self.tail = head
	          #  print self.res.val
	           # print self.tail.val
	            return
	        self.recursive(head.next)
	        self.tail.next = head
	        self.tail = head
	        self.tail.next = None

---
### 简单思路

1、非递归方式：无难度，主要考查链式数据结构的基本操作。

2、递归方式：递归所做的，就是把复杂的问题一级一级的展开，使得每一级的处理方法都一模一样，这是一种解决问题的思路，最终实现应该尽量采用其他实现方式，而不是使用递归实现。应该尽量采用‘递归’思路，而避免使用‘递归’代码，因为问题规模导致的递归深度往往是不可控的，会导致栈溢出，而使用非递归方式，可以认为控制栈的大小，以及及时捕获栈溢出，并进行处理。另外递归效率也不算特别优秀，如果代码写的不够严谨，递归可能会做很多重复的动作，导致效率降低。