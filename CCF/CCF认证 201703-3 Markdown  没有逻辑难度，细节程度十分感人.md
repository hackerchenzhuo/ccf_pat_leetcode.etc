# 原创：CCF认证 201703-3 Markdown  没有逻辑难度，细节程度十分感人

> 
<h2>**作为一个巨恶心的模拟题，这个题目让我在逻辑清醒的情况下足足写了2个小时。。。中途还顺便吃了个饭。。**</h2>

![](https://img-blog.csdnimg.cn/20190313200648966.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9jaGVuemh1by5ibG9nLmNzZG4ubmV0,size_16,color_FFFFFF,t_70)

**不过说到底，其实该题的难度并不大，最为一个大模拟，其难度主要就是堆代码而已，只要保持清醒就行。下面上题目。**

**（小声bb：期间两次运行错误原因主要是因为忘记把**//freopen("C:\\Users\\dell\\Desktop\\in.txt","r",stdin);****删掉了，所以考试的时候一定不要粗心！！！！！！！！！！！！**）**
![](https://img-blog.csdnimg.cn/20190313200947703.png)
![](https://img-blog.csdnimg.cn/20190313200947703.png)
![](https://img-blog.csdnimg.cn/20190313200947703.png)  
**第一次错误的原因是因为无序列表忘记去 * 了，也是属于粗心错误。**

 

问题描述

　　Markdown 是一种很流行的轻量级标记语言（lightweight markup language），广泛用于撰写带格式的文档。例如以下这段文本就是用 Markdown 的语法写成的： 


<br/><img alt="" height="272" src="http://118.190.20.162/RequireFile.do?fid=Yy7nr9Yt" width="493"/><br/><br/><br/>
　　这些用 Markdown 写成的文本，尽管本身是纯文本格式，然而读者可以很容易地看出它的文档结构。同时，还有很多工具可以自动把 Markdown 文本转换成 HTML 甚至 Word、PDF 等格式，取得更好的排版效果。例如上面这段文本通过转化得到的 HTML 代码如下所示：


<br/><img alt="" height="335" src="http://118.190.20.162/RequireFile.do?fid=247472gj" width="542"/><br/><br/><br/>
　　本题要求由你来编写一个 Markdown 的转换工具，完成 Markdown 文本到 HTML 代码的转换工作。简化起见，本题定义的 Markdown 语法规则和转换规则描述如下：

> 
<p><br/>
　　●**区块**：区块是文档的顶级结构。本题的 Markdown 语法有 3 种区块格式。在输入中，相邻两个区块之间用一个或多个空行分隔。**输出时删除所有分隔区块的空行。**<br/>
　　○段落：一般情况下，连续多行输入构成一个段落。段落的转换规则是在段落的第一行行首插入 `&lt;p&gt;`，在最后一行行末插入 `&lt;/p&gt;`。<br/>
　　○标题：每个标题区块只有一行，由若干个 `#` 开头，接着一个或多个空格，然后是标题内容，直到行末。`#` 的个数决定了标题的等级。转换时，`# Heading` 转换为 `&lt;h1&gt;Heading&lt;/h1&gt;`，`## Heading` 转换为 `&lt;h2&gt;Heading&lt;/h2&gt;`，以此类推。标题等级最深为 6。<br/>
　　○无序列表：无序列表由若干行组成，每行由 `*` 开头，接着一个或多个空格，然后是列表项目的文字，直到行末。转换时，在最开始插入一行 `&lt;ul&gt;`，最后插入一行 `&lt;/ul&gt;`；对于每行，`* Item` 转换为 `&lt;li&gt;Item&lt;/li&gt;`。本题中的无序列表只有一层，不会出现缩进的情况。</p>


 

> 
<p><br/>
　　●行内：对于区块中的内容，有以下两种行内结构。<br/>
　　○强调：`_Text_` 转换为 `&lt;em&gt;Text&lt;/em&gt;`。强调不会出现嵌套，每行中 `_` 的个数一定是偶数，且不会连续相邻。注意 `_Text_` 的前后不一定是空格字符。<br/>
　　○超级链接：`[Text](Link)` 转换为 `&lt;a href="Link"&gt;Text&lt;/a&gt;`。超级链接和强调可以相互嵌套，但每种格式不会超过一层。</p>


 

输入格式

　　输入由若干行组成，表示一个用本题规定的 Markdown 语法撰写的文档。

输出格式

　　输出由若干行组成，表示输入的 Markdown 文档转换成产生的 HTML 代码。

> 
样例输入
<p># Hello<br/><br/>
Hello, world!</p>
样例输出
<p>&lt;h1&gt;Hello&lt;/h1&gt;<br/>
&lt;p&gt;Hello, world!&lt;/p&gt;</p>


评测用例规模与约定

　　本题的测试点满足以下条件：<br/>
　　●本题每个测试点的输入数据所包含的行数都不超过100，每行字符的个数（包括行末换行符）都不超过100。<br/>
　　●除了换行符之外，所有字符都是 ASCII 码 32 至 126 的可打印字符。<br/>
　　●每行行首和行末都不会出现空格字符。<br/>
　　●输入数据除了 Markdown 语法所需，内容中不会出现 `#`、`*`、`_`、`[`、`]`、`(`、`)`、`&lt;`、`&gt;`、`&amp;` 这些字符。<br/>
　　●所有测试点均符合题目所规定的 Markdown 语法，你的程序不需要考虑语法错误的情况。<br/>
　　每个测试点包含的语法规则如下表所示，其中“√”表示包含，“×”表示不包含。
|测试点编号|段落|标题|无序列表|强调|超级链接
-|-|-|-|-|-
|1|√|×|×|×|×
|2|√|√|×|×|×
|3|√|×|√|×|×
|4|√|×|×|√|×
|5|√|×|×|×|√
|6|√|√|√|×|×
|7|√|×|×|√|√
|8|√|√|×|√|×
|9|√|×|√|×|√
|10|√|√|√|√|√

提示

　　由于本题要将输入数据当做一个文本文件来处理，要逐行读取直到文件结束，C/C++、Java 语言的用户可以参考以下代码片段来读取输入内容。<br/><img alt="" height="212" src="http://118.190.20.162/RequireFile.do?fid=LefmbYJb" width="536"/><br/><img alt="" height="250" src="http://118.190.20.162/RequireFile.do?fid=f29h8dt2" width="538"/><br/><img alt="" height="266" src="http://118.190.20.162/RequireFile.do?fid=DQedF9g6" width="536"/>

 

# 解题思路：

**自顶向下，逐步分解的思想，先宏观再微观。**

先把几个需要写的函数写出了，再在主函数main中依次调用。同时对于：强调函数，超链接函数这种最底层的，一定要细心。对于标题，列表，段落，这种区块函数，在写的过程中每次都要记得调用到行内函数（强调函数，超链接函数），灵活使用**substr**进行字符串处理，在函数内直接输出。

下面给出代码（PS: 不要被长度吓到了，因为本人for循环的括号喜欢单独占行，实际代码长度大概150行）。

 
![](//17.18-18.30  19.05-19.50
//201703-3 Markdown
#include<iostream>
#include<cstring>
#include<vector>
#include<algorithm>
using namespace std;
vector<string> md;
void emp(string &str)//找强调 
{
	string temp1= "<em>";
	//cout<<temp1<<endl;
	string temp2="</em>";
	for(int i=0;i<str.size();i++)
	{
		if(str[i]=='_')
		{
			int j;
			for(j=i+1;j<str.size();j++)
			{
				if(str[j]=='_')
					break;
			}
			string t1,t2,t3;
			t1=str.substr(0,i);
			t2=str.substr(i+1,j-i-1);
			t3="";
			if(j!=str.size())
				t3=str.substr(j+1);
			str=t1+temp1+t2+temp2+t3;	
		}
	}
}
void link(string &str)//链接  [Text](Link) 转换为 <a href="Link">Text</a>
{
	string temp1= "<a href=\"";
	//cout<<temp1<<endl;
	string temp2="\">";
	string temp3="</a>";
	for(int i=0;i<str.size();i++)
	{
		if(str[i]=='[')
		{
			int j,k,r;
			for(j=i+1;j<str.size();j++)
			{
				if(str[j]==']')
					break;
			}
			for(k=j+1;k<str.size();k++)
			{
				if(str[k]=='(')
					break;
			}
			for(r=k+1;r<str.size();r++)
			{
				if(str[r]==')')
					break;
			}
			string t1,t2,t3,tex,lin;
			t1=str.substr(0,i);//前面 
			tex=str.substr(i+1,j-i-1);
			lin=str.substr(k+1,r-k-1);
			t3="";
			if(r!=str.size())
				t3=str.substr(r+1);
			str=t1+temp1+lin+temp2+tex+temp3+t3;	
		}
	}
} 
 
void dealt()//标题处理 
{
	//cout<<"t"<<endl;
	int num=0;;
	int i;
	emp(md[0]);
	link(md[0]);
	//cout<<md[0]<<endl;
	for(i=0;i<md[0].size();i++)
	{
		if(md[0][i]=='#')
			num++;
		else 
			break;
	}
	//cout<<num<<endl;
	i=num+1;//定位到字符串。
	for(int d=i;d<md[0].size();d++)
	{
		if(md[0][d]!=' ')
		{
			md[0]=md[0].substr(d);
			break;
		}
	}
	string s="";
	char a='0'+num;
	
	string temp1= "<h";
	temp1=temp1+a+'>';
	//cout<<temp1<<endl;
	string temp2="</h";
	temp2=temp2+a+'>';
	s=s+temp1+md[0]+temp2;
	cout<<s<<endl;
}
 
void deals()//段落处理 
{
	for(int i=0;i<md.size();i++)
	{
		emp(md[i]);
		link(md[i]);
		if(i==0)
		{
			md[i]="<p>"+md[i];
		}	
		if(i==(md.size()-1))
		{
			md[i]+="</p>";
		}
		cout<<md[i]<<endl;
	}
	
}
void deall()//列表处理 
{
	cout<<"<ul>"<<endl;
	for(int i=0;i<md.size();i++)
	{
		md[i]=md[i].substr(2);
		for(int d=0;d<md[i].size();d++)
		{
			if(md[i][d]!=' ')
			{
				md[i]=md[i].substr(d);
				break;
			}
		}
		emp(md[i]);
		link(md[i]);
		md[i]="<li>"+md[i]+"</li>";	
		cout<<md[i]<<endl;
	}
	cout<<"</ul>"<<endl;
}
int main()
{
	//freopen("C:\\Users\\dell\\Desktop\\in.txt","r",stdin);
	string str;
	int title;//1->标题。0->不是标题 
	while(getline(cin,str))
	{		
		if(str!="")//未到空行 
			{
				md.push_back(str);
				continue;
			}
		else//到空行了 ,一个块输入结束 
		{
			if(md[0][0]=='#') 
				title=1;
			else title=0;			
		}
		if(title)
		{
			dealt();
		}
		else
		{
			if(md[0][0]=='*')//////////列表处理 
				deall();
			else 
				deals();//段落处理 
		}
		md.clear();
	}
	//////最后一轮处理 
	if(md[0][0]=='#') 
		title=1;
	else title=0;
	if(title)
	{
		dealt();//标题处理 
	}
	else
	{
		if(md[0][0]=='*')//////////列表处理 
			deall();
		else 
			deals();//段落处理 
	}
	return 0;
})
 
