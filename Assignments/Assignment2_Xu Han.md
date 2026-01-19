# Assignment #2: 语法练习

Updated 1335 GMT+8 Sep 16, 2025

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

### 263A. Beautiful Matrix

implementation, 800, https://codeforces.com/problemset/problem/263/A

用时：10min



思路

这个题目实际上和矩阵没有什么关系，只需要计算“1”所在位置到中心位置的水平+垂直距离就可以。



代码

```python
row, column=1,1
for i in range(5):
    Row=list(map(int,input().split()))
    if sum(Row)==1:
        row+=i
        column+=Row.index(1)
print(abs(row-3)+abs(column-3))
```



代码运行截图

![image-20251007161918497](C:\Users\Xu Han\AppData\Roaming\Typora\typora-user-images\image-20251007161918497.png)



### 1328A. Divisibility Problem

math, 800, https://codeforces.com/problemset/problem/1328/A

用时：5min



思路

按照余数向上补全即可。如果这题是可加可减会更有趣，但也只需要多讨论几种情况。



代码

```python
N=int(input())
for _ in range(N):
    a,b=map(int,input().split())
    r=a%b
    if r==0:
        print(0)
    else:
        print(b-r)
```



代码运行截图

![image-20251007162815133](C:\Users\Xu Han\AppData\Roaming\Typora\typora-user-images\image-20251007162815133.png)



### 427A. Police Recruits

implementation, 800, https://codeforces.com/problemset/problem/427/A

用时：5min



思路

按照题意分类计数即可。



代码

```python
N=int(input())
police=0
untreated=0
L=list(map(int,input().split()))
for i in L:
    if i>0:
        police+=i
    elif i==-1:
        if police>=1:
            police-=1
        else:
            untreated+=1
    else:
        print("Error.")
print(untreated)
```



代码运行截图

![image-20251007163430548](C:\Users\Xu Han\AppData\Roaming\Typora\typora-user-images\image-20251007163430548.png)



### E02808: 校门外的树

implementation, http://cs101.openjudge.cn/pctbook/E02808/

用时：10min



思路

按照对应区间把树的标记改成0，如果已经是0则不动。



代码

```python
L,M=map(int,input().split())
trees=[1]*(L+1)
for _ in range(M):
    s, e = map(int, input().split())
    for i in range(e-s+1):
        if trees[s+i]>0:
            trees[s + i]=0
print(sum(trees))
```



代码运行截图 

![image-20251007165008725](C:\Users\Xu Han\AppData\Roaming\Typora\typora-user-images\image-20251007165008725.png)



### sy60: 水仙花数II

implementation, https://sunnywhy.com/sfbj/3/1/60

用时：10min



思路

这题的输出要求比较高，需要整合成list之后，使用print(*list)的方式输出。



代码

```python
def nar(num):
    hundred=num//100
    ten=(num-100*hundred)//10
    one=num-100*hundred-10*ten
    return hundred**3+ten**3+one**3==num

a,b=map(int,input().split())
x=0
count=0
L=[]
while x<=b-a:
    if nar(a+x):
        L.append(a+x)
        count+=1
    x+=1
if count==0:
    print("NO")
else:
    print(*L)
```



代码运行截图 

![image-20251007180838735](C:\Users\Xu Han\AppData\Roaming\Typora\typora-user-images\image-20251007180838735.png)



### M01922: Ride to School

implementation, http://cs101.openjudge.cn/pctbook/M01922/

本题暂时跳过。



## 2. 学习总结和收获

- 这几题仍然需要我们**抽象**出具体的数学问题。比如第一题其实就是到中心的曼哈顿距离，不必把它当矩阵题。  

- 第二题AI说这样写会更简洁：`(b - a % b) % b` 。  
- 第三题使用**状态计数器**，在动态规划或者其他算法的题目中也很常见。  
- 第四题AI给出了降低复杂度的方法，即**差分+求和**：用 `diff[s]+=1, diff[e+1]-=1`进行标记，然后对某个位置之前的diff求和，如果大于0就是被砍掉了，否则没被砍掉。复杂度从区间总长度降到 O(L+M)。  
- 输出的小技巧：`print(*ans)` 或 `' '.join(map(str, ans))`，分别适合“直接打印”和“先合成字符串”。  

