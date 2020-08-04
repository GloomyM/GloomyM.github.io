---
title: 最小生成树算法
date: 2019-10-24
tags: 算法
categories: 
  - 学习历程
  - 算法
  - 最小生成树
---

## 概述：

>　一个有N个点的图，边一定是大于等于N-1条的。图的最小生成树，就是在这些边中选择N-1条出来，连接所有的N个点。这N-1条边的边权之和是所有方案中最小的。

<!-- more -->

## Prim算法介绍：

>Prim算法采用与Dijkstra、Bellman-Ford算法一样的“蓝白点”思想：白点代表已经进入最小生成树的点，蓝点代表未进入最小生成树的点。

由于图中各点都是连通的，要想一条路上的总权值最小，那么最好的方法就是让这条路上的每条边的权值都是最小，那么只要每次找出一个权值最小的点，然后再从这个点出发更新其他可以连接的点的权值，每次更新直到走到最后一个点，最后将这些权值累加即可形成最小生成树。

那么最小生成树有什么实际的作用呢？

### 最优布线问题(wire)

**Description**

学校有n台计算机，为了方便数据传输，现要将它们用数据线连接起来。两台计算机被连接是指它们间有数据线连接。由于计算机所处的位置不同，因此不同的两台计算机的连接费用往往是不同的。

当然，如果将任意两台计算机都用数据线连接，费用将是相当庞大的。为了节省费用，我们采用数据的间接传输手段，即一台计算机可以间接的通过若干台计算机（作为中转）来实现与另一台计算机的连接。

现在由你负责连接这些计算机，任务是使任意两台计算机都连通（不管是直接的或间接的）。

**Input**

输入第一行为整数n（2<=n<=100），表示计算机的数目。此后的n行，每行n个整数。第x+1行y列的整数表示直接连接第x台计算机和第y台计算机的费用。

**Output**

输出一个整数，表示最小的连接费用。

**Sample Input 1**

3
0 1 2
1 0 1
2 1 0

**Sample Output 1**

2

Hint

表示连接1和2，2和3，费用为2

`解决这个问题很明显是最小生成树，不多赘述，直接看代码`

```cpp
#include <bits/stdc++.h>

using namespace std;

const int maxn = 1e4+5;
const int inf = 0x3f3f3f3f;
int mindis[maxn];
bool vis[maxn];

struct node
{
	int u;
	int w;
	node(int uu , int ww) : u(uu),w(ww){}
}; 
vector <node> e[maxn];

void add_edge(int u , int v , int w)
{
	e[u].push_back(node(v,w));
}

int main()
{
	fill(vis,vis+maxn,false);
	fill(mindis,mindis+maxn,inf);
	mindis[1] = 0;
	int n;
	cin >> n ;
	int tot = 0;
	for(int i = 1 ; i <= n ; i++)
	{
		for(int j = 1 ; j <= n ; j++)
		{
			int w;
			cin >> w;
			add_edge(i,j,w);
		}
	}
	for(int i = 1 ; i <= n ; i++)
	{
		int u = -1 , minn = inf;
		for(int j = 1 ; j <= n ; j++)
		{
			if(!vis[j] && minn > mindis[j])	//找出最小权值
			{
				minn = mindis[j];
				u = j;
			}
		}
		if(u == -1)
			break;
		vis[u] = true;
		for(int j = 0 ; j < e[u].size() ; j++)
		{
			int v = e[u][j].u;
			int w = e[u][j].w;
			if(!vis[v] && mindis[v] > w)	//更新边权
				mindis[v] = w;
		}
	}
	for(int i = 1 ; i <= n ; i++)	//累加所有最小的边权
		tot += mindis[i];	
	cout << tot << endl;
	return 0;
}
```
是不是看着很简单呢~那么下面这个算法应该更好理解了

## Kruskal算法介绍：
>Kruskal（克鲁斯卡尔）算法是一种巧妙利用并查集来求最小生成树的算法。首先我们把无向图中相互连通的一些点称为处于同一个连通块中，Kruskal算法将一个连通块当做一个集合。Kruskal首先将所有的边按从小到大顺序排序（一般使用快排），并认为每一个点都是孤立的，分属于n个独立的集合。然后按顺序枚举每一条边。如果这条边连接着两个不同的集合，那么就把这条边加入最小生成树，这两个不同的集合就合并成了一个集合；如果这条边连接的两个点属于同一集合，就跳过。直到选取了n-1条边为止。

`并查集以前写过这里就不多说了，看下面的例题和代码即可`

**联络员(liaison)**

**Description**

Tyvj已经一岁了，网站也由最初的几个用户增加到了上万个用户，随着Tyvj网站的逐步壮大，管理员的数目也越来越多，身为Tyvj管理层的联络员，现在希望你找到一些通信渠道，使得管理员两两都可以联络（直接或者是间接都可以）。Tyvj是一个公益性的网站，没有过多的利润，所以你要尽可能的使费用少才可以。

目前你已经知道，Tyvj的通信渠道分为两大类，一类是必选通信渠道，无论价格多少，你都需要把所有的都选择上；还有一类是选择性的通信渠道，你可以从中挑选一些作为最终管理员联络的通信渠道。数据保证给出的通行渠道可以让所有的管理员联通。

**Input**

第一行n，m表示Tyvj一共有n个管理员，有m个通信渠道

第二行到m+1行，每行四个非负整数，p,u,v,w 当p=1时，表示这个通信渠道为必选通信渠道；当p=2时，表示这个通信渠道为选择性通信渠道；u,v,w表示本条信息描述的是u，v管理员之间的通信渠道，u可以收到v的信息，v也可以收到u的信息，w表示费用。

**Output**

最小的通信费用

**Sample Input 1**

5 6
1 1 2 1
1 2 3 1
1 3 4 1
1 4 1 1
2 2 5 10
2 2 5 5

**Sample Output 1**

9

**Hint**

【样例解释】

1-2-3-4-1存在四个必选渠道，形成一个环，互相可以到达。需要让所有管理员联通，需要联通2号和5号管理员，选择费用为5的渠道，所以总的费用为9。

【注意】

U,v之间可能存在多条通信渠道，你的程序应该累加所有u,v之间的必选通行渠道

【数据范围】

对于30%的数据，n<=10 m<=100

对于50%的数据, n<=200 m<=1000

对于100%的数据，n<=2000 m<=10000

```cpp
#include<bits/stdc++.h>

using namespace std;

const int maxn = 1e4+5;
const int inf = 0x3f3f3f3f;
bool vis[maxn];
int p[maxn];
int n,m;


int find(int x)
{
	return x == p[x] ? x : p[x] = find(p[x]);
}

struct node
{
	int u,v,w;
	friend bool operator <(node a , node b)
	{
		return a.w < b.w;
	}
}e[maxn];

int main()
{
	cin >> n >> m;
	for(int i = 1 ; i <= n ; i++)
		p[i] = i;
	int sum = 0;
	for(int i = 0 ; i < m ; i++)
	{
		int pp;
		cin >> pp >> e[i].u >> e[i].v >> e[i].w;
		if(pp == 1)
		{
			int r1 = find(e[i].u),r2 = find(e[i].v);
			p[r1] = r2;
			sum += e[i].w;
		}
	}
	sort(e,e+m);
	for(int i = 0 ; i < m ; i++)
	{
		int u = e[i].u;
		int v = e[i].v;
		int r1 = find(u),r2 = find(v);
		if(r1 == r2)
			continue;
		p[r1] = r2;
		sum += e[i].w;
	}
	cout << sum ;
	return 0;
}
```

