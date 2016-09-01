##[title](http://code.google.com/codejam/contest/351101/dashboard#s=p2)##
- T9 Spelling

##analysis##
- input

&emsp;&emsp;输入a-z和空格的字符串

- output

&emsp;&emsp;输出为对应的数字键，当数字键和前一个数字键相同时，使用空格隔开

- method

&emsp;&emsp;对每个字符进行硬编码，记录前一次的输出字符串第一个字符是否和当前的字符串第一个字符相同，如果相同则添加空格，否则直接输出

##code##

```C++

	#include<stdio.h>
	#include<stdlib.h>
	#include<string.h>
	#include<limits.h>
	
	char* buf[128];
	int main()
	{
		printf("INT_MAX=%d\n", INT_MAX);
		memset(buf, 0, sizeof(buf));
		buf[' '] = "0";
		buf['a'] = "2";
		buf['b'] = "22";
		buf['c'] = "222";
		buf['d'] = "3";
		buf['e'] = "33";
		buf['f'] = "333";
		buf['g'] = "4";
		buf['h'] = "44";
		buf['i'] = "444";
		buf['j'] = "5";
		buf['k'] = "55";
		buf['l'] = "555";
		buf['m'] = "6";
		buf['n'] = "66";
		buf['o'] = "666";
		buf['p'] = "7";
		buf['q'] = "77";
		buf['r'] = "777";
		buf['s'] = "7777";
		buf['t'] = "8";
		buf['u'] = "88";
		buf['v'] = "888";
		buf['w'] = "9";
		buf['x'] = "99";
		buf['y'] = "999";
		buf['z'] = "9999";
	
		FILE*fp = fopen("C-large-practice.in", "r");
		FILE*wfp = fopen("result.txt", "w+");
		int num = 0;
		fscanf(fp, "%d", &num);
		printf("num=%d\n", num);
		int count = 1;
		char bufmes[1001];
		char bufresult[4048];
		char* pre, *curr;
		fgets(bufmes, sizeof(bufmes), fp);
		while (count <= num)
		{
			pre = "-";
			fgets(bufmes, sizeof(bufmes), fp);
			//printf("count=%d：%s\n",count, bufmes);
			char* cursor = bufresult;
			for (char* i = bufmes;*i != '\n'&&*i;i++)
			{
				curr = buf[*i];
				//printf("curr=%s\n", curr);
				if (curr[0] == pre[0])
					*cursor++ = ' ';
				for (char* j = curr;*j;)
					*cursor++ = *j++;
				pre = curr;
			}
			*cursor = '\0';
			fprintf(wfp,"Case #%d: %s\n", count, bufresult);
			//printf("Case #%d: %s\n", count, bufresult);
			count++;
		}
		fclose(fp);
		fclose(wfp);
	
	}
```