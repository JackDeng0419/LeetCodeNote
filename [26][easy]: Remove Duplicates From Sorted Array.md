## Method 1: 2 pointers

```
class Solution {
    public int removeDuplicates(int[] nums) {
        if(nums.length == 1) return 1;
        int i = 1;
        int j = 1;
        int k = 1;
        int currentNum = nums[0];
        while(i < nums.length) {
            if(nums[i] != currentNum) {
                currentNum = nums[i];
                nums[j] = nums[i];
                j++;
                k++;
            } 
            i++;
        }

        return k;
    }
}
```