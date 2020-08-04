---
title: B - Frogger
date: 2019-10-23
tags: 算法
categories: 
  - 学习历程
  - 算法
  - 最短路径
---

Freddy Frog is sitting on a stone in the middle of a lake. Suddenly he notices Fiona Frog who is sitting on another stone. He plans to visit her, but since the 

<!-- more -->

water is dirty and full of tourists' sunscreen, he wants to avoid swimming and instead reach her by jumping. Unfortunately Fiona's stone is out of his jump range. Therefore Freddy considers to use other stones as intermediate stops and reach her by a sequence of several small jumps. To execute a given sequence of jumps, a frog's jump range obviously must be at least as long as the longest jump occuring in the sequence. The frog distance (humans also call it minimax distance) between two stones therefore is defined as the minimum necessary jump range over all possible paths between the two stones.You are given the coordinates of Freddy's stone, Fiona's stone and all other stones in the lake. Your job is to compute the frog distance between Freddy's and Fiona's stone.   

 #### Input


The input will contain one or more test cases. The first line of each test case will contain the number of stones n (2<=n<=200). The next n lines each contain two integers xi,yi (0 <= xi,yi <= 1000) representing the coordinates of stone #i. Stone #1 is Freddy's stone, stone #2 is Fiona's stone, the other n-2 stones are unoccupied. There's a blank line following each test case. Input is terminated by a value of zero (0) for n. 
#### Output


For each test case, print a line saying "Scenario #x" and a line saying "Frog Distance = y" where x is replaced by the test case number (they are numbered from 1) and y is replaced by the appropriate real number, printed to three decimals. Put a blank line after each test case, even after the last one. 
#### Sample Input
2
0 0
3 4

3
17 4
19 4
18 5

0


#### Sample Output

Scenario #1
Frog Distance = 5.000

Scenario #2
Frog Distance = 1.414

#### 题目大意

**青蛙想从位置1到位置2，这中间有很多块石头，每块石头之间相隔一定的距离，求出最大跳远距离中的最小值，举个例子，①：1 -> 3(5) -> 4 (2) -> 2（3）②：1 -> 4(3) -> 3(2) -> 2(1)在第一条条通路中，最大跳远距离是5，第二条通路中最大跳远距离为3，那么在这两条通路中最大跳远距离的最小值就是3（刚开始我也没太理解题意= =还是题做得太少了）**

```cpp
/*堆优化的Dij算法*/
#include<iostream>
#include<cstdio>
#include<cmath>
#include<vector>
#include<queue>

using namespace std;
const int maxn = 210;
const int inf = 0x3f3f3f3f;
double dx[maxn],dy[maxn],dis[maxn];
bool vis[maxn];
int n,cnt = 1;

double cal(double x,double y,double xx,double yy)
{
	return sqrt((x-xx)*(x-xx)+(y-yy)*(y-yy));
}

float max(float a , float b)
{
	return a > b ? a : b;
}

struct node
{
	int v;
	double w;
	node(int vv , double ww):v(vv),w(ww){}
	friend bool operator <(node a,node b)
	{
		return a.w > b.w;
	}
};
vector<node>e[maxn];


void add_edge(int u , int v , double w)
{
	e[u].push_back(node(v,w));
}

void Dij(int st,int ed)
{
	priority_queue<node>pque;
	fill(vis,vis+maxn,false);
	fill(dis,dis+maxn,inf);
	dis[st] = 0;
	pque.push(node(st,0));
	while(!pque.empty())
	{
		node t = pque.top();
		pque.pop();
		int u = t.v;
		if(vis[u])
			continue;
		vis[u] = true;
		for(int i = 0 ; i < e[u].size() ; i++)
		{
			int v = e[u][i].v;
			double w = e[u][i].w;
			if(!vis[v] && dis[v] > max(w,dis[u]))//dis[v]表示从源点到v的最大跳跃距离的最小值，第一次做不太好理解，还是多做题！
			{
				dis[v] = max(w,dis[u]);
				pque.push(node(v,dis[v]));
			}
		}
	}
	printf("Scenario #%d\nFrog Distance = %.3f\n\n",cnt++,dis[ed]);//注意每次输出后腰空一行
}


int main()
{
	while(cin >> n)
	{
		for(int i = 1 ; i <= n ; i++)	//每组数据读入前要清空上一组数据
			e[i].clear();
		if(n == 0)
			break;
		for(int i = 1 ; i <= n ; i++)
			cin >> dx[i] >> dy[i];
		for(int i = 1 ; i <= n ; i++)
		{
			for(int j = i + 1 ; j <= n ; j++)
			{
				double w = cal(dx[i],dy[i],dx[j],dy[j]);
				add_edge(i,j,w);
				add_edge(j,i,w);
			} 
		}
		Dij(1,2);	
	}
	return 0;
}
```

