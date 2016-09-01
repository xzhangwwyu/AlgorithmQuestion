##[title](https://leetcode.com/problems/triangle/)##
Triangle
##analysis##
- input 

		输入三角形的二维数组
- output

		输出最小和，其中最小和的规则：最小和路径，每行只要一个，每次向下移动时下标必须使相邻的
- method

		从下向上开始计算，第i行每个元素形成的最小和为sum[i][k]=min{sum[i+1][k]+triangle[i][k],sum[i+1][k]+triangle[i][k+1]},所以使用原位运算，并使用n个位置记录路径信息

##code##

```c++

		class Solution {
		public:
		    int minimumTotal(vector<vector<int>>& triangle) {
		        for(int i=triangle.size()-2;i>=0;i--)
		        {
		            for(int j=triangle[i].size()-1;j>=0;j--)
		            {
		                if(triangle[i+1][j]<triangle[i+1][j+1])
		                {
		                    triangle[i][j]+=triangle[i+1][j];
		                }
		                else
		                {
		                    triangle[i][j]+=triangle[i+1][j+1];
		                }
		            }
		        }
		        return triangle[0][0];
		    }
		};
```