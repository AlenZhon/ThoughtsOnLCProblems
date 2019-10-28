# 686. Repeated String Match

## 题目

给定两个字符串A, B，问最少要将A重复拼接几次，才能使得B是拼接后字符串的子串。如果找不到这样的k则返回-1。

>Given two strings A and B, find the minimum number of times A has to be repeated such that B is a substring of it. If no such solution, return -1.
>
>For example, with A = `"abcd"` and B = `"cdabcdab"`.
>
>Return 3, because by repeating A three times (`“abcdabcdabcd”`), B is a substring of it; and B is not a substring of A repeated two times (`"abcdabcd"`).
>
>Note:
>
> - The length of A and B will be between 1 and 10000.

## 解法

首先，如果B要是子串，则拼接后的A长度肯定要不小于B，先假设重复了`i`次后 `len(A * i) >= len(B)`。那么我们只需要判断当拼接了`i`次和`(i+1)`次的时候，B是否是子串即可。因为`(i+1)`次时已经可以包含了所有B可能出现的组合。 `A[i:i+len(B)] == B for i = 0, 1, ..., len(A) - 1`

```java
public int repeatedStringMatch(String A, String B) {
        StringBuilder sb = new StringBuilder();
        int lenb = B.length(), i = 0;
        while (sb.length() < lenb) {
            sb.append(A);
            i++;
        }
        if (sb.indexOf(B) >= 0) return i;
        if (sb.append(A).indexOf(B) >=0 ) return i+1;
        return -1;
    }
```

时间复杂度是 O(N * (M+N))，M和N分别是AB的长度。
>We create two strings `A * i, A * (i+1)` which have length at most `O(M+N)`. When checking whether B is a substring of A, this check takes naively the product of their lengths.

空间复杂度是 O(M + N)。

### 方法2:  Rabin-Karp (Rolling Hash)

由前一种方法中检验B是不是`A * i`字符串的子串而启发。寻找方法使得时间复杂度降到`O(A * i)`。

使用哈希函数手动计算每添加一个字符的哈希值。根据哈希值判断两个字符串是否相等。

>**Algorithm**
>
> For strings S, consider each S[i] as some integer ASCII code. Then for some prime p, consider the following function modulo some prime modulus `M`:
>
>`hash(S) = \sum_{0 <= i < len(S)} p^i * S[i]`
>
Notably, `hash(S[1:] + x) = (hash(S) - S[0]))/ p + p^{n-1} * x`. This shows we can get the hash of every substring of `A * q` in time complexity linear to it's size. (We will also use the fact that `p^(−1) =p^(M−2) mod  M`.)

However, hashes may collide haphazardly. To be absolutely sure in theory, we should check the answer in the usual way. The expected number of checks we make is in the order of `1+s/M`​ where s is the number of substrings we computed hashes for (assuming the hashes are equally distributed), which is effectively 1.

```java
import java.math.BigInteger;

class Solution {
    public boolean check(int index, String A, String B) {
        for (int i = 0; i < B.length(); i++) {
            if (A.charAt((i + index) % A.length()) != B.charAt(i)) {
                return false;
            }
        }
        return true;
    }
    public int repeatedStringMatch(String A, String B) {
        int q = (B.length() - 1) / A.length() + 1;
        int p = 113, MOD = 1_000_000_007;
        int pInv = BigInteger.valueOf(p).modInverse(BigInteger.valueOf(MOD)).intValue();

        long bHash = 0, power = 1;
        for (int i = 0; i < B.length(); i++) {
            bHash += power * B.codePointAt(i);
            bHash %= MOD;
            power = (power * p) % MOD;
        }

        long aHash = 0; power = 1;
        for (int i = 0; i < B.length(); i++) {
            aHash += power * A.codePointAt(i % A.length());
            aHash %= MOD;
            power = (power * p) % MOD;
        }

        if (aHash == bHash && check(0, A, B)) return q;
        power = (power * pInv) % MOD;

        for (int i = B.length(); i < (q + 1) * A.length(); i++) {
            aHash -= A.codePointAt((i - B.length()) % A.length());
            aHash *= pInv;
            aHash += power * A.codePointAt(i % A.length());
            aHash %= MOD;
            if (aHash == bHash && check(i - B.length() + 1, A, B)) {
                return i < q * A.length() ? q : q + 1;
            }
        }
        return -1;
    }
}
```

>**Time Complexity:** O(M+N) (at these sizes), where `M,N` are the lengths of strings A, B. As in Approach #1, we justify that A * (q+1) will be of length `O(M + N)`, and computing the rolling hashes was linear work. We will also do a linear `O(N)` final check of our answer `1 + O(M) / \mathcal{M}` times.  
>**Space complexity:** `O(1)`. Only integers were stored with additional memory.
