## 排序算法

## 二分查找树

### 概念
- 二叉查找树（Binary Search Tree），也称二叉搜索树
- 是指一棵空树或者具有下列性质的二叉树：
	- 任意节点的左子树不空，则左子树上所有结点的值均小于它的根结点的值
	- 任意节点的右子树不空，则右子树上所有结点的值均大于它的根结点的值
	- 任意节点的左、右子树也分别为二叉查找树
	- 没有键值相等的节点
- 二叉查找树相比于其他数据结构的优势
	- 查找、插入的时间复杂度较低
	- 为O(log n)
- 二叉查找树是基础性数据结构，用于构建更为抽象的数据结构
	- 集合
	- multiset
	- 关联数组

### 查找
![BST-Search](https://raw.githubusercontent.com/wu-wenxiang/Media-WebLink/master/qiniu/963d52f904cc483ba9f10b87aea9220d-BST-Search.gif)
- 在二叉搜索树b中查找x的过程为：
	- 若b是空树，则搜索失败，否则：
	- 若x等于b的根节点的数据域之值，则查找成功；否则：
	- 若x小于b的根节点的数据域之值，则搜索左子树；否则：
	- 查找右子树

### 插入
![BST-Insert](https://raw.githubusercontent.com/wu-wenxiang/Media-WebLink/master/qiniu/963d52f904cc483ba9f10b87aea9220d-BST-Insert.gif)
- 向一个二叉搜索树b中插入一个节点s的算法，过程为：
	- 若b是空树，则将s所指结点作为根节点插入，否则：
	- 若s->data等于b的根节点的数据域之值，则返回，否则：
	- 若s->data小于b的根节点的数据域之值，则把s所指节点插入到左子树中，否则：
	- 把s所指节点插入到右子树中。（新插入节点总是叶子节点）

### 建立
![List-BST](https://raw.githubusercontent.com/wu-wenxiang/Media-WebLink/master/qiniu/963d52f904cc483ba9f10b87aea9220d-BST-Build.gif)

### 转化
![BST-List](https://raw.githubusercontent.com/wu-wenxiang/Media-WebLink/master/qiniu/963d52f904cc483ba9f10b87aea9220d-BST-Translation.gif)

## 算法动图
- [visualgo.net](https://visualgo.net/zh)