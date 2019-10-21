# 599. Minimum Index Sum of Two Lists

## 题目

两个人商量去吃饭，他们心中都有一个喜欢餐馆的列表，找到两个列表中的相同餐馆，要求该餐馆在两个列表的下标之和相加最小。如果有多个餐馆同时具有最小值则都输出。

>Suppose Andy and Doris want to choose a restaurant for dinner, and they both have a list of favorite restaurants represented by strings.
>
>You need to help them find out their common interest with the least list index sum. If there is a choice tie between answers, output all of them with no order requirement. You could assume there always exists an answer.
>
>Example 1:
>
>>Input:
>>`["Shogun", "Tapioca Express", "Burger King", "KFC"]`  
>>`["Piatti", "The Grill at Torrey Pines", "Hungry Hunter Steakhouse", "Shogun"]`  
>>Output: `["Shogun"]`
>>Explanation: The only restaurant they both like is "Shogun".
>
>Example 2:
>>
>>Input:
>>`["Shogun", "Tapioca Express", "Burger King", "KFC"]`  
>>`["KFC", "Shogun", "Burger King"]`  
>>Output: `["Shogun"]`
>>Explanation: The restaurant they both like and have the least index sum is "Shogun" with index sum 1 (0+1).
>
>Note:
>
> 1. The length of both lists will be in the range of [1, 1000].
> 2. The length of strings in both lists will be in the range of [1, 30].
> 3. The index is starting from 0 to the list length minus 1.
> 4. No duplicates in both lists.

## 解法

还是用HashMap，先存其中一个列表，保存成`<String, Integer>`的键值对，完成餐馆名字到下标的映射。再比较另一个列表中的餐馆，如果在map中有key，说明两个人都想吃这家餐馆，计算一下这家餐馆的下标之和。

需要一个list保存当前最小下标之和对应的餐馆名字。如果找到了一个新的最小下标和，就得把list清空重新保存。

时间复杂度O(`l1+l2`)，和两个列表的长度有关。空间复杂度取决于list1的长度以及每个字符串字符数。用O(`l1 * x`)表示，x为字符串的平均长度。

```java
public String[] findRestaurant(String[] list1, String[] list2) {
        HashMap<String, Integer> map = new HashMap<>();
        for (int i =0; i< list1.length; i++)
            map.put(list1[i], i);
        List<String> ret = new ArrayList<>();
        int minIndex = 2000, sum;
        for (int i = 0;i < list2.length; i++) {
            if (map.containsKey(list2[i])) {
                sum = map.get(list2[i]) + i;
                if (sum < minIndex) {
                    ret.clear();
                    ret.add(list2[i]);
                    minIndex = sum;
                } else if (sum == minIndex)
                    ret.add(list2[i]);
            }
            if (i >= minIndex) break;  //reduce the number of for loops
        }
        return ret.toArray(new String[ret.size()]);
    }
```
