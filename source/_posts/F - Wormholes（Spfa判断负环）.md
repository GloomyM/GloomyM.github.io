---
title: F - Wormholes（判断负环）
date: 2019-10-23
tags: 算法
categories: 
  - 学习历程
  - 算法
  - 最短路径
---

While exploring his many farms, Farmer John has discovered a number of amazing wormholes. A wormhole is very peculiar because it is a one-way path 

<!-- more -->

that delivers you to its destination at a time that is BEFORE you entered the wormhole! Each of FJ's farms comprises N (1 ≤ N ≤ 500) fields conveniently numbered 1..N, M (1 ≤ M ≤ 2500) paths, and W (1 ≤ W ≤ 200) wormholes.As FJ is an avid time-traveling fan, he wants to do the following: start at some field, travel through some paths and wormholes, and return to the starting field a time before his initial departure. Perhaps he will be able to meet himself :) .To help FJ find out whether this is possible or not, he will supply you with complete maps to F (1 ≤ F ≤ 5) of his farms. No paths will take longer than 10,000 seconds to travel and no wormhole can bring FJ back in time by more than 10,000 seconds.

#### Input
Line 1: A single integer, F. F farm descriptions follow.
Line 1 of each farm: Three space-separated integers respectively: N, M, and W
Lines 2.. M+1 of each farm: Three space-separated numbers ( S, E, T) that describe, respectively: a bidirectional path between S and E that requires T seconds to traverse. Two fields might be connected by more than one path.
Lines M+2.. M+ W+1 of each farm: Three space-separated numbers ( S, E, T) that describe, respectively: A one way path from S to E that also moves the traveler back T seconds. 

#### Output
Lines 1.. F: For each farm, output "YES" if FJ can achieve his goal, otherwise output "NO" (do not include the quotes). 
#### Sample Input
​    2
​    3 3 1
​    1 2 2
​    1 3 4
​    2 3 1
​    3 1 3
​    3 2 1
​    1 2 3
​    2 3 4
​    3 1 8

#### Sample Output

   NO
    YES

#### Hint
For farm 1, FJ cannot travel back in time.
For farm 2, FJ could travel back in time by the cycle 1->2->3->1, arriving back at his starting location 1 second before he leaves. He could start from anywhere on the cycle to accomplish this. 

#### 题目大意

**感觉这题题意太抽象，大意是f张图每张图有n个点，m条路，w条负权路，问从一点出发，是否能后最后还回到这点且能看到原来的自己，也就是判断是否存在负环，最短路中判断负环一般用Spfa**

```cpp
#include<iostream>
#include<vector>
#include<queue>

using namespace std;
const int maxn = 1e5+5;
const int inf = 0x3f3f3f3f;
int cnt[maxn]; 
bool vis[maxn];
int dis[maxn];
int f,n,m,w;

struct node
{
	int u,w;
	node(int uu , int ww) : u(uu),w(ww){}
};
vector<node>e[maxn];

void add_edge(int u , int v , int w)
{
	e[u].push_back(node(v,w));
}

int spfa()
{
	fill(vis,vis+maxn,false);
	fill(dis,dis+maxn,inf);
	fill(cnt,cnt+maxn,0);
	queue<int>q;
	q.push(1);
	dis[1] = 0;
	vis[1] = true;
	cnt[1] = 1;
	while(!q.empty())
	{
		int u = q.front();
		q.pop();
		for(int i = 0 ; i < e[u].size() ; i++)
		{
			int v = e[u][i].u;
			int w = e[u][i].w;
			if(dis[v] > dis[u] + w)
			{
				dis[v] = dis[u] + w;
				if(!vis[v])
				{
					vis[v] = true;
					cnt[v]++;				
					if(cnt[v] >= n)
						return 1;
					q.push(v);
				}	
			} 
		}
		vis[u] = false;
	}
	return 0;
}

int main()
{
	cin >> f;
	while(f--)
	{
		cin >> n >> m >> w;
		for(int i = 1 ; i <= n  ; i++)
			e[i].clear();
		for(int i = 0 ; i < m ; i++)
		{
			int u,v,r;
			cin >> u >> v >> r;
			add_edge(u,v,r);
			add_edge(v,u,r);
		}
		for(int i = 0 ; i < w ; i++)
		{
			int u,v,r;
			cin >> u >> v >> r;
			add_edge(u,v,-r); 
		}
		if(spfa())
			cout << "YES\n";
		else
			cout << "NO\n";
	}
	return 0;
} 
```

