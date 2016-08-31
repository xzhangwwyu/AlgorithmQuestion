##[tittle](http://code.google.com/codejam/contest/351101/dashboard#s=p1)##
- Reverse Words

##analysis##

- input

&emsp;&emsp;第一行为测试样例的个数n，每一个测试样例是由单词和空格组成的字符串

- output

&emsp;&emsp;输出为将每个测试样例按单词的顺序反向输出

- method

&emsp;&emsp;将整个字符串逆转，再根据每个单词逆转，然后将其输出，注意要去掉\n

##code##

```c++

	#include<stdio.h>
	#include<stdlib.h>
	#include<string.h>
	
	char buf[1024];
	
	
	int main()
	{
		FILE* fp = fopen("B-large-practice.in", "r+");
		FILE* wfp = fopen("result.txt", "w+");
		int num = 0;
		fscanf(fp, "%d\n", &num);
		int cnt = 1;
		printf("num=%d\n", num);
		while (cnt<=num)
		{
			if (!fgets(buf, 1024, fp))
			{
				perror("error!\n");
				break;
			}
			
			int len = strlen(buf);
			while (buf[--len] == '\n')
				buf[len] = '\0';
			printf("len=%d\n", len);
			printf("cnt=%d line=%s\n", cnt, buf);
			int start = 0, end = len;
			while (start < end)
			{
				char temp = buf[start];
				buf[start] = buf[end];
				buf[end] = temp;
				start++;
				end--;
			}
			printf("cnt=%d line=%s\n", cnt, buf);
			int cur = 0;
			start = 0;
			while (1)
			{
				if (buf[cur] == '\0')
					break;
				while (buf[cur] == ' ')
					cur++;
				start = cur;
				while (buf[cur] != ' '&&buf[cur]!='\0')
					cur++;
				end = cur - 1;
				while (start < end)
				{
					char temp = buf[start];
					buf[start] = buf[end];
					buf[end] = temp;
					start++;
					end--;
				}
			}
			fprintf(wfp,"Case #%d: %s\n", cnt,buf);
			cnt++;
		}
		return 0;
	}
```