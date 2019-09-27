# 492. Construct the Rectangle

## 题目

给出一个正整数为矩形面积，返回构成这个矩形的长和宽，要求：1.长度必须大于宽度。2.长度和宽度均为正整数值。

>For a web developer, it is very important to know how to design a web page's size. So, given a specific rectangular web page’s area, your job by now is to design a rectangular web page, whose length L and width W satisfy the following requirements:
>
>1. The area of the rectangular web page you designed must equal to the given target area.
>2. The width W should not be larger than the length L, which means L >= W.
>3. The difference between length L and width W should be as small as possible.
>
>You need to output the length L and the width W of the web page you designed in sequence.
>
>**Example:**
>
>>Input: 4  
>>Output: [2, 2]  
>>Explanation: The target area is 4, and all the possible ways to construct it are [1,4], [2,2], [4,1].  
>>But according to requirement 2, [1,4] is illegal; according to requirement 3,  [4,1] is not optimal compared to [2,2]. So the length L is 2, and the width W is 2.
>
>**Note:**
>
> - The given area won't exceed 10,000,000 and is a positive integer
> - The web page's width and length you designed must be positive integers.

## 解法

肯定是从area的平方根开始遍历了。这里有一个trick可以减少遍历次数，就是将`width--`而非`length++`。因为当大于4时，N的平方根就要小于 N/2了，尤其是N越大，则`length++`要遍历的次数`N-sqrt(N)`就会显著大于`sqrt(N)`。

>The `Math.sqrt(N)` is far more less then `N/2`: `sqrt(N) << N/2`. (By solving the equation `sqrt(N) = N/2` you can easily find out only when N is in `[0, 4]`, `sqrt(N)` will large or equal to `N/2`). So if you increase the `sqrt(N)` to get the solution you need to step around `N - sqrt(N)` times. If you decrease it, the step you need is only around `sqrt(N)`. Here we got: `N - sqrt(N) = 2 * N/2 - sqrt(N) >> 2 * sqrt(N) - sqrt(N) = sqrt(N)`. So, decreasing the `sqrt(N)` takes less time.

（一开始没想明白就敲上去了，结果运行时间50ms）

```java
public int[] constructRectangle(int area) {
        int[] res = new int[2];
        for (int i = (int)Math.sqrt(area); i>=1; i-- ){
            if (area % i == 0) {
                res[0] = area / i;
                res[1] = i;
                return res;
            }
        }
        return res;
    }
```
