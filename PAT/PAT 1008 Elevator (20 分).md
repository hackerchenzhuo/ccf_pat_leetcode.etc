# 原创：PAT 1008 Elevator (20 分)

The highest building in our city has only one elevator. A request list is made up with N positive numbers. The numbers denote at which floors the elevator will stop, in specified order. It costs 6 seconds to move the elevator up one floor, and 4 seconds to move down one floor. The elevator will stay for 5 seconds at each stop.

For a given request list, you are to compute the total time spent to fulfill the requests on the list. The elevator is on the 0th floor at the beginning and does not have to return to the ground floor when the requests are fulfilled.

### Input Specification:

Each input file contains one test case. Each case contains a positive integer N, followed by N positive numbers. All the numbers in the input are less than 100.

### Output Specification:

For each test case, print the total time on a single line.

### Sample Input:
3 2 3 1

### Sample Output:
41
 
```c++
#include<iostream>
#include<string>
#include<sstream>
#include<vector>
using namespace std;
//6:33-6:45 
int main()
{
	freopen("C:\\Users\\chenzhuo\\Desktop\\in.txt","r",stdin);
	int num;cin>>num;
	vector<int> tmp(num);
	for(int i=0;i<num;i++)
	{
		cin>>tmp[i];
	}
	
	int now=0;
	int ans=0;
	for(int i=0;i<num;i++)
	{
		int tt=tmp[i]-now;
		if(tt>=0)
		{
			ans+=tt*6;
			ans+=5;
		}
		else if(tt<0)
		{
			ans+=tt*(-4);
			ans+=5;
		}
		now=tmp[i];
	}
	cout<<ans;
	return 0;
}
```