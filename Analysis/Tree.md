# 树
## 基础知识
- [x] [树的基础知识](#树的基础知识)
- [x] [二叉树的基础知识](#二叉树的基础知识)
- [x] [二叉树的存储与建立](#二叉树的存储与建立)
- [x] [二叉树结点的查找与插入](#二叉树结点的查找与插入)
- [x] [二叉查找树(BST)](#二叉查找树BST)
- [x] [平衡二叉树AVL树](#平衡二叉树AVL树)
- [x] [平衡二叉树的插入](#平衡二叉树的插入)
- [x] [并查集](#并查集)
- [x] [堆的基础知识](#堆的基础知识)
- [x] [堆添加一个新元素](#堆添加一个新元素)
- [x] [堆排序](#堆排序)
- [x] [哈夫曼树](#哈夫曼树)
- [x] [二叉树的遍历](#二叉树的遍历)

## 树的基础知识
+ 树的静态存储：用数组表示所有子树的索引。
``` cpp
struct node {
    int data;
    vector<int> child;
}
```
+ 树的先根遍历

``` cpp
void PreOrder(int root){
    cout << Node[root].data << " ";
    for(int i = 0; i < Node[root].child.size(); ++i){
        PreOrder(Node[root].child[i]);
    }
}
```

## 二叉树的基础知识
+ 二叉树的基本知识
二叉树与度为2的树的区别，二叉树严格区分左右树
+ 二叉树的递归定义
  + 边界条件：二叉树没有根节点，是一棵空树
  + 递归式：二叉树由根节点，左右子树组成，且左右子树都是二叉树。
+ 满二叉树
  + 每一层节点个数都达到了当前层能达到的最大节点数。
+ 完全二叉树
  + 除最后一层外，其余层的节点个数都达到了当前层能达到的最大结点数。
最后一层存在从左到右的连续若干结点。
### 二叉树的存储与建立
+ 二叉链表
``` cpp
typedef struct Node{
    char data;
    Node *left, *right;
}
```
+ 二叉树的建立-递归建树
``` cpp
void creatTree(Node* &root){
	char data;
	cin>>data;
	if(data=='#')
		root=nullptr;
	else{
		root=new Node;
		root->data=data;
		creatTree(root->left);
		creatTree(root->right);
	}
}
```
### 二叉树结点的查找与插入
+ 二叉树结点的查找与插入
    递归插入结点：
    递归边界：遇到空节点，插入结点。
    递归条件：左子树搜索，右子树搜索。
    tip:$root = NULL$表示结点不存在，而$*root = NULL$表示结点内容不存在
``` cpp
void search(node* root, int x, int newdata){
    if(root == nullptr){
        return;
    }
    if(root -> data == x){
        root -> data = newdata;
    }
    search(root -> left, x, newdata);
    search(root -> right, x, newdata);
}
```

### 二叉树的遍历
+ 二叉树的遍历
  + 先序遍历：**先处理根节点**;。序列的第一个元素一定是根节点。
  + 中序遍历：**先处理左子树**，后访问根节点。知道根节点可以确定左右子树。
  + 后序遍历：**先处理左右子树**，后访问根节点。序列的最后一个元素一定是根节点
  + 因此，知道先序遍历(或后序遍历)和**中序遍历**可以重建二叉树。
+ 先序：第一次遇到就访问
+ 中序：第二次遇到访问
+ 后序：第二次遇到访问
**递归写法**  
+ 先序遍历
``` cpp
void preTravel(Node* root){

	if(root==nullptr) return;
	pvisit(root);
	preTravel(root->left);
	preTravel(root->right);
}
```
+ 中序遍历
``` cpp
void midTravel(Node *root){
    if(root == nullptr)
        return;
    midTravel(root -> left);
    pvisit(root);
    midTravel(root -> right);
}
```
+ 后序遍历
``` cpp
void postTravel(Node* root){
    if(root == nullptr)
        return;
    postTravel(root -> left);
    postTravel(root -> right);
    pvisit(root);
}
```
**非递归遍历-难理解**  
+ 先序遍历:通用模板化简版本
``` python
class Solution:
    def preorderTraversal(self, root: TreeNode) -> List[int]:
        if not root:
            return []
        stack = [root]
        res = []
        while stack:
            root = stack.pop()
            res.append(root.val)
            if root.right:
                stack.append(root.right)
            if root.left:
                stack.append(root.left)
        return res
```
+ **统一的迭代写法**
+ 用栈模拟，**先访问谁**，**谁后入栈**
+ **先序**
``` cpp
class Solution {
public:
    vector<int> preorderTraversal(TreeNode* root) {
        vector<int> result;
        stack<TreeNode*> st;
        if (root != NULL) st.push(root);
        while (!st.empty()) {
            TreeNode* node = st.top();
            if (node != NULL) {
                st.pop();
                if (node->right) st.push(node->right);  // 右
                if (node->left) st.push(node->left);    // 左
                st.push(node);                          // 中
                st.push(NULL);
            } else {
                st.pop();
                node = st.top();
                st.pop();
                result.push_back(node->val);
            }
        }
        return result;
    }
};
```
+ **中序**
  
``` cpp
class Solution {
public:
    vector<int> inorderTraversal(TreeNode* root) {
        vector<int> result;
        stack<TreeNode*> st;
        if (root != NULL) st.push(root);
        while (!st.empty()) {
            TreeNode* node = st.top();
            if (node != NULL) {
                st.pop(); // 将该节点弹出，避免重复操作，下面再将右中左节点添加到栈中
                if (node->right) st.push(node->right);  // 添加右节点（空节点不入栈）

                st.push(node);                          // 添加中节点
                st.push(NULL); // 中节点访问过，但是还没有处理，加入空节点做为标记。

                if (node->left) st.push(node->left);    // 添加左节点（空节点不入栈）
            } else { // 只有遇到空节点的时候，才将下一个节点放进结果集
                st.pop();           // 将空节点弹出
                node = st.top();    // 重新取出栈中元素
                st.pop();
                result.push_back(node->val); // 加入到结果集
            }
        }
        return result;
    }
};
```
+ **后序**

``` cpp
class Solution {
public:
    vector<int> postorderTraversal(TreeNode* root) {
        vector<int> result;
        stack<TreeNode*> st;
        if (root != NULL) st.push(root);
        while (!st.empty()) {
            TreeNode* node = st.top();
            if (node != NULL) {
                st.pop();
                st.push(node);                          // 中
                st.push(NULL);

                if (node->right) st.push(node->right);  // 右
                if (node->left) st.push(node->left);    // 左

            } else {
                st.pop();
                node = st.top();
                st.pop();
                result.push_back(node->val);
            }
        }
        return result;
    }
};
```
**BFS层序遍历**
``` cpp
void broadTravel(Node* root){
	queue<Node*> que;
	if(root == nullptr)
		return;
	que.push(root);
	Node *p;
	while(!que.empty()){
		p = que.front();
		pvisit(p);
		que.pop();
		if(p -> left) que.push(p -> left);
		if(p -> right) que.push(p -> right);
	} 
}
```

## 二叉查找树BST
**定义**
+ 二叉查找树由根节点和左右子树组成，且左右子树都是二叉查找树。
+ 左子树数据小于根节点，右子树数据大于根节点。
+ 左子树$\leq$ 根节点 $\leq$ 右子树
+ 二叉查找树的**中序**遍历是有序的。

**基本操作**

+ 查找：递归查找-可以根据查找树特性进行优化。
+ 插入：在树中查找不到的位置就是需要插入的位置。
### 二叉查找树的删除操作
+ 时间复杂度是$O(h)$，$h$为查找树的高度。
+ 删除一个节点有两种方式-左子树的最大节点作为新节点(前驱)，右子树的最小节点作为新节点(后继)。
+ 删除过程
  + 查找节点
  + 查找到节点删除节点
    + 首先处理特殊情况-如果欲删除结点是叶结点，直接将叶结点地址设为NULL，释放叶结点内存。
    + 如果非叶结点，使用前驱或后继的方式，删除节点不用改变节点间关系。只需要将欲删除节点的数据域的内容使用前驱结点的内容替代，递归删除前驱结点即可。
``` cpp
void deleteNode(Node* &root, int x){
    if(root == nullptr)
        return;
    if(root -> data == x){
        if(root -> left != nullptr){ //左子树找最大值
            Node* pre = findMax(root -> left);
            root -> data = pre -> data;
            deleteNode(root -> left, pre -> data)
        }else{
            Node* pre = findMax(root -> right);
            root -> data = pre -> data;
            deleteNode(root -> right, pre -> data);
        }
    }else if(root -> data > x){
        deleteNode(root -> left, x);
    }else{
        deleteNode(root -> right, x);
    }
}
```
######
### 平衡二叉树AVL树
+ 平衡二叉树是是仍是二叉查找树。
+ 平衡因子-左右子树的高度之差。
+ 平衡二叉树的平衡因子时刻小于2，因此平衡二叉树的高度可以保持在$O(logn)$。

**节点定义**
AVL树结点需要记录结点的高度。
``` cpp
struct Node{
    int data, height;
    Node *left, *right;
}
```
获取节点高度
``` cpp
int getHeight(Node* root){
    if(root == nullptr)
        return 0;
    return root -> height;
}
```
获取平衡因子
``` cpp
int getBalanceFactor(Node* root){
    return getHeight(root -> left) - getHeight(root -> right);
}
```
更新结点高度
``` cpp
void4 getBalanceFactor(Node* root){
    root -> height = max (getHeight(root -> left), getHeight(root -> right)) + 1;
}
```
**平衡二叉树的查找**
平衡二叉树的查找与二叉查找树完全相同，时间复杂度为$O(logn)$。


## 平衡二叉树的插入
> 图片参考:https://blog.csdn.net/fxkcsdn/article/details/81674653


首先定义：右节点-右子树的根节点，左节点-左子树的根节点。

**左旋**
+ 用右节点代替树的根节点。右节点的左子树变为原根节点的右子树。
``` cpp
void L(Node* root){
    Node* temp = root -> right;
    root -> right = temp -> left;
    temp -> left = root;
    updateHeight(root);
    updateHeight(temp);
    return temp;
}
```
**右旋**
+ 用左节点代替树的根节点。左节点的右子树变为原根节点的左子树。
``` cpp
void R(Node* root){
    Node* temp = root -> left;
    root -> left = temp -> right;
    temp -> right = root;
    updateHeight(root);
    updateHeight(temp);
    return temp;
}
```
**平衡二叉树的插入**
+ 只要把最靠近的失衡结点调整正常，路径上所有的结点都会平衡。
+ 根据失衡情况可分为4种情况$LL, LR, RL, RR$，图解参考算法笔记324
+ $LL:$右旋根节点。
+ $LR:$先转换为$LL$。
+ $RR:$左旋根节点。
+ $RL:$先转换为$RR$。

``` cpp
void insert(Node* &root, int v){
    if(root == nullptr){
        root = newNode(v);
        return;
    }
    if(v < root -> v){
        insert(root -> left, v);
        updateHeight(root);
        if(getBalanceFactor(root) == 2){
            if(getBalanceFactor(root -> left) == 1) //LL
            {
                R(root);
            }else if(getBalanceFactor(root -> left) == -1){  //LR
                L(root -> left);
                R(root);
            }
        }
    }else{
        insert(root -> right, v);
        updateHeight(root);
        if(getBalanceFactor(root) == -2){
            if(getBalanceFactor(root -> right) == -1) //RR
            {
                L(root);
            }else if(getBalanceFactor(root -> right) == 1){ //RL
                R(root -> right);
                L(root);
            }
        }
    }
}
```

## 并查集
**Union,Find,Set**

- 并查集包含Union,Find,Set3个关键词，是一种维护集合的基本操作。
- 并查集由两个任务：
- **合并**：合并两个集合。
  **查找**：判断两个元素是否在一个集合内。
- 实现：数组实现，索引表示结点编号，数组的值表示索引的根节点。
同一个集合中只能包含一个**根节点(father[i] = i)**。

+ 查找父节点

``` cpp
int findFather(int x, int father[]){
    while(x != father[x]){
        x = father[x];
    }
    return x;
}
```

+ 合并结点
  + 一定要使用根节点进行合并。
  + 查找它们的根节点，如果他们根节点不同，则属于不同的集合才可以进行合并。

``` cpp
void Union(int a, int b, int father[]){
    int faA = findFather(a);
    int faB = findFather(b);

    if(faA != faB){
        father[faB] = faA;
    }
}
```

+ 路径压缩
  + 把当前查询结点的路径上所有节点的父亲都指向根节点。
``` cpp
int findFatherBetter(int x, int father[]){
    int a = x;
    while(x != father[x]){
        x = father[x];
    }
    while(a != father[x]){
        int temp = father[a];
        father[a] = x;
        a = temp;
    }
    return x;
}
```

## 堆的基础知识
> + 堆是一颗完全二叉树。
> + 大顶堆：父亲结点的值大于左右子树的结点。
> + 小顶堆：父亲结点的值小于左右子树的结点。

**cpp优先队列初始化过程**
``` cpp
1 //升序队列，小顶堆
2 priority_queue <int,vector<int>,greater<int> > q;
3 //降序队列，大顶堆
4 priority_queue <int,vector<int>,less<int> >q;
```

**初始化堆**
使用数组静态表示堆$heap[i]$从1开始，
该节点左孩子为$heap[2i]$,该节点右孩子为$heap[2i+1]$。
``` cpp
const int maxn = 100;
int heap[maxn], n = 10;
```

### 建堆过程与删除堆顶元素
> + **插入建堆**->自上而下(向上调整)，等同于堆中插入新元素。
> + **调整建堆**->自下而上(向下调整)，全部初始化后进行调整。
+ 首先按照完全二叉树建立初始堆。
  **向下调整**：将当前结点与左右孩子比较。直到将该节点向下调整至合适位置。(向下调整时间复杂度为O(logn))
+ 对非叶子结点,**从下往上**($i<n/2$)进行向下调整。建堆时间复杂度为O(n)。
``` cpp
// 其中low是想要调整元素的下标，high是整个堆长度。
// O(logn)
// 向下调整->建立最大堆
void downAdjust(int low, int high){
    int i = low, j = i * 2;
    while(j <= high){
        // 如果右孩子存在，选取左右孩子中最大的
        if(j + 1 <= high && heap[j] < heap[j+1]){
            j = j + 1;
        }
        // 如果孩子结点比欲调整节点大
        if(heap[j] > heap[i]){
            // 交换孩子结点
            swap(heap[i], heap[j]);
            i = j;
            j = 2 * i;
        }else{
            // 如果孩子权值比根节点小，调整结束。
            break;
        }
    }
}
void creatHeap(){
    for(int i = n/2; i >= 1; i--){
        downAdjust(i, n);
    }
}
```
**删除堆顶元素**
用最后一个元素覆盖堆顶元素，并且删除最后一个元素。之后向下调整堆顶元素。
``` cpp
// 删除堆顶元素
void deleteHeap(){
    // 用最后一个元素替代堆顶元素并且删除最后一个元素
    heap[1] = heap[n--];
    downAdjust(1, n);
}
```

### 堆添加一个新元素
+ 将添加的元素放在堆的最后，之后向上调整该元素，也可以用这种方式建堆。
  + **向上调整**：把欲调整节点与其父亲节点比较，直到其小于父亲节点。时间复杂度O(logn)。
+ 将欲添加元素添加至堆的最后。
+ 将该元素向上调整至合适的位置。
``` cpp
//high 表示待调整的元素
void upAdjust(int low, int high){
    int i = high, int j = i / 2;
    while(j > low){
        if(heap[j] > heap[i]){
            swap(heap[j], heap[i]);
            // 继续向上调整
            i = j;
            j = j / 2;
        }else{
            break;
        }
    }
}
// 添加元素
void insert(int x){
    heap[++n] = x;
    upAdjust(1, n);
}
```

### 堆排序
> 类似于选择排序，每次从堆中将堆顶元素拿出来放入有序序列，然后对堆进行调整。
``` cpp
void heapSort(){
    creatHeap();
    for(int i = n;i > 1; i--){
        // 删除堆顶元素，将堆顶元素放入有序数组。
        swap(heap[1], heap[i]);
        // 向下调整
        downAdjust(1, i);
        // heap最后为从小到大排序
    }
}
```

## 哈夫曼树
+ 结点带权路径长度
  + 结点的权值乘以其路径长度(到根节点经过的边数)
  + **树的带权路径长度是所有叶结点带权路径长度之和**。
+ 带权路径长度最小的树。
+ 哈夫曼树建树思想
  + 反复选择两个权值最小的结点进行合并(包括新合并产生的结点)，直到只剩下一个元素(根节点)。
  + 使用最小堆，每次选择最小的两个元素。合并后，将新产生的结点加入堆中。
+ 哈夫曼编码
  + 哈夫曼编码是一种前缀编码(0/1编码)，某个词的编码不会作为另外一个词的前缀。

**合并果子问题**
``` cpp
#include<cstdio>
#include<algorithm>
using namespace std;
// 小顶堆
priority_queue<int, vector<int>, greater<int>> q;

int main(){
    int n;
    int temp, x, y, ans = 0;
    scanf("%d", &n);
    for(int i = 0; i < n; i++){
        scanf("%d", &temp);
        q.push(temp);
    }
    while(q.size() > 1){
        x = q.top();
        q.pop();
        y = q.top();
        q.pop();
        q.push(x+y);
        ans += x + y;
    }
    printf("%d", ans);
    return 0;
}
```






## 字典树

+ [208.实现Trie(前缀树)](https://leetcode-cn.com/problems/implement-trie-prefix-tree/)


### 概念
普通树节点
``` cpp
struct Treenode{
	int val;//节点值
	Treenode children[MAX_NUM];//节点儿子
}
```
+ 字典树节点：用儿子节点编号是否存在表示父亲节点的可选值。
+ isEnd表示在该节点处是否存在一个完整串。
+ 儿子节点为26个，每个节点编号代表当前节点的字母值。
+ 如果根节点isEnd=True，表示存在一个空字符串
+ 如果根节点children[0],children[1]存在，则有首字母为a，b的串。
``` cpp
struct Treenode{
	bool isEnd;//当前节点是否是一个完整串的结尾
	Treenode children[26];//字母映射表
}
```
+ Tries中一般有大量的空节点。
### 插入操作
+ 遍历输入的字符串
+ 如果当前节点的可选值中不包含该字符，新建一个节点接入对应子节点。
+ 否则，该节点向对应字符节点移动
+ 将字符串最后一个元素对应节点的序号节点的isEnd标记为True

``` python
def insert(self, word: str) -> None:
		node = self
		for ch in word:
				ch = ord(ch) - ord("a")
				if not node.children[ch]:
						node.children[ch] = Trie()
				node = node.children[ch]
		# 标记字符串结束
		node.isEnd = True
```

### 查询全串匹配
+ 遍历输入的字符串
+ 如果当前节点的可选值中不包含该字符，返回False
+ 否则，该节点向对应字符节点移动
+ 字符串最后一个元素对应节点的序号节点的isEnd为True，全串匹配，否则不匹配。

``` python
    def search(self, word: str) -> bool:
        """
        Returns if the word is in the trie.
        """
        node = self
        for ch in word:
            ch = ord(ch) - ord("a")
            if not node.children[ch]:
                return False
            node = node.children[ch]
        if node.isEnd == True:
            return True
        else:
            return False
```

### 查询前缀匹配
+ 遍历输入的字符串
+ 如果当前节点的可选值中不包含该字符，返回False
+ 否则，该节点向对应字符节点移动

``` python
		 def startsWith(self, prefix: str) -> bool:
				"""
				Returns if there is any word in the trie that starts with the given prefix.
				"""
				node = self
				for ch in prefix:
						ch = ord(ch) - ord("a")
						if not node.children[ch]:
								return False
						node = node.children[ch]
				return True
```

### 复杂度分析：
+ 时间复杂度：初始化O(1)，其余操作（插入，查询）O(|S|)，|S|为字符串长度。
+ 空间复杂度：$O(T*\sigma)$,T为所有字符串长度之和。
+ 前缀树使得查询速度只与单词的长度有关，而跟单词的数量无关。

### 代码实现

``` python
class Trie:

    def __init__(self):
        """
        Initialize your data structure here.
        """
        # 26个字母映射
        # 一次建树多次查询
        self.children = [None] * 26
        self.isEnd = False


    def insert(self, word: str) -> None:
        """
        Inserts a word into the trie.
        """
        node = self
        for ch in word:
            ch = ord(ch) - ord("a")
            if not node.children[ch]:
                node.children[ch] = Trie()
            node = node.children[ch]
        # 标记字符串结束
        node.isEnd = True


    def search(self, word: str) -> bool:
        """
        Returns if the word is in the trie.
        """
        node = self
        for ch in word:
            ch = ord(ch) - ord("a")
            if not node.children[ch]:
                return False
            node = node.children[ch]
        if node.isEnd == True:
            return True
        else:
            return False

    def startsWith(self, prefix: str) -> bool:
        """
        Returns if there is any word in the trie that starts with the given prefix.
        """
        node = self
        for ch in prefix:
            ch = ord(ch) - ord("a")
            if not node.children[ch]:
                return False
            node = node.children[ch]
        return True
```

``` cpp
class Trie {
public:
    /** Initialize your data structure here. */
    Trie(): isEnd(false), children(26, nullptr){}
    bool isEnd;
    vector<Trie *> children;
    /** Inserts a word into the trie. */
    void insert(string word) {
        Trie* root = this;
        for(auto chh: word){
            int ch = chh - 'a';
            if(root->children[ch] == nullptr){
                root->children[ch] = new Trie();
            }
            root = root->children[ch];
        }
        root->isEnd = true;
    }
    
    /** Returns if the word is in the trie. */
    bool search(string word) {
        Trie* root = this;
        for(auto chh: word){
            int ch = chh - 'a';
            if(root->children[ch] == nullptr){
                return false;
            }
            root = root->children[ch];
        }
        if(root->isEnd){
            return true;
        }
        else{
            return false;
        }
    }
    
    /** Returns if there is any word in the trie that starts with the given prefix. */
    bool startsWith(string prefix) {
        Trie* root = this;
        for(auto chh: prefix){
            int ch = chh - 'a';
            if(root->children[ch] == nullptr){
                return false;
            }
            root = root->children[ch];
        }
        return true;
    }
};
```

