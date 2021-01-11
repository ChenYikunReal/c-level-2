# 计算机二级C语言程序设计

![](/c.jpg)

说明：
- 搞这个训练只是为了C语言课练题刷GPA，不是为了考计算机二级。
- 考虑到C语言一个project只能有一个可执行的main()，所以干脆把code写到Markdown里，代码会测试的。

## 刷题笔记

1.字符串转整数（限于long long）：
```c
#include <stdio.h>
#include <string.h>

int main() {
    printf("请输入一个整数：");
    char num[30];
    scanf("%s", num);
    int flag = 1, i = 0, len = strlen(num);
    if (num[0] == '-') {
        flag = 0;
        i++;
    }
    long long result = 0;
    for (; i < len; i++) {
        result *= 10;
        result += (num[i]-'0');
    }
    printf("结果为：%lld", flag ? result : -result);
    return 0;
}
```

2.创建长为m的带头结点的单链表，赋值0~m-1：
```c
#include <stdio.h>
#include <stdlib.h>

typedef struct Node Node;

struct Node {
    int value;
    Node *next;
};

Node *createLink(int m) {
    int size = sizeof(Node);
    Node *list = malloc(size);
    Node *temp = list;
    for (int i = 0; i < m; i++) {
        Node *newNode = malloc(size);
        newNode->value = i;
        temp->next = newNode;
        temp = temp->next;
    }
    return list;
}

int main() {
    Node *list = createLink(10), *temp = list;
    for (int i = 0; i < 10; i++) {
        temp = temp->next;
        printf("%d\n", temp->value);
    }
    // 没free
    return 0;
}
```

3.统计一个字符串中单词个数，单词间隔为至少一个空格，单词全是小写字母：
```c
#include <stdio.h>
#include <string.h>

int main() {
    char line[] = "red   math pow    help typetype";
    int len = strlen(line), ptr = 0;
    char temp[len];
    for (int i = 0; i < len; i++) {
        if (line[i] == ' ') {
            if (temp[0] != '\0') {
                printf("%s\n", temp);
                temp[0] = '\0';
                ptr = 0;
            }
        } else {
            temp[ptr] = line[i];
            ptr++;
            temp[ptr] = '\0';
        }
    }
    if (temp[0] != '\0') {
        printf("%s\n", temp);
    }
    return 0;
}
```

4.十进制数转二进制数：
```c
#include <stdio.h>

int main() {
    int a[20], n, i;
    printf("请输入一个十进制数：");
    scanf("%d", &n);
    for (i = 0; n > 0; i++){
        a[i] = n % 2;
        n /= 2;
    }
    printf("对应的二进制数是：");
    for(i = i - 1; i >= 0; i--) {
        printf("%d", a[i]);
    }
    return 0;
}
```

5.正整数逐位编程one、two、three……：
```c
#include <stdio.h>

int main() {
    long int n, sum = 0, r;
    printf("请输入一个正整数：");
    scanf("%ld", &n);
    while(n > 0) {
        r = n % 10;
        sum = sum * 10 + r;
        n /= 10;
    }
    n = sum;
    while(n > 0) {
        r = n % 10;
        switch(r) {
            case 1:
                printf("one ");
                break;
            case 2:
                printf("two ");
                break;
            case 3:
                printf("three ");
                break;
            case 4:
                printf("four ");
                break;
            case 5:
                printf("five ");
                break;
            case 6:
                printf("six ");
                break;
            case 7:
                printf("seven ");
                break;
            case 8:
                printf("eight ");
                break;
            case 9:
                printf("nine ");
                break;
            case 0:
                printf("zero ");
                break;
            default:
                printf("tttt");
                break;
        }
        n /= 10;
    }
    return 0;
}
```

6.打印阶乘三角形：
```c
#include <stdio.h>

int main() {
    int a = 0, b = 1, i, c, n, j;
    printf("请输入一个正整数：");
    scanf("%d", &n);
    for (i = 1; i <= n; i++) {
        a = 0;
        b = 1;
        printf("%4d ", b);
        for (j = 1; j < i; j++) {
            c = a + b;
            printf("%4d ",c);
            a = b;
            b = c;
        }
        printf("\n");
    }
    return 0;
}
```

7.输出数值递增三角：
```c
#include <stdio.h>

int main() {
    int i, j, k, l, n;
    printf("请输入一个正整数：");
    scanf("%d", &n);
    for (i = 1; i <= n; i++) {
        for (j = 1; j <= n-i; j++) {
            printf(" ");
        }
        for (k = 1; k <= i; k++) {
            printf("%d", k);
        }
        for (l = i-1; l >= 1; l--) {
            printf("%d", l);
        }
        printf("\n");
    }
    return 0;
}
```

8.输出大写字母递增三角：
```c
#include <stdio.h>

int main() {
    int i, j, k, m, n;
    int ch = 65;
    printf("请输入一个正整数：");
    scanf("%d", &n);
    for (i = 1; i <= n; i++) {
        for (j = n; j >= i; j--) {
            printf(" ");
        }
        for (k = 1; k <= i; k++) {
            printf("%c", ch++);
        }
        ch--;
        for (m = 1; m < i; m++) {
            printf("%c", --ch);
        }
        printf("\n");
        ch=65;
    }
    return 0;
}
```

9.蒙特卡洛方法估计π：
```c
#include <stdio.h>
#include <stdlib.h>
#include <math.h>

int main() {
    int intP, intCircle, intSquare, intToss, intRM, i;
    float fltPi, fltX, fltY, fltR;
    char ch;
    intRM = RAND_MAX;
    do {
        intCircle = 0;
        do {
            printf("Enteer the number of tosses (2 <= N <= 500) : ");
            scanf("%d", &intToss);
        } while (intToss < 2 || intToss > 5000);
        intSquare = intToss;
        for (i = 0; i < intToss; i++) {
            intP = rand();
            fltX = (float) intP / intRM;
            intP = rand();
            fltY = (float) intP / intRM;
            fltR = sqrt(fltX * fltX + fltY * fltY);
            if (fltR <= 1) {
                intCircle++;
            }
        }
        fltPi = 4 * (float)intCircle / intSquare;
        printf("the value of pi is : %f\n", fltPi);
        printf("Do you want to continue ? (Y/N) : ");
        scanf("%c", &ch);
    } while (ch == 'y' || ch == 'Y');
    printf("Thank you!\n");
    return 0;
}
```

10.八皇后问题求解：
```c
#include <stdio.h>
#include <math.h>

void queen(int row, int p);

int chess[8], count;

int main() {
    int p = 8;
    queen(1, p);
    return 0;
}

void print(int p) {
    int i, j;
    char ch;
    printf("\n\nThis is Solution No.%d\n\n", ++count);
    for(i = 1; i <= p; i++) {
        printf("\t%d", i);
    }
    for(i = 1; i <= p; i++) {
        printf("\n\n%d", i);
        for (j = 1; j <= p; j++) {
            if (chess[i] == j) {
                printf("\tQ");
            } else {
                printf("\t-");
            }
        }
    }
    printf("\n\n\nThere are total 92 solutions for 8-queens problem.");
    printf("\nStrike Enter key to continue : ");
    scanf("%c", &ch);
}

int place(int row, int column) {
    int i;
    for (i = 1; i <= row; i++) {
        if (chess[i] == column || abs(chess-column) == abs(i-row)) {
            return 0;
        }
    }
    return 1;
}

void queen(int row, int p) {
    int column;
    for (column = 1; column <= p; column++) {
        if (place(row, column)) {
            chess[row] = column;
            if (row == p) {
                print(p);
            } else {
                queen(row+1, p);
            }
        }
    }
}
```

11.下面程序的输出结果是：`x=14,y=4`
```c
#include <stdio.h>

int main()
{
    int x=10,y=5;
    switch(x)
    {
        case 1:x++;
        default: x+=y;
        case 2:y--;
        case 3:x--;
    }
    printf("x=%d,y=%d",x,y);
    return 0;
}
```
说明：如果不break，则匹配一次成功后的都会执行。

12.下面程序的输出结果是：`####`
```c
#include <stdio.h>

int main()
{
    int x=3,y=0,z=0;
    if(x=y+z)
        printf("****");
    else
        printf("####");
    return 0;
}
```
说明：之前误以为赋值成功则必为真，现在才发现应该是赋值不为0则必为真。

13.下面程序的输出结果是：`2`
```c
#include <stdio.h>

int main()
{
    int a=2,b=1,c=0;
    if(a>=b){
        switch(a++,b++)
        {
            case 1:
                c=a;
            case 0:
                c=b;break;
            default:
                c=0;
        }
    }
    printf("%d",c);
    return 0;
}
```
说明：一则是在switch条件判断的时候出现了++则a和b的值会改变，另一方面应用到case时a++和b++输出的只有原先的a和b。由于出现了逗号运算符，所以实际switch的是b的原值。进入case先匹配了1但是没有break，会再次匹配2，但是原先对c的赋值便不作数了，此后break。

14.统计输入字符串中大小写字母的个数：
```c
#include <stdio.h>
#include <string.h>
#include <ctype.h>

int main() {
    char str[128];
    gets(str);
    int length = strlen(str), counter = 0;
    for (int i = 0; i < length; i++) {
        if (isalpha(str[i])) {
            counter++;
        }
    }
    printf("%d", counter);
    return 0;
}
```

15.从键盘依次输入的M个整数倒序输出：
```c
#include <stdio.h>

int main() {
    int n;
    printf("请输入整数个数：\n");
    scanf("%d", &n);
    int nums[n];
    for (int i = 0; i < n; i++) {
        scanf("%d", &nums[i]);
    }
    for (int i = n-1; i >= 0; i--) {
        printf("%d ", nums[i]);
    }
    return 0;
}
```

16.键盘输入两个整数，以及一个运算符进行运算（输入格式为`1+2`，输出格式为`1+2=3`）：
```c
#include <stdio.h>

int main() {
    int a, b;
    char operator;
    scanf("%d%c%d", &a, &operator, &b);
    switch (operator) {
        case '+':
            printf("%d%c%d=%d", a, operator, b, a+b);
            break;
        case '-':
            printf("%d%c%d=%d", a, operator, b, a-b);
            break;
        case '*':
            printf("%d%c%d=%d", a, operator, b, a*b);
            break;
        case '/':
            if (b == 0) {
                printf("Divide Error!");
            } else {
                printf("%d%c%d=%d", a, operator, b, a/b);
            }
            break;
        case '%':
            if (b == 0) {
                printf("Mod Error!");
            } else {
                printf("%d%c%d=%d", a, operator, b, a%b);
            }
            break;
    }
    return 0;
}
```

17.统计201~300之间的所有素数并统计总个数：
```c
#include <stdio.h>

int main() {
    int counter = 0;
    for (int i = 201; i <= 300; i++) {
        int flag = 1;
        for (int j = 2; j < i; j++) {
            if (i % j == 0) {
                flag = 0;
                break;
            }
        }
        if (flag) {
            printf("%d ", i);
            counter++;
        }
    }
    printf("\n%d", counter);
    return 0;
}
```

18.统计输入字符串中大写字母的个数：
```c
#include <stdio.h>
#include <string.h>
#include <ctype.h>

int main() {
    char str[128];
    gets(str);
    int length = strlen(str), counter = 0;
    for (int i = 0; i < length; i++) {
        if (isupper(str[i])) {
            counter++;
        }
    }
    printf("%d", counter);
    return 0;
}
```

19.从键盘依次输入的M个整数并输出其中的偶数：
```c
#include <stdio.h>

int main() {
    int n, temp;
    printf("请输入整数个数：\n");
    scanf("%d", &n);
    for (int i = 0; i < n; i++) {
        scanf("%d", &temp);
        if (temp % 2 == 0) {
            printf("%d ", temp);
        }
    }
    return 0;
}
```

20.输出如下三角形：
```text
        *
      * * *
    * * * * *
  * * * * * * *
* * * * * * * * *
```
代码如下：
```c
#include <stdio.h>

int main() {
    for (int i = 1; i <= 5; i++) {
        for (int j = 5-i; j > 0; j--) {
            printf("  ");
        }
        for (int j = 0; j < 2*i-1; j++) {
            printf("* ");
        }
        printf("\n");
    }
    return 0;
}
```

21.假设公鸡2元、母鸡1元、小鸡0.5元，求百钱买百鸡的解决方案：
```c
#include <stdio.h>

int main() {
    for (int i = 0; i <= 50; i++) {
        // 至多100只鸡
        for (int j = 0; j <= 100-i; j++) {
            if (i*4 + j*2 + (100-i-j)*1 == 200) {
                printf("%d %d %d\n", i, j, (100-i-j));
            }
        }
    }
    return 0;
}
```
