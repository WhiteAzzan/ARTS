# ARTS
algorithm, review, tips, share

## Algorithm
###1.字符串转整数（atoi）
实现 atoi，将字符串转为整数。

在找到第一个非空字符之前，需要移除掉字符串中的空格字符。如果第一个非空字符是正号或负号，选取该符号，并将其与后面尽可能多的连续的数字组合起来，这部分字符即为整数的值。如果第一个非空字符是数字，则直接将其与之后连续的数字字符组合起来，形成整数。

字符串可以在形成整数的字符后面包括多余的字符，这些字符可以被忽略，它们对于函数没有影响。

当字符串中的第一个非空字符序列不是个有效的整数；或字符串为空；或字符串仅包含空白字符时，则不进行转换。

若函数不能执行有效的转换，返回 0。

说明：

假设我们的环境只能存储 32 位有符号整数，其数值范围是 [−231,  231 − 1]。如果数值超过可表示的范围，则返回  INT_MAX (231 − 1) 或 INT_MIN (−231) 。

示例 1:

输入: "42"
输出: 42
示例 2:

输入: "   -42"
输出: -42
解释: 第一个非空白字符为 '-', 它是一个负号。
     我们尽可能将负号与后面所有连续出现的数字组合起来，最后得到 -42 。
示例 3:

输入: "4193 with words"
输出: 4193
解释: 转换截止于数字 '3' ，因为它的下一个字符不为数字。
示例 4:

输入: "words and 987"
输出: 0
解释: 第一个非空字符是 'w', 但它不是数字或正、负号。
     因此无法执行有效的转换。
示例 5:

输入: "-91283472332"
输出: -2147483648
解释: 数字 "-91283472332" 超过 32 位有符号整数范围。 
     因此返回 INT_MIN (−231) 。
     
思路：这道题着实是考的编程语言的技巧，我们通过正则表达式可以很好地解决
```     
class Solution:
    def myAtoi(self, str):
        """
        :type str: str
        :rtype: int
        """
        import re#导入正则表达式模块
        #^代表后面的就是开始的，[-+]?说明一开始可以是匹配正负号，也可以没有，\d+代表着后面可以匹配所有的整数
        list_s = re.findall(r"^[-+]?\d+", str.strip()) #strip()是把两边的空格去掉
        if not list_s: 
            return 0
        else:
            num =int(''.join(list_s)) #列表转化为字符串，然后转化为整数
            if num >2**31 -1:
                return 2**31 -1
            elif num < -2**31:
                return -2**31
            else:
                return num
 ```
