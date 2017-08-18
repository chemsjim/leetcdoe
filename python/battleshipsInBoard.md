### 甲板上战舰的数量
---
Follow up:
Could you do it in one-pass, using only O(1) extra memory and without modifying the value of the board?

给出一个二维甲板，计算甲板上有多少战舰。在甲板中，“X”代表战舰，“."代表空槽位。输入数据遵循以下规则：

- 程序收到的输入为有效的输入，即只包含战舰与空槽位。
- 战舰只能水平或者垂直停放，换句话说，在2D甲板上，代表战舰的排列只能是 1XN（水平存放，一行N列），或者NX1(垂直存放，N行一列）。N可以是任何大小。 
- 两个停放的战舰之间至少会相隔一个垂直、水平的单元格。不会出现两个紧邻的战舰。

**Note: 最好只遍历一遍，利用O(1)的额外内存，并且不能修改输入**
### Example:
有效输入:
["X..X","...X","...X"]

在上面输入的甲板上，有两辆战舰

无效输入:
["...X","XXXX","...X"]

上面输入为无效输入，这种不遵循题目阐述规则的的甲板，不会作为输入。战舰之间没有相隔一行、一列单元格，即出现了紧邻的战舰。

### python 实现如下：
	class Solution(object):
	    def countBattleships(self, board):
	        """
	        :type board: List[List[str]]
	        :rtype: int
	        """
	        count = 0
	        for i in xrange(len(board)):
	            for j in xrange(len(board[i])):
	                if board[i][j] == '.':
	                    continue
	                if i > 0 and board[i - 1][j] == 'X':
	                    continue
	                if j > 0 and board[i][j - 1] == 'X':
	                    continue
	                count = count + 1
	        return count
	
	
	if __name__ == '__main__':
	    board = ["X..X","...X","...X"]
	
	    solution = Solution()
	    print solution.countBattleships(board)

---
### 简单思路

只对战舰的“头部”进行计数：在遍历甲板的过程中，如果X的左面，或者上面为“X"，则代表此单元不是战舰的头部，直接跳过。如果为"."，这代表此单元格为战舰的头部，进行计数
 

