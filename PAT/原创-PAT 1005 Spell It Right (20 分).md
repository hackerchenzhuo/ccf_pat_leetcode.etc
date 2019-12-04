# 原创：PAT 1005 Spell It Right (20 分)

Given a non-negative integer N, your task is to compute the sum of all the digits of N, and output every digit of the sum in English.

### Input Specification:

Each input file contains one test case. Each case occupies one line which contains an N (≤10​100​​).

### Output Specification:

For each test case, output in one line the digits of the sum in English words. There must be one space between two consecutive words, but no extra space at the end of a line.

### Sample Input:
12345

### Sample Output:
one five
 
```c++
#include<iostream>
#include<string>
#include<sstream>
#include<vector>
using namespace std;
//6:10-6:24
int main()
{
	//freopen("C:\\Users\\chenzhuo\\Desktop\\in.txt","r",stdin);
	
	string c;
	cin>>c;
	int ans=0;
	for(int i=0;i<c.size();i++)
	{
		ans+=(c[i]-'0');
	}
	string str;
	stringstream ss;
	ss<<ans;
	ss>>str;
	string tmp[]={"zero","one","two","three","four","five","six","seven","eight","nine","ten"};
	for(int i=0;i<str.size();i++)
	{
		cout<<tmp[str[i]-'0'];
		if(i!=str.size()-1) cout<<" ";
	}
	return 0;
}
```