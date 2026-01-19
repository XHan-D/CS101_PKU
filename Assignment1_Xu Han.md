# Assignment #1: 自主学习

Updated 1306 GMT+8 Sep 14, 2025

2025 fall, Complied by **韩旭 元培学院**



**作业的各项评分细则及对应的得分**

| 标准                                 | 等级                                                         | 得分 |
| ------------------------------------ | ------------------------------------------------------------ | ---- |
| 按时提交                             | 完全按时提交：1分<br/>提交有请假说明：0.5分<br/>未提交：0分  | 1 分 |
| 源码、耗时（可选）、解题思路（可选） | 提交了4个或更多题目且包含所有必要信息：1分<br/>提交了2个或以上题目但不足4个：0.5分<br/>少于2个：0分 | 1 分 |
| AC代码截图                           | 提交了4个或更多题目且包含所有必要信息：1分<br/>提交了2个或以上题目但不足4个：0.5分<br/>少于：0分 | 1 分 |
| 清晰头像、PDF文件、MD/DOC附件        | 包含清晰的Canvas头像、PDF文件以及MD或DOC格式的附件：1分<br/>缺少上述三项中的任意一项：0.5分<br/>缺失两项或以上：0分 | 1 分 |
| 学习总结和个人收获                   | 提交了学习总结和个人收获：1分<br/>未提交学习总结或内容不详：0分 | 1 分 |
| 总得分： 5                           | 总分满分：5分                                                |      |

>
>
>
>**说明：**
>
>1. **解题与记录：**
>
>  对于每一个题目，请提供其解题思路（可选），并附上使用Python或C++编写的源代码（确保已在OpenJudge， Codeforces，LeetCode等平台上获得Accepted）。请将这些信息连同显示“Accepted”的截图一起填写到下方的作业模板中。（推荐使用Typora https://typoraio.cn 进行编辑，当然你也可以选择Word。）无论题目是否已通过，请标明每个题目大致花费的时间。
>
>2. **课程平台：**课程网站位于Canvas平台（https://pku.instructure.com ）。该平台将在<mark>第2周</mark>选课结束后正式启用。在平台启用前，请先完成作业并将作业妥善保存。待Canvas平台激活后，再上传你的作业。
>
>3. **提交安排：**提交时，请首先上传PDF格式的文件，并将.md或.doc格式的文件作为附件上传至右侧的“作业评论”区。确保你的Canvas账户有一个清晰可见的本人头像，提交的文件为PDF格式，并且“作业评论”区包含上传的.md或.doc附件。
>
>4. **延迟提交：**如果你预计无法在截止日期前提交作业，请提前告知具体原因。这有助于我们了解情况并可能为你提供适当的延期或其他帮助。  
>
>请按照上述指导认真准备和提交作业，以保证顺利完成课程要求。





## 1. 题目

### E02733: 判断闰年

http://cs101.openjudge.cn/pctbook/E02733/

用时：2min



思路

按照闰年定义列分支语句即可。注意题目中虽然提到“能被3200整除的也不是闰年”，但输入数据范围在3000以内，故代码中不予体现。



代码

```python
year=int(input())
if year%4!=0:
    print("N")
else:
    if year%100!=0:
        print("Y")
    else:
        if year%400!=0:
            print("N")
        else: print("Y")
```



代码运行截图

![image-20250923231647252](C:\Users\Xu Han\AppData\Roaming\Typora\typora-user-images\image-20250923231647252.png)





### E02750: 鸡兔同笼

http://cs101.openjudge.cn/pctbook/E02750/

用时：5min



思路

注意到符合要求的脚个数必须是偶数，然后分类讨论即可。



代码

```python
foot=int(input())
if foot%2:
    print("0 0")
else:
    Max=int(foot/2)
    if not foot%4:
        Min=int(foot/4)
    else:
        Min=int(foot//4+1)
    print(Min,Max)
```



代码运行截图

![image-20250923232948487](C:\Users\Xu Han\AppData\Roaming\Typora\typora-user-images\image-20250923232948487.png)





### 50A. Domino piling

greedy, math, 800, http://codeforces.com/problemset/problem/50/A

用时：5min



思路

按边的奇偶数分类即可。注意最后的算式可以涵盖m=1或n=1的情况。



代码

```python
m,n=map(int,input().split())
ans=0
if m%2==0 or n%2==0:
    ans=int(m*n/2)
else:
    ans=int(((m-1)/2)*n+(n-1)/2)
print(ans)
```



代码运行截图

![image-20250923234546662](C:\Users\Xu Han\AppData\Roaming\Typora\typora-user-images\image-20250923234546662.png)





### 1A. Theatre Square

math, 1000, https://codeforces.com/problemset/problem/1/A

用时：5min



思路

按两边边长（n, m）能否整除a分类即可，不能整除则+1。



代码

```python
n,m,a=map(int,input().split())
n_num= n//a+1 if n%a else n//a
m_num= m//a+1 if m%a else m//a
print(n_num*m_num)
```



代码运行截图

![image-20250923235458445](C:\Users\Xu Han\AppData\Roaming\Typora\typora-user-images\image-20250923235458445.png)





### 112A. Petya and Strings

implementation, strings, 1000, http://codeforces.com/problemset/problem/112/A

用时：5min



思路

用到函数a.lower() （或者a.upper()）。



代码

```python
string1=input()
string2=input()
length=len(string1)
for i in range(length):
    if string1[i].lower()>string2[i].lower():
        print(1)
        break
    elif string1[i].lower()<string2[i].lower():
        print(-1)
        break
    elif string1[i].lower()==string2[i].lower() and i==length-1:
        print(0)
    else:
        continue
```



代码运行截图

![image-20250924000119947](C:\Users\Xu Han\AppData\Roaming\Typora\typora-user-images\image-20250924000119947.png)





### 231A. Team

bruteforce, greedy, 800, http://codeforces.com/problemset/problem/231/A

用时：2min



思路

直接求和判断大于等于2即可。



代码

```python
n=int(input())
ans=0
for i in range(n):
    a,b,c=map(int,input().split())
    if a+b+c>=2:
        ans+=1
print(ans)
```



代码运行截图

![image-20250924003157171](C:\Users\Xu Han\AppData\Roaming\Typora\typora-user-images\image-20250924003157171.png)





## 2. 学习总结和收获

- 这几题核心都是**模型化+分类**：把约束抽象成不变量，再按奇偶/整除分情形就可以概括（Domino 覆盖 m=1 或 n=1；Theatre Square 用整除+补 1）。
- 现在习惯**先样例后边界**：写完先跑极端值（如 n=1、m=1），再决定是否要分支，调试成本更低。
- 思维上更偏**贪心/不变量**：鸡兔同笼盯“偶数脚+上下界”直接定位解；字符串题统一大小写后比较。

