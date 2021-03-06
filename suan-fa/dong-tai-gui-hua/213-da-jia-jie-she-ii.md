# 213 打家劫舍 II

你是一个专业的小偷，计划偷窃沿街的房屋，每间房内都藏有一定的现金。这个地方所有的房屋都围成一圈，这意味着第一个房屋和最后一个房屋是紧挨着的。同时，相邻的房屋装有相互连通的防盗系统，如果两间相邻的房屋在同一晚上被小偷闯入，系统会自动报警。

给定一个代表每个房屋存放金额的非负整数数组，计算你在不触动警报装置的情况下，能够偷窃到的最高金额。

```java
输入: [2,3,2]
输出: 3
解释: 你不能先偷窃 1 号房屋（金额 = 2），然后偷窃 3 号房屋（金额 = 2）, 因为他们是相邻的。

输入: [1,2,3,1]
输出: 4
解释: 你可以先偷窃 1 号房屋（金额 = 1），然后偷窃 3 号房屋（金额 = 3）。
     偷窃到的最高金额 = 1 + 3 = 4 。
```

和上一题一样，不同之处就是分别计算是否偷第一家的结果，然后取两次结果最大值

```java
class Solution {
    public int rob(int[] nums) {
        int len = nums.length;
        if (len == 0) {
            return 0;
        } 
        if (len == 1) return nums[0];
    
        return Math.max(doRob(Arrays.copyOfRange(nums, 0, nums.length - 1)), 
                doRob(Arrays.copyOfRange(nums, 1, nums.length)));
   
    }

    public int doRob(int[] nums) {
        int len = nums.length;
        if (len == 0) {
            return 0;
        } 
        if (len == 1) return nums[0];
        if (len == 2) return Math.max(nums[1], nums[0]);

        int[] d = new int[len];
        d[0] = nums[0];
        d[1] = Math.max(nums[1], d[0]);

        for (int i = 2; i < len; i++) {
            d[i] = Math.max(nums[i] + d[i - 2], d[i - 1]);
        }
        return d[len -1 ];
    }
}
```

