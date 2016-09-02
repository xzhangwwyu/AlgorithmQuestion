##[title](https://code.google.com/codejam/contest/5254486/dashboard)
Lazy Spelling Bee
##analysis##
- input

		一个目标单词w
- output
		
		可接受的单词a定义为对于单词a的第i个字符是目标单词w的第i-1或者i或者i+1个字符，对于第1个单词和最后一个单词，进行特殊处理
		输出a的个数module 1000000009
- method

		对于w长度小于3进行特殊处理，当长度大于2时，对于w单词前i-1个字单词有n个，第位有m中选择（1,2,3）那么前i个字单词有n*m个，
		利用module算法即 m=(n*p)module k等价于m=(n module k)*（p module k） module k
##code##

```c++

		#include<stdio.h>
		#include<stdlib.h>
		#include<string.h>
		int NumberDiff(char a, char b, char c)
		{
			if (a == b)
			{
				if (a == c)
					return 1;
				else
					return 2;
			}
			else
			{
				if (a == c || b == c)
					return 2;
				else
					return 3;
			}
		}
		int main()
		{
			int num = 0;
			FILE* fp = fopen("A-large-practice.in", "r+");
			FILE* wfp = fopen("result.txt", "w+");
			fscanf(fp, "%d\n", &num);
			int count = 0;
			while (count <num)
			{
				count++;
				char buf[1024];
				fgets(buf, sizeof(buf), fp);
				int len = strlen(buf);
				while (buf[--len] == '\n')
				{
					buf[len] = '\0';
				}
				if (len == 0)
					fprintf(wfp,"Case #%d: %d\n", count, 1);
				else if (len == 1)
				{
					if (buf[0] == buf[1])
						fprintf(wfp,"Case #%d: %d\n", count, 1);
					else
						fprintf(wfp,"Case #%d: %d\n", count, 4);
				}
				else
				{
					long long result = 1;
					if (buf[0] != buf[1])
						result = 2;
					for (int i = 1;i < len;i++)
					{
						result *= NumberDiff(buf[i - 1], buf[i], buf[i + 1]);
						while (result > 1000000007)
							result -= 1000000007;
					}
					if (buf[len] != buf[len - 1])
						result *= 2;
					while (result > 1000000007)
						result -= 1000000007;
					fprintf(wfp, "Case #%d: %lld\n", count, result);
				}
			}
			return 0;
		}
```