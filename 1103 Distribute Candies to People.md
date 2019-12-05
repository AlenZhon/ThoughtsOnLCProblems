# 1103. Distribute Candies to People

## 题目

给num_people个人分糖果，第一轮，第一个人1块，第二个人2块，第n个人n块；第二轮，第一个人n+1块，第二个人n+2块...当最后糖果不够的时候，把剩下所有的糖果全部分给那个人。

返回每个人分到的糖果数量，用一个数组表示。

>We distribute some number of candies, to a row of n = num_people people in the following way:
>
>We then give 1 candy to the first person, 2 candies to the second person, and so on until we give n candies to the last person.
>
>Then, we go back to the start of the row, giving n + 1 candies to the first person, n + 2 candies to the second person, and so on until we give 2 * n candies to the last person.
>
>This process repeats (with us giving one more candy each time, and moving to the start of the row after we reach the end) until we run out of candies.  The last person will receive all of our remaining candies (not necessarily one more than the previous gift).
>
>Return an array (of length num_people and sum candies) that represents the final distribution of candies.
>
>**Example 1:**
>
>>Input: candies = 7, num_people = 4  
>>Output: [1,2,3,1]  
>>Explanation:
>>On the first turn, ans[0] += 1, and the array is [1,0,0,0].  
>>On the second turn, ans[1] += 2, and the array is [1,2,0,0].  
>>On the third turn, ans[2] += 3, and the array is [1,2,3,0].  
>>On the fourth turn, ans[3] += 1 (because there is only one candy left), and the final array is [1,2,3,1].
>
>**Example 2:**
>
>>Input: candies = 10, num_people = 3  
>>Output: [5,2,3]  
>>Explanation:  
>>On the first turn, ans[0] += 1, and the array is [1,0,0].  
>>On the second turn, ans[1] += 2, and the array is [1,2,0].  
>>On the third turn, ans[2] += 3, and the array is [1,2,3].
>>On the fourth turn, ans[0] += 4, and the final array is [5,2,3].
>
>**Constraints:**
>
> - 1 <= candies <= 10^9
> - 1 <= num_people <= 1000

## 解法

能咋样，分呗hhh

```java
public int[] distributeCandies(int candies, int num_people) {
        int[] ret = new int[num_people];
        int toGive = 1, i = 0;
        while (candies > 0){
                if (toGive > candies) {
                    ret[i % num_people]+=candies;
                    candies = 0;
                    break;
                } else {
                    ret[i++]+= toGive;
                    candies-= toGive;
                    toGive++;
                    i %= num_people;
                }
        }
        return ret;
    }
```

另一种解法：

```java
public int[] distributeCandies(int candies, int n) {

        int[] ans = new int[n];
        int i = 0;
        int sum = 0;

        while(true){
            int t = ((int)Math.pow(n, 2) * i) + (n * (n + 1))/2;
            if(sum + t > candies) break;
            sum += t;
            i++;
        }

        i--;

        for(int j = 0; j < n; j++){
            ans[j] = (i + 1) * (j + 1) + (i * n * (i + 1))/2;
        }

        i++;
        // System.out.println(i + " " + candies + " " + sum);
        candies -= sum;
        int start = n * i + 1;
        int j = 0;
        while(candies >= start){
            ans[j] += start;
            candies -= start;
            start++;
            j++;
        }

        if(candies > 0) ans[j] += candies;

        return ans;

    }
```
