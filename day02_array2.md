## 代码随想录算法训练营day02|977 有序数组的平方，209 长度最小的子数组，509 螺旋矩阵II

- [977 有序数组的平方](https://leetcode.cn/problems/squares-of-a-sorted-array/)

思路：双指针，比较两个首尾两个指针的大小，移动较大的指针，直到指针相遇

```java
    public int[] sortedSquares(int[] nums) {
        //数组非递减，所以数组的平方的最大值只可能在数组两端取得
        int l = 0;
        int r = nums.length-1;
        int k = nums.length-1;
        int[] res = new int[nums.length];
        while(l <= r){
            if(nums[r]*nums[r] > nums[l]*nums[l]){
                res[k--] = nums[r]*nums[r];
                r--;
            }else{
                res[k--] = nums[l]*nums[l];
                l++;
            }
        }
        return res;
    }
```

- [209 长度最小的子数组](https://leetcode.cn/problems/minimum-size-subarray-sum/)

方法一：暴力(存在超时用例)

```java
    public int minSubArrayLen(int target, int[] nums) {
        //k  
        //***i 数组开始位置
        //j=i,j++,j<=i+k-1; sum += nums[j]
        int res = 999999;
            for(int i=0; i<nums.length; i++){
                int sum = 0;
                for(int j=i; j<nums.length; j++){
                    sum += nums[j];
                    if(sum >= target){
                       res = Math.min(res, j-i+1); 
                       //后面长度肯定比当前大
                       break;
                    }
                }
            }
        return res == 999999 ? 0 : res;
    }
```

方法二：滑动窗口

```java
public int minSubArrayLen(int target, int[] nums) {
            //维护一个总和大于target的数组
            int i =0;
            int sum = 0;
            int res = 999999;
            for(int j=0; j<nums.length; j++){
                sum+=nums[j];
                //不断尝试缩小窗口
                while(sum >= target){
                    res = Math.min(res,j-i+1);
                    sum -= nums[i++];
                }
            }
            return res == 999999 ? 0 : res;
        }
```

- [509 螺旋矩阵II](https://leetcode.cn/problems/spiral-matrix-ii/)

模拟

```java
public int[][] generateMatrix(int n) {
        //使用l,r,t,b来控制循环打印的边界
        //循环在达到n^2时终止
        int l = 0,r=n-1,t=0,b=n-1;
        int[][] nums = new int[n][n];
        int num = 1;
        while(num <= n*n){
            //从左到右
            for(int i=l; i<=r; i++) {
                nums[t][i] = num++;
            }
            t++;
            for(int i=t; i<=b; i++) {
                nums[i][r] = num++;
            }
            r--;
            for(int i=r; i>=l; i--) {
                nums[b][i] = num++;
            }
            b--;
            for(int i=b; i>=t; i--) {
                nums[i][l] = num++;
            }
            l++;
        }
        return nums;
    }
```

