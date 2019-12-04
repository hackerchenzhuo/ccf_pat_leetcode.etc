# 原创：PAT 1132 Cut Integer (20 分)

Cutting an integer means to cut a K digits lone integer Z into two integers of (K/2) digits long integers A and B. For example, after cutting Z = 167334, we have A = 167 and B = 334. It is interesting to see that Z can be devided by the product of A and B, as 167334 / (167 × 334) = 3. Given an integer Z, you are supposed to test if it is such an integer.

### Input Specification:

Each input file contains one test case. For each case, the first line gives a positive integer N (≤ 20). Then N lines follow, each gives an integer Z (10 ≤ Z &lt;2​31​​). It is guaranteed that the number of digits of Z is an even number.

### Output Specification:

For each case, print a single line `Yes` if it is such a number, or `No` if not.

### Sample Input:
3  
167334  
2333  
12345678  
### Sample Output:
Yes  
No  
No  

```c++
#include<iostream>
#include<string>
#include<sstream>
#include<vector>
#include<algorithm>
#include<cmath>
#include<map>
#include<queue>
#include<unordered_map>
#include<set>
using namespace std;
 
//16.50-17:10 使用set
bool jud(int a)
{
	stringstream ss,ss1,ss2;
	ss << a;
	string str;
	ss >> str;
	string s1, s2;
	s1 = str.substr(0, int(str.size() / 2));
	s2= str.substr(int(str.size() / 2));
	int a1, a2;
	ss1 << s1;ss1 >> a1;
	ss2 << s2;ss2 >> a2;
	if (a1 == 0 || a2 == 0) return false;
	if (a % (a1 * a2) == 0) return true;
	return false;
}
int main()
{
	freopen("C:\\Users\\chenzhuo\\Desktop\\in.txt", "r", stdin);
	
	int n;
	cin >> n;
	for (int i = 0;i < n;i++)
	{
		int tmp;
		cin >> tmp;
		if(jud(tmp)) cout<<"Yes"<<endl;
		else cout<<"No"<<endl;
	}
}
```
 
