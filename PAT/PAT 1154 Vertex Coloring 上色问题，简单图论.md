# 原创：PAT 1154 Vertex Coloring 上色问题，简单图论

A **proper vertex coloring** is a labeling of the graph's vertices with colors such that no two vertices sharing the same edge have the same color. A coloring using at most k colors is called a (proper) **k-coloring**.

Now you are supposed to tell if a given coloring is a proper k-coloring.

### Input Specification:

Each input file contains one test case. For each case, the first line gives two positive integers N and M (both no more than 10​4​​), being the total numbers of vertices and edges, respectively. Then M lines follow, each describes an edge by giving the indices (from 0 to N−1) of the two ends of the edge.

After the graph, a positive integer K (≤ 100) is given, which is the number of colorings you are supposed to check. Then K lines follow, each contains N colors which are represented by non-negative integers in the range of **int**. The i-th color is the color of the i-th vertex.

### Output Specification:

For each coloring, print in a line `k-coloring` if it is a proper `k`-coloring for some positive `k`, or `No` if not.

### Sample Input:
10 11  
8 7  
6 8  
4 5  
8 4  
8 1  
1 2  
1 4  
9 8  
9 1  
1 0  
2 4  
4  
0 1 0 1 4 1 0 1 3 0  
0 1 0 1 4 1 0 1 0 0  
8 1 0 1 4 1 0 5 3 0  
1 2 3 4 5 6 7 8 8 9  
### Sample Output:
4-coloring  
No  
6-coloring  
No  
### 数据结构：

### vector&lt;vector&lt;int&gt; &gt;;(因为没有权值) **存边**

**vector&lt;int&gt; 存颜色**
```c++
#include<iostream>
#include<string>
#include<sstream>
#include<vector>
#include<algorithm>
#include<cmath>
#include<map>
using namespace std;
//11:50 图论 
 
 
int main()
{
	freopen("C:\\Users\\chenzhuo\\Desktop\\in.txt","r",stdin);
	int n,m;
	cin>>n>>m;
	vector<vector<int> >tmp(n);
	for(int i=0;i<m;i++)
	{
		int a,b;cin>>a>>b;
		tmp[a].push_back(b);	
	}
	int k;
	cin>>k;
	for(int i=0;i<k;i++)
	{
		vector<int> col(n);
		int flag=1;
		int num=0;//颜色数量 
		map<int,int> mp;
		for(int j=0;j<n;j++)
		{
			cin>>col[j];
			if(mp[col[j]]!=1)
			{
				num++;
				mp[col[j]]=1;
			}
			
		}
		for(int j=0;j<n;j++)//遍历n个顶点 
		{
			for(auto d:tmp[j])//对于每个顶点 
			{
				if(col[j]==col[d])
				{
					cout<<"No"<<endl;
					flag=0;
					break;
				}
			}
			if(flag==0)
			{
				break;
			} 
		}
		if(flag==1)//输出 
		{
			cout<<num<<"-coloring"<<endl;
		}
		
	}
	
}
```
 
