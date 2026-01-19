# Assignment #C: bfs & dp

Updated 1436 GMT+8 Nov 25, 2025

2025 fall, Complied by **韩旭 元培学院**

**说明：**

1）请把每个题目解题思路（可选），源码Python, 或者C++（已经在Codeforces/Openjudge上AC），截图（包含Accepted），填写到下面作业模版中（推荐使用 typora https://typoraio.cn ，或者用word）。AC 或者没有AC，都请标上每个题目大致花费时间。

2）提交时候先提交pdf文件，再把md或者doc文件上传到右侧“作业评论”。Canvas需要有同学清晰头像、提交文件有pdf、"作业评论"区有上传的md或者doc附件。

3）如果不能在截止前提交作业，请写明原因。



## 1. 题目

### sy321迷宫最短路径

bfs, https://sunnywhy.com/sfbj/8/2/321

用时：20min



思路：

这道题是经典的bfs走迷宫的变式，在普通版本的基础上需要对bfs找出的最短路径进行记录。这里仍然需要注意普通版本的一些事项，比如保护圈、`inq`集合记录已经进入队列的点等。这里面使用了`prev`矩阵来记录路径，思路类似并查集，即在队列中某节点出队列后，将其记录为下一步能到达的所有节点的父节点。这样，最后到达(n,m)点返回后，在`prev`矩阵中逐渐上溯到(1,1)再反转（用`path.reverse()`函数）即可得到相应路径。



代码：

```python
from collections import deque

n,m=map(int,input().split())
maze=[[-1]*(m+2)]+[[-1]+list(map(int,input().split()))+[-1] for _ in range(n)]+[[-1]*(m+2)]
dx=[-1,1,0,0]
dy=[0,0,-1,1]

def bfs(x,y,n,m,maze):
    queue=deque([(x,y)])
    inq={(x,y)}
    prev=[[False]*(m+2) for _ in range(n+2)]

    while queue:
        cur_x,cur_y=queue.popleft()
        if cur_x==n and cur_y==m:
            return prev
        for i in range(4):
            next_x=cur_x+dx[i]
            next_y=cur_y+dy[i]
            if maze[next_x][next_y]==0 and (next_x,next_y) not in inq:
                queue.append((next_x,next_y))
                inq.add((next_x,next_y))
                prev[next_x][next_y]=(cur_x,cur_y)

prev=bfs(1,1,n,m,maze)
path=[(n,m)]
tmp_x,tmp_y=n,m
while tmp_x!=1 or tmp_y!=1:
    path.append(prev[tmp_x][tmp_y])
    tmp_x,tmp_y=prev[tmp_x][tmp_y]
path.reverse()

for x,y in path:
    print(x,y)
```



代码运行截图

![image-20251202163842119](C:\Users\Xu Han\AppData\Roaming\Typora\typora-user-images\image-20251202163842119.png)





### sy324多终点迷宫问题

bfs, https://sunnywhy.com/sfbj/8/2/324

用时：10min



思路：

这道题也是经典的bfs走迷宫的变式，在普通版本的基础上需要对到达每个点的最短路径进行记录。由于本题输出的是路径长度，所以保存到队列里面的元组要包含目前的步数。bfs的特性保证了只要完整地跑完这个算法，就可以遍历迷宫中所有可达的点，且到达每个点的时候都是最短路径。因此只需要在每个节点出队列的时候，将对应的步长记录在`ans`矩阵中即可，没有被记录的节点默认为-1（不可达到）。



代码：

```python
from collections import deque

n,m=map(int,input().split())
maze=[[-1]*(m+2)]+[[-1]+list(map(int,input().split()))+[-1] for _ in range(n)]+[[-1]*(m+2)]
dx=[-1,1,0,0]
dy=[0,0,-1,1]
ans=[[-1]*(m+2) for _ in range(n+2)]

def bfs(x,y,maze):
    queue=deque([(0,x,y)])
    inq={(x,y)}
    while queue:
        step,cur_x,cur_y=queue.popleft()
        ans[cur_x][cur_y]=step
        for i in range(4):
            next_x=cur_x+dx[i]
            next_y=cur_y+dy[i]
            if maze[next_x][next_y]==0 and (next_x,next_y) not in inq:
                queue.append((step+1,next_x,next_y))
                inq.add((next_x,next_y))

prev=bfs(1,1,maze)
for i in range(1,n+1):
    print(" ".join(map(str,ans[i][1:m+1])))
```



代码运行截图

![image-20251202173849199](C:\Users\Xu Han\AppData\Roaming\Typora\typora-user-images\image-20251202173849199.png)





### M02945: 拦截导弹

dp, greedy http://cs101.openjudge.cn/pctbook/M02945

用时：25min



思路

这道题等价于在导弹序列中找到单调递减（非严格）的最长子序列。我们按照子序列结尾进行dp，`dp[i]`表示以序号i的导弹结尾的子序列中，最长的单调递减子序列。那么对于`dp[i+1]`，我们只需要遍历第0个到第i-1个导弹，然后找到其中不比第i个导弹小的导弹序号s，再在`1+dp[s]`中选取最大值即可。



代码：

```python
k=int(input())
missile=list(map(int,input().split()))
dp=[0]*k
for i in range(k):
    if i==0:
        dp[i]=1
        continue
    tmp=1
    for s in range(i-1,-1,-1):
        if missile[s] >= missile[i]:
            tmp=max(tmp,1+dp[s])
    dp[i]=tmp

ans=0
for i in range(k):
    ans=max(ans,dp[i])
print(ans)
```



代码运行截图

![image-20251202180852666](C:\Users\Xu Han\AppData\Roaming\Typora\typora-user-images\image-20251202180852666.png)





### 189A. Cut Ribbon

brute force/dp, 1300, https://codeforces.com/problemset/problem/189/A

用时：10min



思路：

这道题根据ribbon的长度确定状态进行dp。对于某个长度i，我们要找出其最多能按照a,b,c切成多少段。那么就遍历a,b,c，以a为例，考虑去掉a之后长度为i-a的ribbon能否按a,b,c切分，以及如果能，能够切多少段。所以这里的判断条件比较重要，如果要更新`dp[i]`，要么是`i-a==0`，即切掉a后就完成了，这时候更新为1；要么是`i-a>0`但是`dp[i-a]>0`，即切掉a之后剩下的部分能够按照a,b,c切分，这时候更新为`dp[i-a]+1`。遍历a,b,c，选出对应更新的`dp[i]`中的最大值即可。这里默认值设置成`-float('inf')`可能更好，相当于区分清楚了“无法按a,b,c切分”和"0段"的情况，if条件更简单。



代码：

```python
n,a,b,c=map(int,input().split())
dp=[0]*(n+1)
MIN=min(a,b,c)
for i in range(n+1):
    if i<MIN:
        continue
    if i==MIN:
        dp[i]=1
    for j in [a,b,c]:
        if (i-j>0 and dp[i-j]>0) or (i==j):
            dp[i]=max(dp[i],dp[i-j]+1)
print(dp[n])
```



代码运行截图

![image-20251202222223015](C:\Users\Xu Han\AppData\Roaming\Typora\typora-user-images\image-20251202222223015.png)





### M01384: Piggy-Bank

dp, http://cs101.openjudge.cn/practice/01384/

用时：25min



思路

这道题的整体思路和Cut Ribbon很像，但是Cut Ribbon是取最大值，所以默认值设置为0（或者`-float('inf')`更好），这里面是算最小值，所以默认值设置为`float('inf')`。注意这里面用coins数组整体存储values和weights的方式可以在循环时直接对coin数组循环避免使用索引，从而提高速度。



代码：

```python
T=int(input())
for _ in range(T):
    E,F=map(int,input().split())
    W=F-E
    N=int(input())
    coins=[]
    for i in range(N):
        coins.append(tuple(map(int,input().split())))
    dp=[float('inf')]*(W+1)
    dp[0]=0
    for i in range(W+1):
        for v,w in coins:
            if i-w>=0:
                dp[i]=min(dp[i],v+dp[i-w])
    if dp[W]<float('inf'):
        print(f"The minimum amount of money in the piggy-bank is {dp[W]}.")
    else:
        print("This is impossible.")
```



代码运行截图

![image-20251202232758560](C:\Users\Xu Han\AppData\Roaming\Typora\typora-user-images\image-20251202232758560.png)





### M02766: 最大子矩阵

dp, kadane, http://cs101.openjudge.cn/pctbook/M02766

用时：20min



思路

首先遍历子矩阵的最上方行和最下方行（`top`和`bottom`），然后把各列和压缩成`col_sum`，再使用Kandane算法即可。这里要特别注意计算`col_sum`的时候，不需要对每一对`top`和`bottom`都从头开始计算，而是使用类似前缀和的方式，在遍历`bottom`的时候依次在`col_sum`上把当前行的值进行累加，就可以得到当前从`top`到`bottom`的各列和。另外需要注意这个题目的输入比较奇怪，第一，需要限定输入的数字个数在`n**2`以内，然后用`while`循环进行不定行输入；第二，需要用一个列表生成式把nums切片成matrix。



代码：

```python
n=int(input())
nums=[]
while len(nums)<n**2:
    nums+=list(map(int,input().split()))
matrix=[nums[i*n:(i+1)*n] for i in range(n)]

def kadane(s):
    cur_max=total_max=s[0]
    for x in s[1:]:
        cur_max=max(x,cur_max+x)
        total_max=max(total_max,cur_max)
    return total_max

ans=0
for top in range(n):
    col_sum=[0]*n
    for bottom in range(top,n):
        for j in range(n):
            col_sum[j]+=matrix[bottom][j]
        ans=max(ans,kadane(col_sum))
print(ans)
```



代码运行截图

![image-20251209161654350](C:\Users\Xu Han\AppData\Roaming\Typora\typora-user-images\image-20251209161654350.png)



## 2. 学习总结和收获

本次作业包括 BFS 与 DP 两个部分。

在BFS 部分，通过两道迷宫题，我更加熟悉了BFS的模版写法，同时也认识到BFS在进入队列的元素、需要记录的内容等方面具有一定的**灵活性**，这方面和前面练习的DFS（比如全排列的各种变式）很像，比如所需要的结果有时候在进入队列的元素里面递推地记录，有时候又可以在一个全局变量或数据结构中记录。尤其在第一题中，通过维护 `prev` 矩阵实现最短路径恢复，思路和**并查集**的想法很像，是一种**用链表构造图关系**的方法。与此同时，我也关注到了BFS中的常见技巧，例如保护圈、`inq` 集合/数组去重等。

在DP部分，我发现很多dp的题型都可以归结为某些经典的例题，比如说拦截导弹问题实际上是 **LIS 的递减版**，关键仍然在于围绕“以 i 结尾”的子序列建立局部最优。Cut Ribbon 与 Piggy Bank 本质上都是**完全背包问题**，其核心就是允许同一物品重复使用，并且在更新 dp 时只需考虑 dp[i - w] 是否可行。但它们分别是取最大值与取最小值的版本，从而需要不同的默认值与判断逻辑（如 `float('inf')`）。
