# Algorithm

#### 1.快速排序

```py
Class QuickSort:
    def quickSort(self,A,n):
        if n <= 1:
            return A
        left = []
        right = []
        pivot = A.pop()
        for i in A:
            if i < pivot:
                A.append(left[i])
            else:
                A.append(right[i])
        result = self.quickSort(left[i]) + [pivot] + self.quickSort(right[i])
        return result
```

#### 2.归并排序

```py
Class MergeSort:
    def mergeSort(self,A,n):
        if n <= 1:
            return A
        mid = len(A)//2
        left = mergeSort(A[:mid],mid)
        right = mergeSort(A[mid:],mid)
        i,j = 0,0
        result = []
        while i<len(left) and j<len(right):
            if left[i] <= right[j]:
                result.append(left[i])
                i+=1
            else:
                result.append(right[j])
                j+=1
        result += left[i:]
        result += right[j:]
        return result
```






Remove Duplicates from Sorted Array 

Given a sorted array nums, remove the duplicates in-place such that each element appear only once and return the new length.

Do not allocate extra space for another array, you must do this by modifying the input array in-place with O(1) extra memory.

Example 1:

Given nums = [1,1,2],

Your function should return length = 2, with the first two elements of nums being 1 and 2 respectively.

It doesn't matter what you leave beyond the returned length.
Example 2:

Given nums = [0,0,1,1,1,2,2,3,3,4],

Your function should return length = 5, with the first five elements of nums being modified to 0, 1, 2, 3, and 4 respectively.

It doesn't matter what values are set beyond the returned length.

[删除排序数组中的重复项](https://leetcode-cn.com/problems/remove-duplicates-from-sorted-array/description/)，因为想用python，第一想到的是
用set函数，set和dict类似，也是一组key的集合，但不存储value。由于key不能重复，所以，在set中，没有重复的key。利用这一特性，可以过滤掉重复元素。

但是仔细一看题目要求，完全不符合，题目是要求原地删除重复元素。如果用set方法，会返回一个新的字典，而原数组不会改变。list有个remove方法，remove方法
是一个没有返回值的原位置改变的方法，他修改了列表但是没有返回值。由于给定的是排序数组，这就容易多了，比较两两相邻的数组元素，相同就把其中的一个利用
remove方法从列表中移除。

```
class Solution:
    def removeDuplicates(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        i = 0
        while i < len(nums) - 1:
            if nums[i] == nums[i+1]:
                nums.remove(nums[i])
            else:
                i = i+1
        return len(nums)
```
特别简单的一题。自己还想了很久。。。

买卖股票的最佳时机 II
给定一个数组，它的第 i 个元素是一支给定股票第 i 天的价格。

设计一个算法来计算你所能获取的最大利润。你可以尽可能地完成更多的交易（多次买卖一支股票）。

注意：你不能同时参与多笔交易（你必须在再次购买前出售掉之前的股票）。

示例 1:

输入: [7,1,5,3,6,4]
输出: 7
解释: 在第 2 天（股票价格 = 1）的时候买入，在第 3 天（股票价格 = 5）的时候卖出, 这笔交易所能获得利润 = 5-1 = 4 。
     随后，在第 4 天（股票价格 = 3）的时候买入，在第 5 天（股票价格 = 6）的时候卖出, 这笔交易所能获得利润 = 6-3 = 3 。
示例 2:

输入: [1,2,3,4,5]
输出: 4
解释: 在第 1 天（股票价格 = 1）的时候买入，在第 5 天 （股票价格 = 5）的时候卖出, 这笔交易所能获得利润 = 5-1 = 4 。
     注意你不能在第 1 天和第 2 天接连购买股票，之后再将它们卖出。
     因为这样属于同时参与了多笔交易，你必须在再次购买前出售掉之前的股票。
示例 3:

输入: [7,6,4,3,1]
输出: 0
解释: 在这种情况下, 没有交易完成, 所以最大利润为 0。

思路：这道题比较简单，就是需要如果后面的股价大于前面的就应该买入卖出，反之就不进行操作。
```
class Solution:
    def maxProfit(self, prices):
        """
        :type prices: List[int]
        :rtype: int
        """
        benefit = 0
        if len(prices) == 0:
            return 0
        i = 0
        j = 1
        while (j < len(prices)):
            if (prices[j] > prices[i]):
                benefit += prices[j] - prices[i]
            j += 1
            i += 1
        return benefit
```

第二题：旋转数组
给定一个数组，将数组中的元素向右移动 k 个位置，其中 k 是非负数。

示例 1:

输入: [1,2,3,4,5,6,7] 和 k = 3
输出: [5,6,7,1,2,3,4]
解释:
向右旋转 1 步: [7,1,2,3,4,5,6]
向右旋转 2 步: [6,7,1,2,3,4,5]
向右旋转 3 步: [5,6,7,1,2,3,4]

思路：直接用切片，简洁，快速。
```
class Solution:
    def rotate(self, nums, k):
        """
        :type nums: List[int]
        :type k: int
        :rtype: void Do not return anything, modify nums in-place instead.
        """
        k = k%len(nums)
        nums[:] = nums[-k:]+nums[:-k]  
```

1.存在重复
给定一个整数数组，判断是否存在重复元素。

如果任何值在数组中出现至少两次，函数返回 true。如果数组中每个元素都不相同，则返回 false。

示例 1:

输入: [1,2,3,1]
输出: true
示例 2:

输入: [1,2,3,4]
输出: false
示例 3:

输入: [1,1,1,3,3,4,3,2,4,2]
输出: true

思路：python当中的set集合本身就是没有重复元素的，我们可以利用这个特性去判断真假
```
class Solution:
    def containsDuplicate(self, nums):
        """
        :type nums: List[int]
        :rtype: bool
        """
        if len(set(nums)) == len(nums):
            return False
        else:
            return True
```


2.只出现一次的数字
给定一个非空整数数组，除了某个元素只出现一次以外，其余每个元素均出现两次。找出那个只出现了一次的元素。

说明：

你的算法应该具有线性时间复杂度。 你可以不使用额外空间来实现吗？

示例 1:

输入: [2,2,1]
输出: 1
示例 2:

输入: [4,1,2,1,2]
输出: 4

思路：python的特点就是代码少，运算的比较慢，我们可以先把整个数组排序，如果只有一个数，那就是他了，如果不止一个数，看前两个是不是一样，一样的话
就把他们都删除，不一样就取第一个数。
```
class Solution(object):
    def singleNumber(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        nums.sort()
        for i in range(len(nums)):
            if len(nums) == 1:
                return nums[0]
            if nums[0] == nums[1]:
                del nums[0]
                del nums[0]
            else:
                return nums[0]
```

1.加一
给定一个由整数组成的非空数组所表示的非负整数，在该数的基础上加一。

最高位数字存放在数组的首位， 数组中每个元素只存储一个数字。

你可以假设除了整数 0 之外，这个整数不会以零开头。

示例 1:

输入: [1,2,3]
输出: [1,2,4]
解释: 输入数组表示数字 123。
示例 2:

输入: [4,3,2,1]
输出: [4,3,2,2]
解释: 输入数组表示数字 4321。

思路：看题目是数组的最后一位加了一个1，所以进位是我们需要考虑的，那么问题来了，倘若是9，进位不就是10了吗？那么就要重新插入一个insert(0,1)
```
class Solution:
    def plusOne(self, digits):
        """
        :type digits: List[int]
        :rtype: List[int]
        """
        carry = 1
        for i in range(len(digits)-1, -1, -1):
            if digits[i] + carry == 10:
                digits[i] = 0
                carry = 1
            else:
                digits[i] = digits[i] + carry
                carry = 0
        
        if carry == 1:
            digits.insert(0, 1)
        return digits
```

2.移动零
给定一个数组 nums，编写一个函数将所有 0 移动到数组的末尾，同时保持非零元素的相对顺序。

示例:

输入: [0,1,0,3,12]
输出: [1,3,12,0,0]
说明:

必须在原数组上操作，不能拷贝额外的数组。
尽量减少操作次数。

思路：pop函数有默认删除末尾的元素，但是只要我们判断列表中出现了0，就记录下下表，就能够把0给pop掉，再append在最后。
```
class Solution:
    def moveZeroes(self, nums):
        """
        :type nums: List[int]
        :rtype: void Do not return anything, modify nums in-place instead.
        """
        j=0
        for i in range(len(nums)):
            if nums[j] == 0:
                nums.append(nums.pop(j))

            else:
                j+=1
```

3.反转字符串
编写一个函数，其作用是将输入的字符串反转过来。

示例 1:

输入: "hello"
输出: "olleh"
示例 2:

输入: "A man, a plan, a canal: Panama"
输出: "amanaP :lanac a ,nalp a ,nam A"
思路：这道题实在是太简单，用python
```
class Solution:
    def reverseString(self, s):
        """
        :type s: str
        :rtype: str
        """
        new_s = ""
        for i in range(len(s)-1,-1,-1):
            new_s += s[i]
        return new_s
```
用在循环里面会让运行时间变得很慢。所以直接御用python的特性，return s[::-1]就好


4.字符串中的第一个唯一字符
给定一个字符串，找到它的第一个不重复的字符，并返回它的索引。如果不存在，则返回 -1。

案例:

s = "leetcode"
返回 0.

s = "loveleetcode",
返回 2.
思路：python中有collections.counter这个函数可以调用，作用是可以统计列表中相同字符的个数。
```
class Solution:
    def firstUniqChar(self, s):
        """
        :type s: str
        :rtype: int
        """
        dic = collections.Counter(s)
        for i in range(len(s)):
            if dic[s[i]] == 1:
                return i
        return -1
            
```


 1.字符串转整数（atoi）
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

.报数序列是指一个整数序列，按照其中的整数的顺序进行报数，得到下一个数。其前五项如下：

1.     1
2.     11
3.     21
4.     1211
5.     111221
1 被读作  "one 1"  ("一个一") , 即 11。
11 被读作 "two 1s" ("两个一"）, 即 21。
21 被读作 "one 2",  "one 1" （"一个二" ,  "一个一") , 即 1211。

给定一个正整数 n ，输出报数序列的第 n 项。

注意：整数顺序将表示为一个字符串。

示例 1:

输入: 1
输出: "1"
示例 2:

输入: 4
输出: "1211"
首先解释题目。我觉得问题就在于没有把题目解释清楚上。

1 读 one one

11 不读 one one one one,读 two one, 连着一起相同的数会先说数量再说值。

以上是基础。接下来看怎么得到下一项的结果。从题目所给出的示例4 ： 1211 到 5 : 111221。1211 第一位是1，所以读作 one one，也就是 1 1 .2读作one two, 
所以是12. 11连着读作two one, 所以是21.这所有加起来就是答案 111221。

思路：根据报数的特点，我们可以根据上一项的结果推导下一项。我们遍历上一项，辅以计数变量统计一下某些数字出现的次数。同时我们要不断保存上一项。
```
class Solution:  
    def countAndSay(self, n):  
        """ 
        :type n: int 
        :rtype: str 
        """  
        if n==1:#类似于斐波拉契数，后面的数跟前面的数有关  
            return '1'  
        if n==2:  
            return '11'
        #进行i=3时的循环时，它的上一项为'11'
        pre='11'
        
        #用for循环不断去计算逼近最后一次
        for i in range(3,n+1):  
            res=''#结果，每次报数都要初始化  
            cnt=1#计数变量
            
            length=len(pre)#遍历我们的上一项，所以记录它的长度
            for j in range(1,length):  
                if pre[j-1]==pre[j]:#相等则加一  
                    cnt+=1  
                else:
                    #一旦遇到不同的变量，就更新结果
                    res+=str(cnt)+pre[j-1]  
                    cnt=1#重置为1
            #把最后一项及它的数量加上
            res+=str(cnt)+pre[j]  
            pre=res#保存上一次的结果  
        return res
```

2.实现strStr()
实现 strStr() 函数。

给定一个 haystack 字符串和一个 needle 字符串，在 haystack 字符串中找出 needle 字符串出现的第一个位置 (从0开始)。如果不存在，则返回  -1。

示例 1:

输入: haystack = "hello", needle = "ll"
输出: 2
示例 2:

输入: haystack = "aaaaa", needle = "bba"
输出: -1
说明:

当 needle 是空字符串时，我们应当返回什么值呢？这是一个在面试中很好的问题。

对于本题而言，当 needle 是空字符串时我们应当返回 0 。这与C语言的 strstr() 以及 Java的 indexOf() 定义相符。

思路：haystack中的字符串和needle的要重合
```
class Solution:
    def strStr(self, haystack, needle):
        """
        :type haystack: str
        :type needle: str
        :rtype: int
        """
        len1 = len(needle)
        if len1 == 0:
            return 0
        for i in range(len(haystack)):
            if haystack[i:i+len1] == needle:
                return i
        return -1
```



## 2.review
[机器学习无监督学习算法——聚类](https://en.wikipedia.org/wiki/Cluster_analysis)

无监督学习中，聚类的算法有超过100种，但是目的都是从庞大的样本中选出有代表性的加以学习，或者选出很棒的特征来。
常用的有k-means，用于簇是密集的情况。类内紧凑，类间独立。
还有DBSCAN（具有噪声的基于密度的聚类），将具有足够密度的区域划分为簇，并在具有噪声的空间数据库中发现任意形状的簇。他将簇定义为密度相连的点的最大集合。
还有局部密度聚类，层次聚类和谱聚类。

## 3.tips
由于还在学校念书，就把科研或者遇到的问题记录下来。
一个循环队列的问题:
我们之所以把静态队列归为循环队列，是因为用数组实现的队列，如果仅仅是像普通的链式队列的话会导致浪费内存空间。
![循环队列](https://gss1.bdstatic.com/-vo3dSag_xI4khGkpoWK1HF6hhy/baike/c0%3Dbaike80%2C5%2C5%2C80%2C26/sign=2d7e279f259759ee5e5d6899d3922873/5d6034a85edf8db1ee973ff60a23dd54574e74e2.jpg)

一共有两个参数：
front和rear，这里简称f和r
内存中增加一个内容，r就往下一个移动，r是指向最后一个元素的下一个元素，若队列为空，f和r一定相等。
这样的话f和r就不会冲突。
(r+1)%长度 == f的话就说明整个队列满了。r==f就代表队列是空的。

## 4.share
这次分享一下读书心得，最近读《小王子》，这里[](https://book.douban.com/review/1000104/)
一切虽然有些讽刺大人们的物质功利世界，但是，我们又何尝不是活成了不想成为的样子呢？
一个小孩说，有一种车他最喜欢。于是大人们纷纷开始猜测，奔驰，大卡，云云。结果小孩说，他最喜欢垃圾车。
因为垃圾车来的时候，都有音乐。