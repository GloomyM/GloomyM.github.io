---
title: 最短路径（Dijkstra算法 + 堆优化）
date: 2019-09-02
tags: 算法
categories: 
  - 学习历程
  - 算法
  - 最短路径
---

## 概述

Dijkstra算法用于解决单源最短路径问题，也就是从某一点c1到终点c2的最短路径，但无法处理负边权情况。
未使用优先队列（堆优化）的算法复杂度为O(N<sup>2</sup>)，使用优先队列优化后的算法复杂度大概为O(NlogN),下面会一一进行介绍。

## 算法描述
Dijkstra算法可以简单的理解为广度优先搜索（BFS）加上贪心算法，因为他是从源点开始像四周搜寻路径最短的点，再从相邻的最短的点继续向四周搜索，最后找出从源点到终点的最短路径。

第一种方法，不加任何优化，朴素算法，复杂度O(N<sup>2</sup>)：
vis数组用来标记该结点是否被访问，dis用来存储每次从源点到相邻节点的最短路径长度，e数组用来连通图


```cpp
#include <bits/stdc++.h>  /*Dijkstra朴素算法：算法复杂度：O(N2)
							这里把c1当作源点，c2当作终点
						  */
const int inf = 99999999;               //inf表示无穷大，提前声明一下~偷个懒~~hh
const int maxn = 1e4+5;

bool vis[maxn];                            //vis用来标记是否访问过该点
int e[maxn][maxn],dis[maxn];                  //e邻接矩阵,dis表示从c1到每个点的路径长度


int main()
{
    int n , m , c1 , c2;               //c1,c2分别表示起点和终点
    cin >> n >> m >> c1 >> c2;
    fill(e[0],e[0]+N*N,inf);            //邻接矩阵初始化为无穷大
    fill(dis,dis+N,inf);               //初始化路径长度为无穷大
    for(int i = 0 ; i < m ; i++)
    {
        int num1,num2,road;
        cin >> num1 >> num2 >> road;
        e[num1][num2] = e[num2][num1] = road;   //连通各点连通图,这里要看清题目要求，看清路径是否互相连通
    }
    dis[c1] = 0;                              //首先把起点赋值为0
    for(int i = 0 ; i < n ; i++)
    {
        int u = -1 , minm = inf;
        for(int j = 0 ; j < n ; j++)   //每次寻找路径最短的值
        {
            if(vis[j] == false && dis[j] < minm)
            {
                minm = dis[j];
                u = j;
            }
        }
        if(u == -1)                 //如果u还为-1就说明所有点，都已经被访问
            break;
        vis[u] = true;             //标记访问
        for(int v = 0 ; v < n ; v++)
        {
            if(vis[v] == false && e[u][v] != inf)
            {
                if(dis[u] + e[u][v] < dis[v])       //如果dis[v]大于dis[u] + e[u][v] ,说明找到了更小的路径
                    dis[v] = dis[u] + e[u][v];      //更新dis[v]
            }
        }
    }
    if(dis[c2] == inf)
    	cout << "-1" << endl;		//如果终点的值为inf则说明从源点无法走到终点
    else
    	cout << dis[c2]; 				//输出从源点到终点的最短路径长度
    return 0;
}
```
这种朴素算法的弊端就是，当数据个数超过1e5之后，这种算法就无法解决问题了，因此我们需要第二种方法，对Dijkstra算法进行堆优化，优化后的算法复杂度为O(NlogN)。

```cpp
#include <bits/stdc++.h>  	/*Dijkstra算法堆优化：算法复杂度：O(NlogN)
							代码里把源点当作1，终点当作n，可根据题目要求自行修改
							*/
using namespace std;

const int maxn = 1e4+5;
const int inf = 0x3f3f3f3f;
bool vis[maxn];
int dis[maxn];
int c1,c2;

struct node
{
    int u;			//u用来存储点
    int w;			//w用来存储边的权值
    node(int x,int y) : u(x) , w(y){}
    bool operator <(const node &r)const
    {
        return w > r.w;
    }
};

vector <node> e[maxn];

void add_edge(int u , int v , int w)	//用于每次添加边
{
    e[u].push_back(node(v,w));
}

void dijkstra(int st)
{
    fill(vis,vis+maxn,false);
    fill(dis,dis+maxn,inf);
    priority_queue <node> pque;
    dis[st] = 0;
    pque.push(node(st,0));
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
            if(!vis[v] && dis[v] > dis[u] + w)
            {
                dis[v] = dis[u] + w;
                pque.push(node(v,dis[v]));
            }
        }
    }
}

int main()
{
    int n,m;			//n代表一共有多少个节点，m表示一共有多少路径
    cin >> n >> m;
    for(int i = 1 ; i <= m ; i++)
    {
        int u,v,w;
        cin >> u >> v >> w;
        add_edge(u,v,w);		//向图内添加边，用来连通图
        add_edge(v,u,w);
    }
    dijkstra(1);			//我这里默认每次的源点都是1
    if(dis[n] == inf)		//如果dis[n]为inf表示从源点1到终点n无法连通，也就不存在最短路径
        cout << "-1";
    else
        cout << dis[n] << endl;
    return 0;
}
```
比较两种算法的运行时间（图1是朴素算法，图二是堆优化后的算法）：
图一：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190902171640315.png)
图二：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190902171755990.png)
`数据个数大于1e5的题目需要使用堆优化后的算法来简化复杂度`