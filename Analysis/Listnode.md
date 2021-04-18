# 链表

## 单链表
### 结构体->动态链表
+ 动态链表new的过程比较耗费时间
``` cpp
struct ListNode{
    int val;
    ListNode* next;
};
```

### 数组模拟->静态链表

``` cpp
e[i] = node.val;
ne[i] = node.next;
nullptr = -1;
```

+ 静态链表操作
    + 在头节点后插入一个节点
    + 在第k个插入的节点(索引为k-1)后插入一个节点
    + 在第k个插入的节点后删除一个节点

``` cpp
#include <iostream>

using namespace std;

#define N 100001

// -1表示空节点，index表示当前可用的节点。
int e[N], ne[N], head = -1, index = 0;

void insert_head(int x){
    e[index] = x;
    ne[index] = head;
    head = index;
    index++;
}

void remove_at_k(int k, int x){
    ne[k] = ne[ne[k]];   
}

void insert_at_k(int k, int x){
    e[index] = x;
    ne[index] = ne[k];
    ne[k] = index;
    index++;
}

int main(){
    int m;
    cin >> m;
    while( m--){
        int x, k;
        char op;
        cin >> op;
        
        if(op == 'H'){
            cin >> x;
            insert_head(x);
        }
        else if(op == 'I'){
            cin >> k >> x;
            // 第k个插入的数的索引是确定的
            // 第k个插入的数的索引是k-1,也就是在k-1后面插入一个数
            insert_at_k(k-1, x);
        }
        else if(op == 'D'){
            cin >> k;
            // k=0 删除头节点
            // k-1<0 直接head=ne[head]
            if(!k)head=ne[head];
            // 第k个插入的数的索引是确定的
            // 删除第k个插入的数就是删除链表索引为k-1后的数
            else remove_at_k(k-1, x);
        }
        
    }
    for(int i = head; i != -1; i = ne[i]){
        cout << e[i] << ' ' ;
    }
    cout << endl;
    return 0;
    
}
```