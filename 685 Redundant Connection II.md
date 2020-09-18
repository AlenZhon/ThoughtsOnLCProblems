# 685. Redundant Connection II

## 题目

在本问题中，有根树指满足以下条件的有向图。该树只有一个根节点，所有其他节点都是该根节点的后继。每一个节点只有一个父节点，除了根节点没有父节点。

输入一个有向图，该图由一个有着N个节点 (节点值不重复1, 2, ..., N) 的树及一条附加的边构成。附加的边的两个顶点包含在1到N中间，这条附加的边不属于树中已存在的边。

结果图是一个以边组成的二维数组。 每一个边 的元素是一对 [u, v]，用以表示有向图中连接顶点 u 和顶点 v 的边，其中 u 是 v 的一个父节点。

返回一条能删除的边，使得剩下的图是有N个节点的有根树。若有多个答案，返回最后出现在给定二维数组的答案。
```java
示例 1:

输入: [[1,2], [1,3], [2,3]]
输出: [2,3]
解释: 给定的有向图如下:
  1
 / \
v   v
2-->3

示例 2:

输入: [[1,2], [2,3], [3,4], [4,1], [1,5]]
输出: [4,1]
解释: 给定的有向图如下:
5 <- 1 -> 2
     ^    |
     |    v
     4 <- 3
```

注意:

- 二维数组大小的在3到1000范围内。
- 二维数组中的每个整数在1到N之间，其中 N 是二维数组的大小。


## 解法

[官方题解](https://leetcode-cn.com/problems/redundant-connection-ii/solution/rong-yu-lian-jie-ii-by-leetcode-solution/)

并查集的思路。时间复杂度：O(Nlog⁡N)，其中 N 是图中的节点个数。需要遍历图中的 N 条边，对于每条边，需要对两个节点查找祖先，如果两个节点的祖先不同则需要进行合并，需要进行 2 次查找和最多 1 次合并。一共需要进行 2N 次查找和最多 N 次合并，因此总时间复杂度是 O(2Nlog⁡N)=O(Nlog⁡N)。这里的并查集使用了路径压缩，但是没有使用按秩合并，最坏情况下的时间复杂度是 O(Nlog⁡N)，平均情况下的时间复杂度依然是 O(Nα(N))，其中 α 为阿克曼函数的反函数，α(N) 可以认为是一个很小的常数。

空间复杂度：O(N)，其中 N 是图中的节点个数。使用数组 `parent` 记录每个节点的父节点，并查集使用数组记录每个节点的祖先。

思路是从边的关系入手。根据题意，树的边数必定是节点数 N-1。现在有N条边，说明可能有两种情况：
- 新加的边指向根节点，那么有向图成环了。
- 新加的边指向非根节点，那么有可能成环，也有可能不成环（因为是有向图要考虑环的方向）。此时被指向的节点有两个父节点。

所以遍历所有边建立树，寻找导致冲突的边和环路出现的边。

```java
class Solution {
    public int[] findRedundantDirectedConnection(int[][] edges) {
        int count = edges.length;
        UnionFind uf = new UnionFind(count + 1);
        int[] parent = new int[count + 1];
        for (int i = 1; i<= count; i++){
            parent[i] = i;
        }

        int conflictIndex = -1, cycleIndex = -1;
        for (int i = 0; i < count; i++){
            int[] edge = edges[i];
            int node0 = edge[0], node1 = edge[1];
            if (parent[node1] != node1){
                conflictIndex = i;
            } else {
                parent[node1] = node0;
                if (uf.find(node0) == uf.find(node1)){
                    cycleIndex = i; 
                } else {
                    uf.union(node0, node1);
                }
            }
        }
        if (conflictIndex < 0){
            return edges[cycleIndex];
        } else {
            int[] conflictEdge = edges[conflictIndex];
            if (cycleIndex>=0){
                return new int[]{parent[conflictEdge[1]], conflictEdge[1]};
            } else {
                return conflictEdge;
            }
        }
    }
}

class UnionFind{
    int[] ancestor;

    public UnionFind(int n){
        ancestor = new int[n];
        for (int i = 0; i< n; i++){
            ancestor[i] = i;
        }
    }

    public void union(int index1, int index2){
        ancestor[find(index1)] = find(index2);
    }
    public int find(int index){
        if (ancestor[index] != index){
            ancestor[index] = find(ancestor[index]);
        }
        return ancestor[index];
    }
}
```

使用数组 parent 记录每个节点的父节点，初始时对于任何 1≤i≤N 都有 parent[i]=i，另外创建并查集，初始时并查集中的每个节点都是一个连通分支，该连通分支的根节点就是该节点本身。遍历每条边的过程中，维护导致冲突的边和导致环路出现的边，由于只有一条附加的边，因此最多有一条导致冲突的边和一条导致环路出现的边。

当访问到边 [u,v] 时，进行如下操作：

    如果此时已经有 parent[v]≠v，说明 v 有两个父节点，将当前的边 [u,v] 记为导致冲突的边；

    否则，令 parent[v]=u，然后在并查集中分别找到 u 和 v 的祖先（即各自的连通分支中的根节点），如果祖先相同，说明这条边导致环路出现，将当前的边 [u,v] 记为导致环路出现的边，如果祖先不同，则在并查集中将 u 和 v 进行合并。

根据上述操作，同一条边不可能同时被记为导致冲突的边和导致环路出现的边。如果访问到的边确实同时导致冲突和环路出现，则这条边被记为导致冲突的边。

在遍历图中的所有边之后，根据是否存在导致冲突的边和导致环路出现的边，得到附加的边。

如果没有导致冲突的边，说明附加的边一定导致环路出现，而且是在环路中的最后一条被访问到的边，因此附加的边即为导致环路出现的边。

如果有导致冲突的边，记这条边为 [u,v]，则有两条边指向 v，另一条边为 [parent[v],v]，需要通过判断是否有导致环路的边决定哪条边是附加的边。

- 如果有导致环路的边，则附加的边不可能是 [u,v]（因为 [u,v]已经被记为导致冲突的边，不可能被记为导致环路出现的边），因此附加的边是 [parent[v],v]。

- 如果没有导致环路的边，则附加的边是后被访问到的指向 v 的边，因此附加的边是 [u,v]。
