# 原创：PAT 1027 Colors in Mars (20 分)

People in Mars represent the colors in their computers in a similar way as the Earth people. That is, a color is represented by a 6-digit number, where the first 2 digits are for `Red`, the middle 2 digits for `Green`, and the last 2 digits for `Blue`. The only difference is that they use radix 13 (0-9 and A-C) instead of 16. Now given a color in three decimal numbers (each between 0 and 168), you are supposed to output their Mars RGB values.

### Input Specification:

Each input file contains one test case which occupies a line containing the three decimal color values.

### Output Specification:

For each test case you should output the Mars RGB value in the following format: first output `#`, then followed by a 6-digit number where all the English characters must be upper-cased. If a single color is only 1-digit long, you must print a `0` to its left.

### Sample Input:
1234567899

### Sample Output:
Yes
2469135798

```c++
#include<iostream>
#include<string>
#include<sstream>
#include<vector>
#include<algorithm>
#include<cmath>
using namespace std;
//9:38
 
int main()
{
	//freopen("C:\\Users\\chenzhuo\\Desktop\\in.txt","r",stdin);
	
	vector<int> tmp(10,0);
	vector<int> tmp1(10,0);
	string str1;
	cin>>str1;
	for(int i=0;i<str1.size();i++)
	{
		tmp[str1[i]-'0']++;
	}
	int jin=0;
	string str2="";
	for(int i=str1.size()-1;i>=0;i--)
	{
		int k=2*(str1[i]-'0')+jin;
		jin=0;
		if(k>=10)
		{
			k-=10;jin=1;
		}
		char c=k+'0';
		str2=c+str2;
	}
	if(jin==1)
	{
		str2='1'+str2;
	}
	for(int i=0;i<str2.size();i++)
	{
		tmp[str2[i]-'0']--;
	}
	if(tmp==tmp1) 
		cout<<"Yes"<<endl;
	else cout<<"No"<<endl;
	
	for(int i=0;i<str2.size();i++)
	{
		cout<<str2[i];
	}
}
```
 
