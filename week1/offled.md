```
/*************************************************************************
    > File Name: offled.cpp
    > Author: fam
    > Mail: izjfan@136.com 
    > Created Time: 2018年09月26日 星期三 20时57分38秒
 ************************************************************************/

#include<iostream>
using namespace std;
int puzzle[6][8];   //注意pdf
int press[6][8];
bool guess()
{
	int c,r;
	for(r=1;r<5;r++)
		for(c=1;c<7;c++)	//判断按键是否需要按下（由上一个的最终状态决定）
			press[r+1][c]=(puzzle[r][c]+press[r][c]+press[r-1][c]+press[r][c-1]+press[r][c+1])%2;
	for(c=1;c<7;c++)
		for(c=1;c < 7; c++)   //判断最后一排是否可以全部灭灯
			if((press[5][c-1]+press[5][c]+press[5][c+1]+press[4][c])%2!=puzzle[5][c])
			return(false);
	return true;
}
void enumerate()
{
	int c;
	bool success;
	for(c=1;c<7;c++)
		press[1][c]=0;
	while(guess() == false)
	{
		press[1][1]++;
		c = 1;
		while(press[1][c]>1)  //第一行一次枚举，这里使用模拟二进制的方法 
		{
			press[1][c]=0;
			c++;
			press[1][c]++;
		}
	}
	return;
}
int main()
{
	int cases,i,r,c;
	for(r=0;r<6;r++)
	{
		press[r][0]=press[r][7]=0;
	}
	for(c=1;r<7;r++)
	{
		press[0][c]=0;
	}
	for(r=1;r<6;r++)
	{
		for(c=1;c<7;c++)
			cin >> puzzle[r][c];
	}
	enumerate();
	cout << "ans:" << endl;
	for(r=1;r<6;r++)
	{
		for(c=1;c<7;c++)
			cout << press[r][c] << ' ';
		cout << endl;
	}
}
```