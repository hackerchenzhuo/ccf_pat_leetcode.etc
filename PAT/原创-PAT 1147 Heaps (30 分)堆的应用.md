# 原创：PAT 1147 Heaps (30 分)堆的应用

In computer science, a **heap** is a specialized tree-based data structure that satisfies the heap property: if P is a parent node of C, then the key (the value) of P is either greater than or equal to (in a max heap) or less than or equal to (in a min heap) the key of C. A common implementation of a heap is the binary heap, in which the tree is a complete binary tree. (Quoted from Wikipedia at [https://en.wikipedia.org/wiki/Heap_(data_structure](https://en.wikipedia.org/wiki/Heap_(data_structure)))

Your job is to tell if a given complete binary tree is a heap.

### Input Specification:

Each input file contains one test case. For each case, the first line gives two positive integers: M (≤ 100), the number of trees to be tested; and N (1 &lt; N ≤ 1,000), the number of keys in each tree, respectively. Then M lines follow, each contains N distinct integer keys (all in the range of **int**), which gives the level order traversal sequence of a complete binary tree.

### Output Specification:

For each given tree, print in a line `Max Heap` if it is a max heap, or `Min Heap` for a min heap, or `Not Heap` if it is not a heap at all. Then in the next line print the tree's postorder traversal sequence. All the numbers are separated by a space, and there must no extra space at the beginning or the end of the line.

### Sample Input:
3 8  
98 72 86 60 65 12 23 50  
8 38 25 58 52 82 70 60  
10 28 15 12 34 9 8 56  
### Sample Output:
Max Heap  
50 60 65 72 12 23 86 98  
Min Heap  
60 58 52 38 82 70 25 8  
Not Heap  
56 12 34 28 9 8 15 10  

```c++
#include<iostream>
#include<string>
#include<sstream>
#include<vector>
#include<algorithm>
#include<cmath>
#include<map>
#include<queue>
using namespace std;
 
//15.42-16.30 又是堆
 
bool judge(int a, vector<int>& tree,int& m,int &jd)//1->max 2->min 3->not 0->到底了 jd->预判
{
	if (2 * a + 2 >= m) {
		if (2 * a + 1 >= m) {
			return 1;//最后一个了
		}
		else {
			if (tree[a] >= tree[2 * a + 1] && jd == 1 || tree[a] <= tree[2 * a + 1] && jd == 2)
			{
				return 1;
			}
			else return 0;
		}
	}
	else
	{
		return judge(2 * a + 1, tree, m, jd) && judge(2 * a + 2, tree, m, jd) && (tree[a] >= tree[2 * a + 1] && jd == 1 || tree[a] <= tree[2 * a + 1] && jd == 2) && (tree[a] >= tree[2 * a + 2] && jd == 1 || tree[a] <= tree[2 * a + 2] && jd == 2);
	}
}
void vis(int a, vector<int> &tree,int &m)
{
	if (a >= m) return;
	vis(2 * a + 1, tree, m);
	vis(2 * a + 2, tree, m);
	cout << tree[a];
	if (a != 0) cout << " ";
}
 
int main()
{
	freopen("C:\\Users\\chenzhuo\\Desktop\\in.txt", "r", stdin);
	
	int n, m;cin >> n >> m;
	vector<vector<int> > tree(n,vector<int>(m));
	for (int i = 0;i < n;i++)
	{
		for (int j = 0;j < m;j++)
		{
			cin >> tree[i][j];
		}
	}
 
 
	for (int i = 0;i < n;i++)
	{
		int jd;
		if (tree[i][0] >= tree[i][m - 1]) jd = 1;//mx
		else jd = 2;
		bool jud = judge(0, tree[i], m,jd);
		if (jud&&jd==1) {
			cout << "Max Heap" << endl;
		}
		else if (jud && jd == 2) {
			cout << "Min Heap" << endl;
		}
		else{
			cout << "Not Heap" << endl;
		}
 
		vis(0, tree[i], m);
		cout << endl;
	}
	return 0;
}
```
 
