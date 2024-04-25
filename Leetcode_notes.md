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

