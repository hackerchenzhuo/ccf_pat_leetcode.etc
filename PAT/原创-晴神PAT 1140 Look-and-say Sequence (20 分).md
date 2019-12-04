# 原创：晴神PAT 1140 Look-and-say Sequence (20 分)

Look-and-say sequence is a sequence of integers as the following:

### Sample Input:

### Sample Output:

我的代码：

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
using namespace std;
 
//15:21
 
int main()
{
	freopen("C:\\Users\\chenzhuo\\Desktop\\in.txt", "r", stdin);
	string tmp = "";
	char c; cin >> c; tmp =tmp+ c;
	int n; cin >> n;
	for (int i = 1; i < n; i++)
	{
		//cout << 1;
		string tmp1="";
		char last = tmp[0];
		//cout << last;
		int sz = 0;
		for (int j = 0; j < tmp.size(); j++)
		{
			if (tmp[j] == last)
			{
				sz++;
			}
			else
			{
				tmp1 += last;
				last = tmp[j];
				char cc = '0'; cc += sz;
				tmp1 =tmp1+ cc;
				sz = 1;
			}
		}
		tmp1 += last;
		char cc = '0'; cc += sz; tmp1 = tmp1 + cc;
		tmp = tmp1;
		cout << tmp<<endl;
	}
	cout << tmp;
}
 
 
 ```

 

 

晴神代码优点：

循环不换行，显得紧密。

使用了函数 to_string 

两个for循环一次遍历。

```c++
#include <iostream>
using namespace std;
int main() {
    string s;
    int n, j;
    cin >> s >> n;
    for (int cnt = 1; cnt < n; cnt++) {
        string t;
        for (int i = 0; i < s.length(); i = j) {
            for (j = i; j < s.length() && s[j] == s[i]; j++);
            t += to_string((s[i] - '0') * 10 + j - i);
        }
        s = t;
    }
    cout << s;
    return 0;
}
``` 
