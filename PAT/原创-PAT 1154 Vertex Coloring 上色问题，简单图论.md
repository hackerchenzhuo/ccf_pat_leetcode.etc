# 原创：PAT 1154 Vertex Coloring 上色问题，简单图论

A **proper vertex coloring** is a labeling of the graph's vertices with colors such that no two vertices sharing the same edge have the same color. A coloring using at most k colors is called a (proper) **k-coloring**.

Now you are supposed to tell if a given coloring is a proper k-coloring.

### Input Specification:

Each input file contains one test case. For each case, the first line gives two positive integers N and M (both no more than 10​4​​), being the total numbers of vertices and edges, respectively. Then M lines follow, each describes an edge by giving the indices (from 0 to N−1) of the two ends of the edge.

After the graph, a positive integer K (≤ 100) is given, which is the number of colorings you are supposed to check. Then K lines follow, each contains N colors which are represented by non-negative integers in the range of **int**. The i-th color is the color of the i-th vertex.

### Output Specification:

For each coloring, print in a line `k-coloring` if it is a proper `k`-coloring for some positive `k`, or `No` if not.

### Sample Input:

### Sample Output:

### 数据结构：

### vector&lt;vector&lt;int&gt; &gt;;(因为没有权值) **存边**

**vector&lt;int&gt; 存颜色**

 
