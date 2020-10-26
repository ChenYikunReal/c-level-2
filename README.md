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
