# 原创：PAT 1146 Topological Order (25 分) 拓扑验证

### Sample Input:
6 8
1 2
1 3
5 2
5 4
2 3
2 6
3 4
6 4
5
1 5 2 3 6 4
5 1 2 6 3 4
5 1 2 3 6 4
5 2 1 6 3 4
1 2 3 4 5 6
### Sample Output:

 3 4

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
 
//12:55 
 
int main()
{
	//freopen("C:\\Users\\chenzhuo\\Desktop\\in.txt", "r", stdin);
	int m,n;
	cin >> n >> m;
	vector<vector<int> > node(n + 1);
	vector<int> fron(n + 1,0);//前驱结点
	for (int i = 1;i <= m;i++){//建表
		int k1;cin >> k1;
		int k2;cin >> k2;
		node[k1].push_back(k2);
		fron[k2]++;//前驱加1
	}
 
	int num;
	cin >> num;
	int isf = 1;
	for (int i = 0;i < num;i++)
	{
		vector<int> fron1(fron);//拷贝前驱表
		vector<int>tmp(n);
		int key;
		for (int a = 0;a < n;a++){
			cin >> tmp[a];
		}
		int flag = 1;
		for (auto k : tmp) {
			if (fron1[k] > 0) {//还有前驱存在
				flag = 0;
				break;
			}
			for (auto j : node[k]) {
				fron1[j]--;
			}
		}
		if (!flag) {
			if (isf) {
				isf = 0;//现在开始不是第一个出现了
			}
			else cout <<" ";
			cout <<i;
		}
 
			
	}
 
 
 
 
}
```

