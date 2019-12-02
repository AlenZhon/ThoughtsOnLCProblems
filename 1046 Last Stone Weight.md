# 1046. Last Stone Weight

## 题目

用一个数组存储一堆石头中每一块的重量。对石头堆进行一系列操作，每次操作选目前石头堆里**最重的**两块石头相撞，假设两块石头分别为x, y并且 x <=y。

- 如果 x == y， 那么两块石头完全粉碎，一点重量都没有。
- 如果 x < y，那么x被完全粉碎，y剩下的重量是y - x。

对这堆石头反复进行操作，返回最后剩下的石头重量。如果最后一块石头都不剩就返回0。

>We have a collection of rocks, each rock has a positive integer weight.
>
>Each turn, we choose the **two heaviest** rocks and smash them together.  Suppose the stones have weights x and y with x <= y.  The result of this smash is:
>
> - If x == y, both stones are totally destroyed;
> - If x != y, the stone of weight x is totally destroyed, and the stone of weight y has new weight y-x.
>
>At the end, there is at most 1 stone left.  Return the weight of this stone (or 0 if there are no stones left.)
>
> **Example 1:**
>
>>Input: `[2,7,4,1,8,1]`  
>>Output: 1  
>>Explanation:  
>>We combine 7 and 8 to get 1 so the array converts to `[2,4,1,1,1]` then,
>>we combine 2 and 4 to get 2 so the array converts to `[2,1,1,1]` then,
>>we combine 2 and 1 to get 1 so the array converts to `[1,1,1]` then,
>>we combine 1 and 1 to get 0 so the array converts to `[1]` then that's the value of last stone.
>
>**Note:**
>
> - 1 <= stones.length <= 30
> - 1 <= stones[i] <= 1000

## 解法

没啥想法，所以先sort一下，然后从最后两个元素开始进行操作，每一步操作完了做个排序。考虑到每一步排序之后都是有序的，可使用插入排序。

```java
public int lastStoneWeight(int[] stones) {
        Arrays.sort(stones);
        for (int i = stones.length - 1; i >= 1; i--){
            if (stones[i] == stones[i - 1]){
                stones[i] = 0;
                stones[i-1] = 0;
                i --;
            } else {
                stones[i - 1] = stones[i] - stones[i - 1];
                mySort(stones, i - 1);
            }
        }
        return stones[0];
    }
    private void mySort(int[] array, int index){
        int insertVal = array[index], i = index - 1;
        for (; i>=0 && array[i] > insertVal; i--)
            array[i + 1] = array[i];
        array[i + 1] = insertVal;
    }
```
