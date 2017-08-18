### 二叉搜索树的最低祖先结点
---
For example, the lowest common ancestor (LCA) of nodes 2 and 8 is 6. Another example is LCA of nodes 2 and 4 is 2, since a node can be a descendant of itself according to the LCA definition.

给出一个二叉搜索树(BST)，找出指定两个结点的最低的公共祖先结点(LCA)。

根据维基百科关于LCA的定义：在树中的两个结点v和w，的最低公共祖先结点应该是同时能将v和w作为后代结点的结点。（允许一个结点作为自己的后代结点）

### Example:
	        _______6______
	       /              \
	    ___2__          ___8__
	   /      \        /      \
	   0      _4       7       9
	         /  \
	         3   5


结点2和结点6的最低公共祖先点是6。而结点2和结点4的最低公共祖先结点是4，因为一个结点允许作为自己的子孙结点。

### python 实现如下：
	#Definition for a binary tree node.
	class TreeNode(object):
	     def __init__(self, x):
	         self.val = x
	         self.left = None
	         self.right = None

	class Solution(object):
	    def service(self, root, p, q):
	        if root == None:
	            return None
	        if p.val <= root.val and q.val >= root.val:
	            return root
	        elif q.val <= root.val:
	            return self.lowestCommonAncestor(root.left, p, q)
	        elif p.val >= root.val:
	            return self.lowestCommonAncestor(root.right, p, q)
	
	    def lowestCommonAncestor(self, root, p, q):
	        """
	        :type root: TreeNode
	        :type p: TreeNode
	        :type q: TreeNode
	        :rtype: TreeNode
	        """
	        if p.val <= q.val:
	            res =  self.service(root, p, q)
	        else:
	            res = self.service(root, q, p)
	        return res

---
### 简单思路

对于两个结点v和w，他们的最低公共祖先结点满足一个条件，即v.val<=root.val<=w.val或者w.val<=root.val<=v.val。 利用递归，对左子树、又子书进行相同的递归操作。 

