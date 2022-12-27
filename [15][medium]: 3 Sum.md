## Method 1: find the two sum

```
class Solution {
    public List<List<Integer>> threeSum(int[] nums) {
        Arrays.sort(nums);
        List<List<Integer>> res = new ArrayList<>();
        for(int i = 0; i<nums.length-2; i++) {
            if(i != 0 && nums[i] == nums[i-1]) {
                continue;
            }

            List<List<Integer>> twoSumRes = twoSum(nums, i+1, nums.length-1, -nums[i]);
            if(twoSumRes.size() != 0) {
                for(int j = 0; j < twoSumRes.size(); j++) {
                    List<Integer> subRes = new ArrayList<>();
                    subRes.add(nums[i]);
                    subRes.add(twoSumRes.get(j).get(0));
                    subRes.add(twoSumRes.get(j).get(1));
                    res.add(subRes);
                }
            }
        }

        return res;
    }

    public List<List<Integer>> twoSum(int[] nums, int first, int second, int target) {
        Map<Integer, Integer> map = new HashMap<>();
        Map<Integer, Integer> usedNum = new HashMap<>();
        List<List<Integer>> res = new ArrayList<>();
        for(int i = first; i <= second; i++) {
            if(i != first && usedNum.containsKey(nums[i])) {
                continue;
            }
            int i_target = target - nums[i];
            if(map.containsKey(i_target)) {
                List<Integer> subRes = new ArrayList<>();
                subRes.add(i_target);
                subRes.add(nums[i]);
                res.add(subRes);
                usedNum.put(nums[i], 1);
                usedNum.put(i_target, 1);
            }
            map.put(nums[i], i);
        }
        return res;
    }
}
```

## Method 2: two pointers
```
class Solution {

    public List<List<Integer>> threeSum(int[] nums) {
        Arrays.sort(nums);
        List<List<Integer>> res = new ArrayList<>();
        if(nums.length < 3) {
          return null;
        }
        int i = 0;
        while (i <= nums.length-3) {
            if(nums[i] > 0) {
                break;
            }
            int j = i + 1;
            int k = nums.length - 1;
            while(j < k) {
                int sum = nums[j] + nums[k] + nums[i];

                if(sum == 0) {
                    res.add(Arrays.asList(nums[i], nums[j], nums[k]));
                    j++;
                    k--;
                    while(nums[j-1] == nums[j] && j < k) j++;
                    while(nums[k+1] == nums[k] && j < k) k--;
                } else if (sum < 0) {
                    j++;
                    while(nums[j-1] == nums[j] && j < k) j++;
                } else {
                    k--;
                    while(nums[k+1] == nums[k] && j < k) k--;
                }
            }
            while(i <= nums.length-3 && nums[i] == nums[++i]);
        }
        return res;
    }
}
```