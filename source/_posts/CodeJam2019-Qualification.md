---
title: CodeJam2019-Qualification
date: 2020-04-02 14:09:00
tags: 算法
---

## Foregone Solution (6pts, 10pts, 1pts)

### Problem

Someone just won the Code Jam lottery, and we owe them **N** jamcoins!  However, when we tried to print out an oversized check, we encountered a  problem. The value of **N**, which is an integer, includes at least one  digit that is a `4`... and the `4` key on the keyboard  of our oversized check printer is broken.

  Fortunately, we have a workaround: we will send our winner two checks for  positive integer amounts A and B, such that neither A nor B contains any  digit that is a `4`, and A + B = **N**. Please help us find any  pair of values A and B that satisfy these conditions.

### Input

  The first line of the input gives the number of test cases, **T**.  **T** test cases follow; each consists of one line with an integer  **N**.

### Output

  For each test case, output one line containing `Case #x: A B`,  where `x` is the test case number (starting from 1), and  `A` and `B` are positive integers as described above.

  It is guaranteed that at least one solution exists. If there are multiple  solutions, you may output any one of them. (See  "What if a test case has multiple correct solutions?" in the Competing  section of the  [FAQ](https://codingcompetitions.withgoogle.com/codejam/faq). This  information about multiple solutions will not be explicitly stated in the  remainder of the 2019 contest.)

### Limits

  1 ≤ **T** ≤ 100.
  Time limit: 10 seconds per test set.
  Memory limit: 1GB.
  At least one of the digits of **N** is a 4.

#### Test set 1 (Visible)

  1 < **N** < 105.

#### Test set 2 (Visible)

  1 < **N** < 109.

Solving the first two test sets for this problem should get you a long way toward advancing. The third test set is worth only 1 extra point, for extra fun and bragging rights!

#### Test set 3 (Hidden)

  1 < **N** < 10100.

### Sample

**Input**

3

4

940

4444

**Output**     

Case #1: 2 2

Case #2: 852 88

Case #3: 667 3777   

 In Sample Case #1, notice that A and B can be the same. The only other  possible answers are `1 3` and `3 1`.

**题目大意：**

**给出一个整数n，这个整数包含若干个4，要求将该整数转换为两个不含4的数字，答案不唯一**

**题解：**

**遍历碰到4就将4转换为1，3分别赋值给两个整数，如果不是4就赋值为0**

```cpp
#include <bits/stdc++.h>

using namespace std;

string tpl;
int k,cnt;

string fun(string s)
{
	string st = "";
	int k = 0;
	while(s[k] == '0') k++;
	for(int i = k ; i < s.length() ; i++)
		st += s[i];
	return st;
}

int main()
{
	int n;
	cin >> n;
	while(n--)
	{
		cin >> tpl;
		string s1 = "" , s2 = "";
		for(int i = 0 ; i < tpl.length(); i++)
		{
			if(tpl[i] == '4')
				s1 += '1',s2 += '3';
			else
				s1 += tpl[i],s2 += '0';
		}
		k = 0; 
		cout << "Case #" << ++cnt << ": " << s1 << " " << fun(s2) << endl;		
	}	
	return 0;
} 
```

## You Can Go Your Own Way (5pts, 9pts, 10pts)

### Problem

  You have just entered the world's easiest maze. You start in the northwest  cell of an **N** by **N** grid of unit cells, and you must reach the  southeast cell. You have only two types of moves available: a unit move to  the east, and a unit move to the south. You can move into any cell, but you  may not make a move that would cause you to leave the grid.

  You are excited to be the first in the world to solve the maze, but then  you see footprints. Your rival, Labyrinth Lydia, has already solved the maze  before you, using the same rules described above!

  As an original thinker, you do not want to reuse any of Lydia's moves.  Specifically, if her path includes a unit move from some cell A to some  adjacent cell B, your path cannot also include a move from A to B.  (However, in that case, it is OK for your path to visit A or visit B, as long  as you do not go from A to B.) Please find such a path.

  In the following picture, Lydia's path is indicated in blue, and one  possible valid path for you is indicated in orange:

### Input

  The first line of the input gives the number of test cases, **T**.  **T** test cases follow; each case consists of two lines. The first line  contains one integer **N**, giving the dimensions of the maze, as  described above. The second line contains a string **P** of 2**N** - 2  characters, each of which is either uppercase `E` (for east) or  uppercase `S` (for south), representing Lydia's valid path  through the maze.

### Output

  For each test case, output one line containing `Case #x: y`, where  `x` is the test case number (starting from 1) and `y`  is a string of 2**N** - 2 characters each of which is either uppercase  `E` (for east) or uppercase `S` (for south),  representing your valid path through the maze that does not conflict with  Lydia's path, as described above. It is guaranteed that at least one  answer exists.

### Limits

  1 ≤ **T** ≤ 100.
  Time limit: 15 seconds per test set.
  Memory limit: 1GB.
 **P** contains exactly **N** - 1 `E` characters and exactly    **N** - 1 `S` characters.

#### Test set 1 (Visible)

  2 ≤ **N** ≤ 10.

#### Test set 2 (Visible)

  2 ≤ **N** ≤ 1000.

#### Test set 3 (Hidden)

  For at most 10 cases, 2 ≤ **N** ≤ 50000.
  For all other cases, 2 ≤ **N** ≤ 10000.

### Sample

**Input** 

2

2

SE

5

EESSSESE

**Output**    

Case #1: ES 

Case #2: SEEESSES

In Sample Case #1, the maze is so small that there is only one valid  solution left for us.

Sample Case #2 corresponds to the picture above. Notice that it is acceptable  for the paths to cross.

**题目大意:**

从左上角走到右下角，且不能与Lydia走过的路重合，输出方向，答案不唯一。

**题解：**

反转Lydia所走过的道路即可

```cpp
#include<bits/stdc++.h>

using namespace std;

int n,m,cnt;
string s;

int main()
{
	cin >> n;
	for(int i = 0 ; i < n ; i++)
	{
		cin >> m;
		cin >> s;
		string st = "";
		for(int i = 0 ; i < s.length() ; i++)
		{
			if(s[i] == 'E') st += 'S';
			else st += 'E';
		}
		cout << "Case #" << ++cnt << ": " << st << endl;
	}
	return 0;
}
```

Problem Address：

[https://codingcompetitions.withgoogle.com/codejam/round/0000000000051705]: 

