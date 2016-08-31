##[title](http://code.google.com/codejam/contest/351101/dashboard#s=p0)##
- Store Credit


##analysis##
- input

&emsp;&emsp;第一行是测试样例N，第二行表示第一个测试样例的信用数目，第三行表示商店商品数目，第四行表示每个商品的价格

- output

&emsp;&emsp;输出两个商品的下标，使其满足商品价格之和为拥有的现金数，并且下标是最小的

- method

&emsp;&emsp;由于价格有限制，所以可以将价格作为索引，创建一个结构体，此结构体存储是否有此价格flag，以及此价格对应的下标（最多存储两个），通过遍历价格存储，并且遍历价格进行查找，需要2*n的时间，n为商品数目

##code##

```c++

	#include<stdio.h>
	#include<stdlib.h>
	#include<string.h>

	typedef struct
	{
		bool flag;
		int index[2] ;
	}node;
	node nd[1001];
	
	int main()
	{
		FILE* fp = fopen("A-small-practice.in", "r");
		FILE* wfp = fopen("result.txt", "w+");
		int count = 0;
		memset(nd, 0, sizeof(nd));
		fscanf(fp, "%d", &count);
		int cnt = 1;
		while (cnt<=count)
		{
			int total = 0;
			fscanf(fp,"%d", &total);
			int num = 0;
			fscanf(fp, "%d", &num);
			int* price = (int*)malloc(sizeof(int)*(num+1));
			for (int i = 1;i <=num;i++)
			{
				fscanf(fp, "%d", price + i);
				if (!(nd[price[i]].flag))
				{
					nd[price[i]].flag = true;
					nd[price[i]].index[0] = i;
				}
				else if (nd[price[i]].flag&&(nd[price[i]].index[1] == 0))
					nd[price[i]].index[1] = i;
			}
			int index1 = 0, index2 = 0;
			for (int i = 1;i <= num;i++)
			{
				index1 = i;
				int temp = total - price[i];
				if (temp < 0 || temp>1000)
					continue;
				if (temp == price[i] && nd[temp].index[1] != 0)
				{
					index2 = nd[temp].index[1];
					break;
				}
				else if (temp != price[i]&&nd[temp].flag)
				{
					index2 = nd[temp].index[0];
					break;
				}				
			}
			fprintf(wfp,"Case #%d: %d %d\n", cnt, index1, index2);
			for (int i = 1;i <= num;i++)
			{
				nd[price[i]].flag = 0;
				nd[price[i]].index[0] = 0;
				nd[price[i]].index[1] = 0;
			}
			free(price);
			cnt++;
		}
		fclose(fp);
		return 0;
	}
