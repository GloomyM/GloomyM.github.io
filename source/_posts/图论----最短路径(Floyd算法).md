---
title: 最短路径(Floyd算法)
date: 2019-09-02
tags: 算法
categories: 
  - 学习历程
  - 算法
  - 最短路径
---

## 概述

Floyed-Warshall算法用来解决全源最短路径问题，简单来说就是求出任意一点c1到任意一点c2的最短路径，算法复杂度O（n<sup>3</sup>）。
## 算法描述
Floyed-Warshall算法暴力求出全源最短路径，首先选出一个转折点k，然后遍历所有节点，以k为转折在去遍历所有节点，每次询问 eij > eik + ekj ?（eij表示从i -> j的最短路径） 如果找到更短路径就直接把最短路径的长度赋给eij，三重for循环后找到全源最短路径。

```cpp
#include <bits/stdc++.h> /*Floyed-Warshall算法：算法复杂度O(N^3)
							解决全源最短路问题	
						*/
using namespace std;

const int maxn = 1e4+5;
const int inf = 0x3f3f3f3f;
int e[maxn][maxn];
int n,m;


void floyd()     				//floyd算法
{
    for(int k = 1 ; k <= n ; k++)	//k作为转折点
    {
        for(int i = 1 ; i <= n ; i++)	//遍历所有路径
        {
            for(int j = 1 ; j <= n ; j++)
            {
                if(e[i][j] > e[i][k] + e[k][j])
                    e[i][j] = e[i][k] + e[k][j];
            }
        }
    }
}

void init()	//初始化图
{			
    fill(e[0],e[0]+maxn*maxn,inf);
    cin >> n >> m;
    for(int i = 0 ; i < m ; i++)
    {
        int u,v,w;
        cin >> u >> v >> w;
        e[u][v] = e[v][u] = w; 	// 连通图
    }
}

void opt()						//输出全源最短路长度
{
    for(int i = 1 ; i <= n ; i++)
    {
        for(int j = 1 ; j <= n ; j++)
        {
            cout << e[i][j] << " ";
        }
        cout << endl;
    }
}

int main()
{
    init();
    floyd();
    opt();
    return 0;
}

```

