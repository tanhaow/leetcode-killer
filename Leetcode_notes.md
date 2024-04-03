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





