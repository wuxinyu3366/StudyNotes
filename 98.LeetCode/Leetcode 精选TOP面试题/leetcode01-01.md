#### [1. 两数之和](https://leetcode-cn.com/problems/two-sum/)

==简单==

给定一个整数数组 nums 和一个整数目标值 target，请你在该数组中找出 和为目标值 的那 两个 整数，并返回它们的数组下标。

你可以假设每种输入只会对应一个答案。但是，数组中同一个元素不能使用两遍。

你可以按任意顺序返回答案。

![image-20210226225334793](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210226225334.png)

```java
class Solution {
    	// 时间复杂度：O(n^2)
    	// 空间复杂度：O(1)
    public int[] twoSum(int[] nums, int target) {
      if(nums==null||num.length==0){
        return new int [0];
      }
      for(int i=0;i<num.length;i++){
        int x=num[i];
        //线性查找
        for(int j = i+1;j<num.length;j++){
          if(nums[j]==target-x){
            return new int []{i,j};
          }
        }
      }
      return new int [0];

    }
}
```



#### [7. 整数反转](https://leetcode-cn.com/problems/reverse-integer/)

给你一个 32 位的有符号整数 x ，返回 x 中每位上的数字反转后的结果。

如果反转后整数超过 32 位的有符号整数的范围 [−231,  231 − 1] ，就返回 0。

假设环境不允许存储 64 位整数（有符号或无符号）。

![image-20210228194944734](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210228194951.png)

![image-20210228200008209](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210228200008.png)

[解题思路]https://leetcode-cn.com/problems/reverse-integer/solution/tu-jie-7-zheng-shu-fan-zhuan-by-wang_ni_ma/

```java
class Solution {
    public int reverse(int x) {
			int res = 0;
      while(x!=0){
        //每次取末尾数字
        int tmp = x % 10;
        //判断是否 大于 最大32位整数
        if (res > 214748364 || (res == 214748364 && tmp > 7)) {
          return 0;
        }
        //判断是否 小于 最小32位整数
        if (res < -214748364 || (res == -214748364 && tmp < -8)) {
          return 0;
        }
        res = res*10+tmp;
        x=x/10;
      }
      return res;
    }
}
```

#### [2. 两数相加](https://leetcode-cn.com/problems/add-two-numbers/)

给你两个 非空 的链表，表示两个非负的整数。它们每位数字都是按照 逆序 的方式存储的，并且每个节点只能存储 一位 数字。

请你将两个数相加，并以相同形式返回一个表示和的链表。

你可以假设除了数字 0 之外，这两个数都不会以 0 开头。

![image-20210228214003411](https://typora-wenjiuzhou.oss-cn-beijing.aliyuncs.com/20210228214003.png)

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
//时间复杂度 O（n）
//空间复杂度 O（n）
class Solution {
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
      ListNode pre = new ListNode(0);
      ListNode cur = pre;
      int carry=0;
      while(l1!=0||l2!=0){
        int x=l1==null?0:l1.val;
        int y=l2==null?0:l2.val;
        int sum=x+y+carry;
        
        carry=sum/10;
        //个位上的数字
        sum=sum%10;
        cur.next=new ListNode(sum);
        cur=cur.next;
        
        if(l1!=null){
          l1=l1.next;
        }
        if(l2!=null){
          l2=l2.next;
        }
      }
      if(carry==1){
        cur.next=new ListNode(carry);
      }
      //最开始那位为0
      return pre.next;
    }
}
```

