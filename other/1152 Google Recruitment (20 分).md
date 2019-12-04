# 原创：1152 Google Recruitment (20 分)

The natural constant e is a well known transcendental number（超越数）. The first several digits are: e = 2.71828182845904523536028747135266249775724709369995957496696762772407663035354759457138217852516642**7427466391**932003059921... where the 10 digits in bold are the answer to Google's question.

Now you are asked to solve a more general problem: find the first K-digit prime in consecutive digits of any given L-digit number.

### Input Specification:

Each input file contains one test case. Each case first gives in a line two positive integers: L (≤ 1,000) and K (&lt; 10), which are the numbers of digits of the given number and the prime to be found, respectively. Then the L-digit number N is given in the next line.

### Output Specification:

For each test case, print in a line the first K-digit prime in consecutive digits of N. If such a number does not exist, output `404` instead. Note: the leading zeroes must also be counted as part of the K digits. For example, to find the 4-digit prime in 200236, 0023 is a solution. However the first digit 2 must not be treated as a solution 0002 since the leading zeroes are not in the original number.

### Sample Input 1:

### Sample Output 1:

### Sample Input 2:

### Sample Output 2:

 
```c++
#include<iostream>
#include<string>
#include<sstream>
#include<vector>
#include<algorithm>
#include<cmath>
using namespace std;
//11:06
 
bool isp(int a)
{
	if(a<=1) return false;
	int k=pow(a,0.5);
	for(int i=2;i<k;i++)
	{
		if(a%i==0) return false;
	}
	return true;
}
int main()
{
	//freopen("C:\\Users\\chenzhuo\\Desktop\\in.txt","r",stdin);
	int n,m;
	cin>>n>>m;
	string s;
	cin>>s;
	for(int i=0;i<=n-m;i++)
	{
		string str=s.substr(i,m);
		stringstream ss;ss<<str;
		int tmp;
		ss>>tmp;
		if(isp(tmp))
		{
			cout<<str;
			return 0;
		}
	}
	cout<<"404";
	
	
}
```
