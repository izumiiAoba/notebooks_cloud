### 题目

输出水仙花数。输入一个正整数 n（3 ≦ n ≦ 7），输出所有的 n 位水仙花数。水仙花数是指一个n位的正整数，它的各位数字的n次幂之和等于它本身。例如：153。

### 解题思路

- 不是去找,是去穷举然后验证是不是水仙花数
- 迭代

### 错解

```c
#include<stdio.h>
#include<math.h>
int main (void){
    int n,k,m;
    float i,max,sum=0;
    printf("Enter n\n");
    scanf("%d",&n);
    max=pow(10.0,n)-1;
    for(i=pow(10.0,n-1);i<=max;i++){
        m=(int)i;
        for(k=1;k<=n;k++){
            sum+=pow((float)(m%10),n);
            m=m/ 10;
        }
        if(sum==i)
            printf("%.0f",i);
    }
    return 0;
}
```

### 错误分析

在第一层循环的时候，每测试一个数都没把sum置零。

### 正解

```c
#include<stdio.h>
#include<math.h>
int main (void){
    int n,k,m;
    float i,max,sum;
    printf("Enter n: ");
    scanf("%d",&n);
    max = pow(10.0,n)-1;
    for(i=pow(10.0,n-1);i<=max;i++){
    	sum = 0;
        m = (int)i;
        for(k=1;k<=n;k++){
            sum+=pow((float)(m%10),n);
            m=m/ 10;
        }
        if(sum==i)
            printf("%.0f",i);
    }
    return 0;
}
```

