## Record

### Apr 1, 2024

今日2题：

875. Koko Eating Bananas
    
    trick: use res = min(res, new_res) to keep track of the best result

153. Find Minimum in Rotated Sorted Array
    
    "write an algorithm that runs in O(log n) time" --> immediately think about Binary Search



### Apr 2, 2024

Joined leetcode-master bootcamp:

https://github.com/youngyangyang04/leetcode-master

useful tools can be found in: 

https://www.yuque.com/chengxuyuancarl/wnx1np/ktwax2



**Tips for Debugging**

1. for循环内部出现问题: print i 来定位轮次
```Java
for(int i = 0; i < n; i ++){
    //输出语句
    System.out.println(i + " " + 任意你下面可能用到的变量);  
    一系列逻辑操作
    System.out.println(i + " " + 任意你上面用到的变量);
    //注意i是必须要有的可以看轮次,如果一系列操作出出现了异常可以定位出第几次
}
```


2. 链表出现问题,空针异常:
```Java
ListNode list = new ListNode();
ListNode next = list.next;
int cnt = 0; //标记轮次
    while(判断逻辑){
        逻辑操作
		System.out.println(cnt + "  " + list.val + " "  + next.val+ " " + 你想加的); //出现空针异常可以看一下上一轮的值
        cnt ++;
        //上面的找不出问题继续
        System.out.println((list.next == next) + " " + 一系列可能引起空针或者环的操作或者值或者地址)  
    }
```


3. 数组越界问题
```Java
int cnt = 0; // 用来定位, 如果for循环可以每次都声明一次这个没关系的
System.out.println(cnt + " " + 下标); 
// 用到下标的任意代码
cnt ++;
System.out.println(cnt + " " + 下标);
//找到没有打的输出语句的前一轮次可以定位问题,因为我们的日志也打了输出语句所以你可以看到下标是多少
```

4. 判断是否进入if
```Java
if(){
    //任意输出
}
//如果没进入在if上面打输出语句看你的变量是否正确
```

5. 树递归
```Java
int cnt = 0;//轮次变量
void f(TreeNode root){ //递归的方法
    if(root == null) System.out.println(cnt); //放空针异常
    else System.out.println(root.val +  " " + cnt); //根据root.val和cnt来判断到哪个节点了
    cnt ++;
    //逻辑操作(可能含有递归,没关系我们的cnt是全局的)
    if(root == null) System.out.println(cnt); //放空针异常
    else System.out.println(root.val +  " " + cnt);
    cnt ++;
} 
//再来个层序
while(!q.isEmpty()){
    //任何获取到TreeNode后的操作和需要用到TreeNode的地方之前打一个输出即可
    //操作前操作后都需要打！！！！！！！！！！！
}
```


今日2题：

704. Binary Search
    
    **一种更好的求mid的方法**
    我之前的： int mid = (left + right) / 2;
    更好的：int mid = left + ((right - left) >> 1);
        `(right - left)`: 这个部分计算的是left和right之间的距离或者说是它们的差值。这个差值表示了从left到right有多少个元素间隔。
        `>> 1`: 这个操作是位运算中的右移操作。将任何数字右移1位，效果等同于将该数字除以2。
    这种计算中点的方式有2个好处：
    防止溢出：直接使用(left + right) / 2可能在left和right都很大的时候导致整数溢出。通过先计算差值然后再加上left，可以避免这个问题。
    效率：位运算的效率通常高于除法运算。
    

27. Remove Element
    
    two pointers不只是一左一右的，也可以两个都在左边起点。


### Apr 3, 2024

今日2题：

977. Squares of a Sorted Array
    
    很简单。秒了。也是two pointers。
    
```Python3
    for i in range(len(nums)):
    nums[i] = nums[i] * nums[i]
    // Tip: 关于square a array，下面这样写更优雅。
    nums = [num * num for num in nums]
```

121. Best Time to Buy and Sell Stock

    我的做法是先算出每天的profit变化，然后找max_profit，我的答案在memeory上优于97.5%的答案。但另一种方式更直观更简单：https://youtu.be/1pkOgXD63yU
    
    我原本困惑的点在于为什么prices[r] <= prices[l]就要l += 1。
    其实很简单，当第二天没有利润的时候，说明股票跌了，那么这个时候入手，肯定比之前入手要好。所以不用担心前一天的价格还没有loop完不知道结果，因为不管怎么样从后面一天入手都更好。所以直接将左边的pointer移到现在的最低价位处，l = r。
    
3. Longest Substring Without Repeating Characters    
    
    我原本以为set()里element的顺序是随机的，但其实set()是有顺序的，dictionary里的才没有，之后不要弄混了。所以，可以用`charSet = set()`来记录char出现过的顺序。

    其次，滑窗的时候要注意是用while而不是if，只要条件满足，就应该继续滑动。
    
    滑窗 = 用一个for循环来完成暴力解法两个for循环才能完成的事。for里循环的是r（终点位置），我们自己需要想办法移动l（起点位置）。for循环会一次一次奖终点位置向后移动，当满足条件时，我们自动起点位置，来试图更加逼近条件。
    https://www.bilibili.com/video/BV1tZ4y1q7XE/
    
    `min_len = float('inf')` 这行代码在Python中的意思是将变量`min_len`初始化为无穷大。在Python中，`float('inf')`表示正无穷大，而`float('-inf')`表示负无穷大。将变量初始化为无穷大在某些算法中非常有用，特别是在需要找到最小值的情况下。
    初始化`min_len`为无穷大的目的是为了确保在后续的比较中，任何实际的、有限的长度值都会小于`min_len`。这样，第一次比较就可以成功更新`min_len`为一个实际的长度值。这种方法常用于求最小值的问题。

59. Spiral Matrix II
    
    four pointers: left, right, top, bottom.
    
    When to terminate the loop? When left cross right, top cross bottom.
    
    Neetcode老哥讲得太好了：https://youtu.be/RvLrWFBJ9fM
    
    
### Apr 23, 2024

Linked List问是否有环(loop) -> 快慢指针

找环形入口： x = z
![示意图](https://code-thinking-1253855093.file.myqcloud.com/pics/20220925103433.png)


### Apr 24, 2024

什么用哈希法？-> **当我们遇到需要判断一个元素是否出现过的场景，第一时间想到哈希法！**
这句话很重要，大家在做哈希表题目都要思考这句话。 
比如在202. Happy Number里，需要判断一个sum是否重复出现过，就可以使用哈希法，用一个unordered set来判断sum是否出现过。

**常见的三种哈希结构：**
当我们想使用哈希法来解决问题的时候，我们一般会选择如下三种数据结构：
**数组
set（集合）
map（映射)**
哈希法牺牲了空间换取了时间，因为我们要使用额外的数组，set或者是map来存放数据，才能实现快速的查找。

**divmod(n1, n2)的用法：**
n, r = divmod(112, 10): 
先div(n = 112 // 10 = 11), 然后mod(r = 112 % 10 = 2)

**.index(n):** 可以通过nums.index(n)来获取某一个数在List里的index。

**2sum**用hashset，**3sum**和**4sum**用two pointers(l, r)，4sum就是在3sum上多套了一个loop而已。


### Apr 25, 2024

今天在练习字符串，下面这个python的写法很巧妙，学习一下。
541. Reverse String II
```class Solution:
    def reverseStr(self, s: str, k: int) -> str:
        # Two pointers. Another is inside the loop.
        p = 0
        while p < len(s):
            p2 = p + k
            # Written in this could be more pythonic.
            s = s[:p] + s[p: p2][::-1] + s[p2:]
            p = p + 2 * k
        return s
```

**双指针法**是字符串处理的常客。
**双指针法的效率优势**：通过两个指针在一个for循环下完成两个for循环的工作，将O(n^2)的时间复杂度降为O(n)。

其实很多数组（字符串）填充类的问题，都可以先预先给数组扩容带填充后的大小，然后在**从后向前**进行操作。
为什么要从后向前填充，从前向后填充不行么？从前向后填充就是O(n^2)的算法了，因为每次添加元素都要将添加元素之后的所有元素向后移动。


KMP算法是字符串查找最重要的算法。
还剩KMP算法没看，明天起来看一下，一刷可以先不用完全搞懂。


### Apr 26, 2024

今天开始练stack和queue

**232. Implement Queue using Stacks**
用两个stack模拟queue

**225. Implement Stack using Queues**
用一个deque模拟stack

有点晕。多练练。

![stack vs. queue](https://web.stanford.edu/class/archive/cs/cs106b/cs106b.1206/lectures/stacks-queues/img/stacks-queues.png)
Stack是叠起来的，LIFO，越靠后进去的越先出来。
Queue是一队列的，FIFO，最先进去的最先出来。

20. Valid Parentheses
要注意检查stack是不是空了(if stack)，如果空了就不能pop了；并且，结束的时候如果不是空的，就说明就问题。


1047. 删除字符串中的所有相邻重复项 

Stack的经典应用。Stack很适合这种类似于消消乐的操作，因为stack帮助我们记录了，遍历数组当前元素时候，前一个元素是什么。




**⚠️注意：int() 和 //(integer division) 不一样，在负数时是有区别的**
int()是向0取整，//是向下取整。

- `int(-13 / 5)` results in `-2` -- 向0取整
- `-13 // 5` results in `-3` -- 向下取整

正数时看似一样，但实则内在逻辑不同：
- `13 // 5` results in `2` -- 向0取整
- `int(13 / 5)` results in `2` -- 向下取整

这么看的话，计算类的题里用int()应该更普遍。


一道有意思的hard：
239. Sliding Window Maximum
如果不是两侧滑动窗口，只增加数字不减少数字的话，用一个大顶堆（优先级队列/max-heap）来存放数字，每次只能弹出最大值，就行了。但问题是，这个窗口是固定长度滑动的，每一次增加一个数字，都会减少一个数字，而大顶堆记录的是所有见到过的最大值，而不是滑动窗口里面的所有数值。

这道题，我们要用到**单调队列(Monotonic Queue)**，即单调递减(non-increasing)或单调递增(non-decreasing)的队列。这个队列没有必要维护窗口里的所有元素，只需要维护有可能成为窗口里最大值的元素就可以了，同时保证队列里的元素数值是由大到小的。

**pop():** 每次pop的时候，比较当前要pop的数值是否是队列前端出口的数值(也就是说我们要pop的这个值是当前记录的最大值)，如果是最大值，就说明这一步里窗口从最大值划走了，于是，把之前记录的最大值pop掉，我们需要重新找最大值了。**-> 这就解决了我们记录的是滑动窗口里面的最大值。**
**push():** 如果push进去的数值大于后段入口元素的数值，那么就将队列后端的数值pop掉（因为我们找到比这个数更大的值了），一直pop到要push进去的数值小于等于队列入口元素的数值为止。**-> 这样就保持了队列里的数值是单调从大到小的了。
**


347. Top K Frequent Elements

这道题有很多坑，可以多练几遍。我之前是用hash table做的，这次知道了也可以用heap(priority queue)做。

**小顶堆每次将最小的元素弹出** 用于统计最大前k个元素 -> 小顶堆每次将最小的元素弹出，最后剩下的就是前k个最大元素。
**大顶堆每次将最大的元素弹出** 用于统计最小前k个元素 -> 大顶堆每次将最大的元素弹出，最后剩下的就是前k个最小元素。

Python 的 heapq 默认提供的是小顶堆，需要将优先级取负来实现最大堆。
```
    默认小顶堆：heapq.heappush(min_heap, (priority, task))
    取负变成大顶堆：heapq.heappush(max_heap, (-priority, task))
```
Java 的 PriorityQueue 默认是小顶堆，需要自定义比较器来实现最大堆。
```
    默认小顶堆：PriorityQueue<Integer> minHeap = new PriorityQueue<>();
    加反转器变成大顶堆：PriorityQueue<Integer> maxHeap = new PriorityQueue<>(Collections.reverseOrder());
    
    * 默认的小顶堆其实相当于：PriorityQueue<Integer> minHeap = new PriorityQueue<>(Integer::compareTo);
    Integer::compareTo是按照自然升序（由小到大）来排序的

```

C++ 的 priority_queue 默认是大顶堆，需要自定义比较器来实现最小堆。
```
    默认大顶堆：priority_queue<int> maxHeap;
    priority_queue<int, vector<int>, greater<int>> minHeap;
    
    * 默认的小顶堆相当于：priority_queue<int, vector<int>, less<int>> minHeap;
    只不过less被默认省略去了
```

std::priority_queue<int, std::vector<int>, std::greater<int>> minHeap;


