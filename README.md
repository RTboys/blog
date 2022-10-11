# blog
this is a test blog
## 日志
### 2022/10/11 傍晚
开始考虑毕业后的事。
准备在实习和毕业前考几个二级证和专插本。
>目前专插本学习进度缓慢。

### 2022/10/7 上午
日常上午无课自学高数
>最近进度有点慢

### 2022/10/6 晚上
第一次写日志。
不知道写什么。
那就用c语音写个hello world吧。

####hello world
```
#inlcude<stdio.h>
  int main(){
  printf("hello world\n");
  return 0;
}
```

####扫雷
```
#include <stdio.h>
#include <stdlib.h>
#include <time.h>

#define ROW 9
#define COL 9
#define ROWS ROW+2
#define COLS COL+2
#define mine_count 10

void initboard(char board[ROWS][COLS],int rows,int cols,char ret){
    int i=0;
    int j=0;
    for(i=0;i<rows;i++)
    {
        for(j=0;j<cols;j++)
        {
            board[i][j]=ret;
        }
    }
}

void displayboard(char board[ROWS][COLS],int row,int col){
    int i=0;
    int j=0;
    printf("******************************\n");
    for(i=0;i<=row;i++)
        {
            printf(" %d ",i);
        }
        printf("\n");
    for(i=1;i<=row;i++)
    {   
        printf(" %d ",i);
        for(j=1;j<=col;j++)
        {
            printf(" %c ",board[i][j]);
        }
        printf("\n");
    }
    printf("******************************\n");
}

void setmine(char board[ROWS][COLS],int row,int col){
    int count=mine_count;
    while(count){
        int x=rand()%row+1;
        int y=rand()%col+1;
        if(board[x][y]=='0')
        {
            board[x][y]='1';
            count--;
        }
    }
}

int fine_mine_count(char mine[ROWS][COLS],int x,int y){
    return mine[x-1][y-1]+mine[x-1][y]+mine[x-1][y+1]+mine[x][y-1]+mine[x][y+1]+mine[x+1][y-1]+mine[x+1][y]+mine[x+1][y+1]-8*'0';
    /*or
    int i=0;
    int j=0;
    int n=0;
    for(i=-1;i<=1;i++)
    {
        for(j=-1;j<=1;j++)
        {
            if(x!=0 && y!=0)
            {
                n+=mine[x][y]-'0';
            }
        }
    }
    return n;
    */
}

void finemine(char mine[ROWS][COLS],char show[ROWS][COLS],int row,int col){
    int x=0;
    int y=0;
    int ret=0;
    int win=0;
    while (win<row*col-mine_count)
    {   
        printf("请输入坐标:>");
        scanf("%d %d",&x,&y);
        if(x>=1 && x<=row && y>=1 && y<=col)
        {
            if(mine[x][y]=='1')
            {
                printf("很抱歉,您踩到雷了\n");
                displayboard(mine,ROW,COL);
                break;
            }
            else
            {
                ret=fine_mine_count(mine,x,y);
                show[x][y]=ret+'0';
                displayboard(show,ROW,COL);
                win++;
            }
        }
    }
    if(win==row*col-mine_count)
    {
        printf("恭喜你,排雷成功\n");
        displayboard(mine,ROW,COL);
    }
}

void game(){
    char mine[ROWS][COLS];
    char show[ROWS][COLS];
    //初始化数组
    initboard(mine,ROWS,COLS,'0');
    initboard(show,ROWS,COLS,'*');
    //检查数组
    //displayboard(mine,ROW,COL);
    //displayboard(show,ROW,COL);
    //埋雷
    setmine(mine,ROW,COL);
    //用于检查是否埋雷成功
    displayboard(mine,ROW,COL);
    //打印显示用棋盘
    displayboard(show,ROW,COL);
    //找地雷
    finemine(mine,show,ROW,COL);
    
}

void menu(){
    printf("******************************\n");
    printf("**********  1.play  **********\n");
    printf("**********  0.exit  **********\n");
    printf("******************************\n");
}

void test(){
    int n=0;
    srand((unsigned int)time(NULL));
    do
    {   
        menu();
        printf("请选择:>");
        scanf("%d",&n);
        switch (n)
        {
        case 1:
        printf("扫雷:\n");
            game();
            break;
        case 0:
            printf("退出游戏\n");
            break;
        default:
            printf("输入错误，请重新输入!\n");
            break;
        }
    } while (n);
}


int main(){
    test();
    return 0;
}

```
