## 代码随想录算法训练营第一天| 704. 二分查找、27. 移除元素

- ##### [704. Binary Search](https://leetcode.cn/problems/binary-search/description/)

思路：二分查找

```java
	public int search(int[] nums, int target) {
        //3种情况，等于中间值，小于
        int l = 0;
        int r = nums.length - 1;
        while (l <= r){
            int mid = (l+r)/2;
            if (nums[mid] < target){
               l = mid + 1;
            }else if (nums[mid] > target){
                r = mid -1;
            }else{
                return mid;
            }
        }
        return -1;
    }
```

- ##### [27.移除元素](https://leetcode.cn/problems/remove-element/description/)

首先用暴力循环写,这里数组会变小，为了索引到正确的元素，下标也要变小才行;

时间复杂度为O(n^2)

```java
	//方法1：暴力
    public int removeElement(int[] nums, int val) {
       //第一层循环遍历数组，第二层循环删除元素移动数组,数组的长度会变
       if(nums.length == 0) return 0;
        int size = nums.length;
        for(int i=0; i<size; i++){
            if(nums[i] == val){
                for(int j=i; j<size-1; j++){
                    nums[j] = nums[j+1];
                }
                size--;
                i--;//数组大小减1，那么原来下标i+1对应元素（这是下一个要判断的值）在新数组中对应下标应为i，所以要减1，那再移动加1的时候下标就是正确的;
            }
        }
        return size;
    }
```

使用双指针，最坏情况左右指针都遍历一次，时间复杂度为O(n)

```java
//方法2：双指针（未优化）
public int removeElement(int[] nums, int val) {
    //左指针，下一个被替换的位置
   int index = 0;
   //右指针遍历数组，若数组元素不等于val，移动左右两个指针；等于只移动右指针；
   //新数组[0,index-1],index是下一个被替换的位置，所以新数组长度是index
   for(int i=0; i< nums.length; i++){
       if(nums[i] != val)
         nums[index++] = nums[i];
   }
   return index;
}
```
- ##### [35.搜索插入位置](https://leetcode.cn/problems/search-insert-position/)

```java
    public int searchInsert(int[] nums, int target) {
        //不存在插入位置 就是l的位置
        int l = 0;
        int r = nums.length-1;
        while(l <= r){
            int mid = (r-l)/2+l;
            if(nums[mid] == target) return mid;
            else if(target < nums[mid]) 
                r = mid-1;
            else 
                l = mid+1;
        }
        return l;
    }
```

