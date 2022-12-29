```
class Solution {
    public List<List<Integer>> groupThePeople(int[] groupSizes) {
        
        List<List<Integer>> res = new ArrayList<>();
        Map<Integer, List<Integer>> map = new HashMap<>();

        for(int i = 0; i < groupSizes.length; i++) {
            if(groupSizes[i] == 1) {
                List<Integer> subRes = new ArrayList<>();
                subRes.add(i);
                res.add(subRes);
            }
            if(map.containsKey(groupSizes[i]) && map.get(groupSizes[i]).size() != 0) {
                List<Integer> subRes = map.get(groupSizes[i]);

                subRes.add(i);

                if(subRes.size() == groupSizes[i]) {
                    res.add(subRes);
                    List<Integer> list = new ArrayList<>();
                    map.put(groupSizes[i], list);
                }
            } else {
                if(!map.containsKey(groupSizes[i])) {

                    List<Integer> list = new ArrayList<>();
                    list.add(i);
                    map.put(groupSizes[i], list);
                } else {
                    map.get(groupSizes[i]).add(i);
                }
            }
        }
        return res;
    }
}
```