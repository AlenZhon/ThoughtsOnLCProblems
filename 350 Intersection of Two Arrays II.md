# 350. Intersection of Two Arrays II

## 题目

给出两个数组，求出两个数组中均出现的元素。要求重复出现的元素都计算在内。

>Given two arrays, write a function to compute their intersection.
>
>**Example 1:**
>
>>Input: nums1 = [1,2,2,1], nums2 = [2,2]  
>>Output: [2,2]
>
>Example 2:
>
>>Input: nums1 = [4,9,5], nums2 = [9,4,9,8,4]  
>>Output: [4,9]
>
>**Note:**
>
> - Each element in the result should appear as many times as it shows in both arrays.
> - The result can be in any order.
>
>**Follow up:**
>
> - What if the given array is already sorted? How would you optimize your algorithm?
> - What if nums1's size is small compared to nums2's size? Which algorithm is better?
> - What if elements of nums2 are stored on disk, and the memory is limited such that you cannot load all elements into the memory at once?

## 解法

直接先排序了。简单粗暴。排序需要O(nlogn)，两个指针遍历需要O(n+m)。  
还可以在开头把空数组的边界情况先排除掉。

```java
public int[] intersect(int[] nums1, int[] nums2) {
        Arrays.sort(nums1); // assume sorted
        Arrays.sort(nums2); // assume sorted
        int l1 = nums1.length, l2 = nums2.length, length = Math.min(l1, l2);
        int[] intersection = new int[length];

        int i1 = 0, i2 = 0 , j = 0;
        while (i1 < l1 && i2< l2) {
            int val1 = nums1[i1], val2 = nums2[i2];
            if (val1 == val2) {
                intersection[j++] = val1;
                i1++;
                i2++;
            }
            else if (val1 > val2)
                i2++;
            else
                i1++;
        }
        return Arrays.copyOf(intersection, j);
    }
```

存成HashMap的方法：

```java
public int[] intersect(int[] nums1, int[] nums2) {
        Map<Integer, Integer> map = new HashMap<>();
        List<Integer> result = new ArrayList<>();
        for(int i=0;i<nums1.length;i++){
            if(map.containsKey(nums1[i])){
                map.put(nums1[i],map.get(nums1[i])+1);
            }
            else{
                map.put(nums1[i],1);
            }
        }
        for(int i=0;i<nums2.length;i++){
            if(map.containsKey(nums2[i])){
                if(map.get(nums2[i])>0){
                    map.put(nums2[i],map.get(nums2[i])-1);
                    result.add(nums2[i]);
                }
            }
        }
        int[] resArr = new int[result.size()];
        for(int i=0;i<result.size();i++){
            resArr[i]=result.get(i);
        }
        return resArr;
    }
```

Follow-Up的问题3可不可以把sums1，sums2切分成几段，每段并行去做比较？
