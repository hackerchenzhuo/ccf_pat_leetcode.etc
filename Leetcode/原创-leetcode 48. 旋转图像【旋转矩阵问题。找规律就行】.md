# 原创：leetcode 48. 旋转图像【旋转矩阵问题。找规律就行】

把正方形分为四个部分。只需要动其中一个部分就行，其他的按旋转平移

> 
<p>a1=matrix[i][j];<br/>
 matrix[i][j]=matrix[sz-1-j][i];<br/>
matrix[sz-1-j][i]=matrix[sz-1-i][sz-1-j];<br/>
matrix[sz-1-i][sz-1-j]=matrix[j][sz-1-i];<br/>
matrix[j][sz-1-i]=a1;</p>


 
