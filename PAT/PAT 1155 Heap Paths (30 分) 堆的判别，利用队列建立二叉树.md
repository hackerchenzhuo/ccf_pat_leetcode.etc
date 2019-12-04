# 原创：PAT 1155 Heap Paths (30 分) 堆的判别，利用队列建立二叉树

In computer science, a **heap** is a specialized tree-based data structure that satisfies the heap property: if P is a parent node of C, then the key (the value) of P is either greater than or equal to (in a max heap) or less than or equal to (in a min heap) the key of C. A common implementation of a heap is the binary heap, in which the tree is a complete binary tree. (Quoted from Wikipedia at [https://en.wikipedia.org/wiki/Heap_(data_structure](https://en.wikipedia.org/wiki/Heap_(data_structure)))

One thing for sure is that all the keys along any path from the root to a leaf in a max/min heap must be in non-increasing/non-decreasing order.

Your job is to check every path in a given complete binary tree, in order to tell if it is a heap or not.

### Input Specification:

Each input file contains one test case. For each case, the first line gives a positive integer N (1&lt;N≤1,000), the number of keys in the tree. Then the next line contains N distinct integer keys (all in the range of **int**), which gives the level order traversal sequence of a complete binary tree.

### Output Specification:

For each given tree, first print all the paths from the root to the leaves. Each path occupies a line, with all the numbers separated by a space, and no extra space at the beginning or the end of the line. The paths must be printed in the following order: for each node in the tree, all the paths in its right subtree must be printed before those in its left subtree.

Finally print in a line `Max Heap` if it is a max heap, or `Min Heap` for a min heap, or `Not Heap` if it is not a heap at all.

### Sample Input 1:
8  
98 72 86 60 65 12 23 50
### Sample Output 1:
98 86 23  
98 86 12  
98 72 65  
98 72 60 50  
Max Heap  
### Sample Input 2:
8  
8 38 25 58 52 82 70 60
### Sample Output 2:
8 25 70  
8 25 82  
8 38 52  
8 38 58 60  
Min Heap  
### Sample Input 3:
8  
10 28 15 12 34 9 8 56
### Sample Output 3:
10 15 8  
10 15 9  
10 28 34  
10 28 12 56  
Not Heap  
 
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
 
//12:20-13:30 堆的建立 
int mh=1;//是否大顶堆 
struct hep{
	int d;
	hep*l;
	hep*r;	
	hep(int x):d(x),l(NULL),r(NULL){
	}
};
 
void dfs(hep *root,vector<int> t)
{
	if(root==NULL) return;
	else if(!root->l&&!root->r)//到底了 
	{
		t.push_back(root->d);
		for(int i=0;i<t.size();i++)
		{
			cout<<t[i];
			if(i!=t.size()-1) cout<<" ";
		}
		cout<<endl;
		//判断是否大/小顶堆
		if(mh==1)
		{
			for(int i=0;i<t.size()-1;i++)
			{
				if(t[i]<t[i+1]) 
				{
					mh=0;
					break;
				}
			}
			
		} 
		else if(mh==2)
		{
			for(int i=0;i<t.size()-1;i++)
			{
				if(t[i]>t[i+1]) 
				{
					mh=0;
					break;
				}
			}
		}
		
		return; 
		 
	}
	else//没到底 
	{
		t.push_back(root->d);
		dfs(root->r,t);
		dfs(root->l,t);
	}
}
int main()
{
	freopen("C:\\Users\\chenzhuo\\Desktop\\in.txt","r",stdin);
	int n;
	cin>>n;
	vector<int> a(n);
	for(int i=0;i<n;i++)
	{
		cin>>a[i];
	}
	if(a[0]>a[n-1])
	{
		mh=1;//猜测大顶 
	}
	else mh=2;//猜测小 
	//层次遍历创建二叉树
	queue<hep*> q;
	hep *root=new hep(a[0]);
	q.push(root);
	//cout<<root->d;
	for(int i=1;i<n;)
	{
		hep *t=q.front();
		q.pop();//出队 
		hep *r1=new hep(a[i]);
		i++;
		t->l=r1;
		q.push(r1);//入 
		if(i>=n) break;
		hep *r2=new hep(a[i]);
		i++;
		t->r=r2;
		q.push(r2);
	}
//	hep *gg=root;
//	while(gg!=NULL)
//	{
//		cout<<gg->d<<" ";
//		gg=gg->r;
//	}cout<<endl;
	//此时二叉树已经构造完成
	//使用递归dfs进行遍历 
	vector<int> key;
	dfs(root,key);
	
	if(mh==1)
	{
		cout<<"Max Heap"<<endl;
	}
	else if(mh==2)
	{
		cout<<"Min Heap"<<endl;
	}
	else
	{
		cout<<"Not Heap"<<endl;
	}
	 
	
}
```