# 保留n位小数

## c++:

<font color="#dd0000" size=5>使用fixed和setprecision</font>

```c++
#include<iostream> 
#include <iomanip>//头文件
using namespace std;
int main()
{
    int n;
    cin>>n;
    cout << fixed << setprecision(n)<<3.141529<endl;
}
```

## c:

```c
printf("%.2f\n", 3.141529);

```

   


# 并查集

~~~c++
int f(int x)
{
    if (x == fa[x])
    {
        return x;
    }
    return fa[x] = f(fa[x]);
}
~~~

## 并查集[啊哈算法](https://bbs.codeaha.com/forum.php?mod=viewthread&tid=11223)



# 用二进制存储数据（与或运算的应用）



## [题目](http://xujcoj.com/Home/Problems/status/pro_id/1528)

## 代码：



```c++
#include<bits/stdc++.h>
using namespace std;
typedef long long ll;
int re[1000100];
int g[32];
int main()
{
	int n;
	cin >> n;
	while (n--)
	{
		
		int m;
		cin >> m;
		for(int j=0;j<m;j++)
		{
			int q = 0;
			int a;
			cin >> a;
			for (int i = 0; i < a; i++)
			{
				int b;
				cin >> b;
				q = (q | (1 << b));
			}
			re[j] = q;
		}
		int p;
		cin >> p;
		for (int i = 0; i < p; i++)
		{
			int sum = 0;
			int q = 0;
			int b;
			cin >> b;
			while (b--)
			{
				int dj;
				cin >> dj;
				q = q | (1 << dj);
			}
			for (int j = 0; j < m; j++)
			{
				if ((q & re[j]) == q)
				{
					sum++;
				}
			}
			g[i] = sum;
		}
		for (int i = 0; i < p; i++)
		{
			if (i > 0)
			{
				cout << " ";
			}
			cout << g[i];
		}
		cout << endl;
	}
}
```




