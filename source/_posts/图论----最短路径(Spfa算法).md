---
title: 最短路径(Spfa算法)
date: 2019-09-06
tags: 算法
categories: 
  - 学习历程
  - 算法
  - 最短路径
---

﻿# 概述

SPFA算法O(kE，k是常数，平均值为2，是Bellman-Ford算法的队列实现)，Bellman-Ford算法主要是处理负权边问题，但无法处理负回路，只能判断是否为负环。
# 算法描述
dis数组用来存储从源点到各个点的路径长度，vis用来标记是否已经被走过，这里注意，每次取出队头元素，对所有点进行遍历时要对每个点进行标记，但处理完之后要把对头元素重新标记为true，这样才不会影响下面的计算，这里还可以进行优化，可以用DFS进行深搜，这样可以将复杂度减少至O(N)

#### 代码：

```cpp
#include <bits/stdc++.h>

using namespace std;

const int maxn = 1e5+5;
const int inf = 0x3f3f3f3f; //inf表示无穷大
int num[maxn];
int dis[maxn];
bool vis[maxn];
int n,m;

struct node // v表示终点，w表示边权
{
    int v,w;
    node(int vv,int ww):v(vv),w(ww){}
};

vector <node> e[maxn];
queue <int> q;

void add_edge(int u , int v , int w) //用来添加边
{
    e[u].push_back(node(v,w));
}

void init()   //初始化数据，对图进行添加边，连通图
{
    cin >> n >> m;
    for(int i = 0 ; i < m ; i++)
    {
        int u,v,w;
        cin >> u >> v >> w;
        add_edge(u,v,w);		//这里注意要添加两次，因为有些题目的路径是双向的
        add_edge(v,u,w);
    }
}


void spfa(int st,int ed) //st表示源点 ed表示终点
{
    fill(vis,vis+maxn,false); // 初始化vis数组为false
    fill(dis,dis+maxn,inf);	// 初始化dis数组为inf
    q.push(st);			//将起点入队
    dis[st] = 0;		
    vis[st] = true;		//标记源点
    while(!q.empty())
    {
        int u = q.front();
        q.pop();
        for(unsigned int i = 0 ; i < e[u].size() ; i++)	//遍历所有与u有连接的路线
        {
            int v = e[u][i].v;
            int w = e[u][i].w;
            if(dis[v] > dis[u] + w) //对路径进行松弛，更新最短路径
            {
                dis[v] = dis[u] + w;
                if(!vis[v])
                {
                    q.push(v); //入队标记
                    vis[v] = true;
                }
            }
        }
        vis[u] = false; //切记要把u重新标记
    }
    cout << dis[ed] << endl;
}

int main()
{
    init();
    spfa(1,n);
    return 0;
}

```

