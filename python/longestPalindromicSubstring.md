## 求出字符串中的最长子回文

### Example:
输入: "babad"
输出: "bab"

### 注意: "aba"同样为正确答案。

### python实现如下：
    class Solution(object):
        def longestPalindrome(self, s):
            """
            :type s: str
            :rtype: str
            """
            maxlen = -1
            index = -1
            for i in range(len(s)):
                maxPal, startIndex = self.getOddMaxPal(s, i)
                # print "1" + str(maxPal) + "\t" + str(startIndex)
                maxPal1, startIndex1 = self.getEvenMaxPal(s, i)
                #print "2" + str(maxPal1) + "\t" + str(startIndex1)

                if maxPal1 > maxlen:
                    maxlen, index = maxPal1, startIndex1
                if maxPal > maxlen:
                    maxlen, index = maxPal, startIndex
            print maxlen,index
            return s[index:maxlen + index]

        def getOddMaxPal(self, s, pivot):
            i = pivot - 1
            j = pivot + 1
            maxPal = 1  
            startIndex = pivot
            while i >= 0 and j < len(s) and s[i] == s[j]:
                maxPal = maxPal + 2
                startIndex = i
                i = i - 1
                j = j + 1
            return maxPal, startIndex

          def getEvenMaxPal(selfself, s, pivot):
                i = pivot
                j = pivot + 1
                maxPal = 0
                startIndex = pivot
                while i >= 0 and j < len(s) and s[i] == s[j]:
                    maxPal = maxPal + 2
                    startIndex = i
                    i = i - 1
                    j = j + 1
                return maxPal, startIndex


    if __name__ == '__main__':
        solution = Solution()
        caseStr = 'aaaaa'

        print solution.longestPalindrome(caseStr)

