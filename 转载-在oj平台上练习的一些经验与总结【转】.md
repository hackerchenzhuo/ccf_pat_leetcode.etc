# 转载：在oj平台上练习的一些经验与总结【转】

# [在oj平台上练习的一些总结【转】](https://www.cnblogs.com/lunlv/p/4985391.html)

<br/>
程序书写过程中的一些小技巧：

<br/>
1. freopen(“1.txt”,”r”,stdin); //程序运行后系统自动输入此文档里面的内容（不需要进行手动输入）<br/>
freopen(“1.txt”,”w”,stdout); //程序输出的内容保存在此文件里<br/>
2. memset(a,0,sizeof(a)); //数组的初始化。一般定义一个数组都要初始化<br/>
数组定义int a[10] 为全局变量的话，其全部元素默认赋值为0；整型数据默认为0，字符串默认为空。<br/>
3. #define max 0x0ffffff; //max 为正无穷<br/>
#define min -0x0ffffff;<br/>
4. 多组测试数据使用 while(n--){ 程序 }<br/>
5. 一般用C语言节约空间，要用C++库函数或STL时才用C++;<br/>
cout、cin和printf、scanf最好不要混用。而且需要注意的是，如果题目是大规模数据的输入输出，尽量使用printf和scanf，数据量一大，速度明显比c++的输入输出快。 输出1000000个数据，cout 大概用6s printf 用了0.562s<br/>
6. 有时候int型不够用，可以用long long或__int64型(两个下划线__)。<br/>
值类型表示值介于 -2^63 ( -9,223,372,036,854,775,808) 到2^63-1(+9,223,372,036,854,775,807 )之间的整数。<br/>
printf("%I64d",a);<br/>
printf("%lld",a);<br/>
7. OJ判断是只看输出结果的。<br/>
所以大部分题处理一组数据后可以直接输出，就不需要用数组保存每一个Case的数据。

<br/>
8. 纯字符串用puts()输出，会增快速度。<br/>
9. 先用scanf()，再用gets()会读入回车。scanf("%c%c",&amp;c1,&amp;c2) 后者会读入空格和回车；要使用getchar()吸收空格和回车的录入，使用c语言读字符和字符串一定要十分小心。尽量写好就自己输出一下看看是否是自己需要的值被读入。<br/>
10. 读到文件的结尾，程序自动结束<br/>
while( ( scanf(“%d”,&amp;a) ) != -1 )<br/>
while( ( scanf(“%d”,&amp;a) ) != EOF)<br/>
while( ( scanf(“%d”,&amp;a) ) == 1 )<br/>
读到一个0时，程序结束<br/>
while( scanf(“%d”,&amp;a) &amp;&amp;a)<br/>
读到多个0时，程序结束<br/>
while( scanf(“%d%d%d”,&amp;a,&amp;b,&amp;c)&amp;&amp;a+b+c )，该方法不能读取负值。<br/>
11. 圆周率=cos(-1.0) 自然对数=exp(1.0)<br/>
12. 如果要乘或除2^n,用位移运算速度快。a&gt;&gt;n;a&lt;&lt;n; 如：求n^m 时间复杂度log(m)<br/>
int calc(int n,int m){<br/>
int re=1;<br/>
while(m){<br/>
if(m&amp;1)<br/>
re*=n;<br/>
n*=n;<br/>
m&gt;&gt;=1;<br/>
}<br/>
return re;<br/>
}

<br/>
13. 定义数组时，数组大小最好比告诉的最大范围大一点。字符数组大小必须比字符串最大长度大1。<br/>
14. 习惯使用三目运算符<br/>
int max(int a,int b){return a&gt;b?a:b;}<br/>
int gcd(int m,int n){return n?gcd(n,m%n):m;}<br/>
int abs(int a){return a&lt;0?-a:a;}<br/>
15. 有的题数据范围小但是计算量大可以用打表法，先把结果算出来保存在数组里，要用时直接取出来。<br/>
16. 大概的计算自己程序的时间的方法：引入头文件：#include&lt;time.h&gt; 主函数末尾添加上一句cout&lt;&lt;(double)clock()/CLOCKS_PER_SEC;但是输入必需重定向，不然会计算输入数据等待时间。<br/>
17. runtimeerror 一般这种错误都是下标越界或者是未赋值的变量就直接使用这两种情况，一定要好好排查，不仔细一般找不出来。另外还有在函数内开了一个比较大的数组，使堆栈耗尽所以出错。 这个是后来加上的

 
