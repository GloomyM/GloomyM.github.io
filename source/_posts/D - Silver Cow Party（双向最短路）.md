---
title: D - Silver Cow Party（双向最短路）
date: 2019-10-23
tags: 算法
categories: 
  - 学习历程
  - 算法
  - 最短路径
---

One cow from each of N farms (1 ≤ N ≤ 1000) conveniently numbered 1..N is going to attend the big cow party to be held at farm #X (1 ≤ X ≤ N). A total of M (1 ≤ M ≤ 100,000) unidirectional (one-way roads connects pairs of farms; road i 

<!-- more -->

requires Ti (1 ≤ Ti ≤ 100) units of time to traverse.Each cow must walk to the party and, when the party is over, return to her farm. Each cow is lazy and thus picks an optimal route with the shortest time. A cow's return route might be different from her original route to the party since roads are one-way.Of all the cows, what is the longest amount of time a cow must spend walking to the party and back?

#### Input
Line 1: Three space-separated integers, respectively: N, M, and X
Lines 2.. M+1: Line i+1 describes road i with three space-separated integers: Ai, Bi, and Ti. The described road runs from farm Ai to farm Bi, requiring Ti time units to traverse. 
#### Output
Line 1: One integer: the maximum of time any one cow must walk. 
#### Sample Input
​    4 8 2
​    1 2 4
​    1 3 2
​    1 4 7
​    2 1 1
​    2 3 5
​    3 1 2
​    3 4 4
​    4 2 3

#### Sample Output

   10

#### Hint
   Cow 4 proceeds directly to the party (3 units) and returns via farms 1 and 3 (7 units), for a total of 10 time units. 

#### 题意大意
**农场x举办派对，不同的牛要从自己的农场到x农场参加派对，由于路是单向的，所以来回的最短路径是不同的，现在要找出来回一次的最短路中最长的路线 ,也就是双向最短路，然后在这些最短路中寻找最长的一条，每次用两次Dij算法，一来一回，然后找最大值即可**

```c++
#include<iostream>
#include<queue>
#include<vector>

using namespace std;

const int maxn = 1e5+5;
const int inf = 0x3f3f3f3f;
int dis[maxn];
bool vis[maxn];
int m,n,x;

struct node
{
	int u,w;
	node(int uu , int ww) : u(uu),w(ww){}
	friend bool operator < (node a , node b)
	{
		return a.w > b.w;
	}
};
vector<node>e[maxn];
priority_queue<node>pque;

void add_edge(int u , int v , int w)
{
	e[u].push_back(node(v,w));	
} 

int Dij(int st , int ed)
{
	while(!pque.empty())
		pque.pop();
	fill(vis,vis+maxn,false);
	fill(dis,dis+maxn,inf);
	pque.push(node(st,0));
	dis[st] = 0;
	while(!pque.empty())
	{
		node t = pque.top();
		pque.pop();
		int u = t.u;
		if(vis[u])
			continue;
		vis[u] = true;
		for(int i = 0 ; i < e[u].size() ; i++)
		{
			int v = e[u][i].u;
			int w = e[u][i].w;
			if(dis[v] > dis[u] + w)
			{
				dis[v] = dis[u] + w;
				pque.push(node(v,dis[v]));
			}
		}
	}
	return dis[ed];
}


int main()
{
	cin >> n >> m >> x;
	for(int i = 0 ; i < m ; i++)
	{
		int u,v,w;
		cin >> u >> v >> w;
		add_edge(u,v,w);
	}
	int maxm = 0 , sum = 0;
	for(int i = 1 ; i <= n ; i++)
	{
		if(i != x)
			sum = Dij(i,x) + Dij(x,i);
		maxm = max(sum,maxm);
	}
	cout << maxm << endl;
	return 0;
} 
```

