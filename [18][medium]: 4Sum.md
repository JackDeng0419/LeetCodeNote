## Method 1: use 3 sum

```
class Solution {
    public List<List<Integer>> fourSum(int[] nums, int target) {
        if(nums.length < 4) {
            return new ArrayList<>();
        }
        Arrays.sort(nums);
        List<List<Integer>> res = new ArrayList<>();


        int i = 0;
        while (i <= nums.length - 4) {
            if(target < 0 && nums[i] > 0) {
                break;
            }

            int j = i + 1;
            while(j <= nums.length -3) {

                int m = j + 1;
                int n = nums.length - 1;

                while (m < n) {
                    int sum = nums[i] + nums[j] + nums[m] + nums[n];
                    
                    if(sum == target) res.add(Arrays.asList(nums[i], nums[j], nums[m], nums[n]));
                    if(sum >= target) while(nums[n] == nums[--n] && m < n);
                    if(sum <= target) while(nums[m] == nums[++m] && m < n);
                }
                while(j <= nums.length - 3 && nums[j] == nums[++j]);
            }
            
            while(i <= nums.length - 4 && nums[i] == nums[++i]);
        }

        return res;
    }
}
```