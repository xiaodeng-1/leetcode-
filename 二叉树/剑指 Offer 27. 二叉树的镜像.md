二叉树的镜像

## 题目描述
请完成一个函数，输入一个二叉树，该函数输出它的镜像。

例如输入：

​     4

   /   \
  2     7
 / \   / \
1   3 6   9
镜像输出：

​     4

   /   \
  7     2
 / \   / \
9   6 3   1


## 示例1
```
输入：root = [4,2,7,1,3,6,9]
输出：[4,7,2,9,6,3,1]
```
## 思路一：递归
二叉树中最常用的方法就是递归法，一定要掌握递归法。   

根据二叉树镜像的定义，考虑递归遍历（dfs）二叉树，交换每个节点的左 / 右子节点，即可生成二叉树的镜像。 

递归解析：
终止条件： 当节点 root为空时（即越过叶节点），则返回 null   
递推工作：
  	初始化节点tmp ，用于暂存 root的左子节点；  
 	 开启递归 右子节点 mirrorTree(root.right)，并将返回值作为  root 的 左子节点 。  
  	开启递归 左子节点 mirrorTree(tmp)，并将返回值作为 root的右子节点 。  
  	返回值： 返回当前节点 root；  



## 代码

```python3
class Solution:
    def mirrorTree(self, root: TreeNode) -> TreeNode:
        if not root:return
        temp = root.left
        root.left = self.mirrorTree(root.right)
        root.right = self.mirrorTree(temp)
        return root
```

复杂度分析：  
时间复杂度 O(N) ： 其中 NN 为二叉树的节点数量，建立二叉树镜像需要遍历树的所有节点，占用 O(N) 时间。  
空间复杂度 O(N) ： 最差情况下（当二叉树退化为链表），递归时系统需使用 O(N)大小的栈空间。  

## 思路二：借助栈

利用栈（或队列）遍历树的所有节点 node ，并交换每个 nodenode 的左 / 右子节点。  
算法流程：  
	特例处理： 当 root为空时，直接返回 null；  
	初始化： 栈（或队列），本文用栈，并加入根节点 root。  
	循环交换： 当栈 stack 为空时跳出；  
	出栈： 记为 node ；  
	添加子节点： 将 node左和右子节点入栈；  
	交换： 交换 node 的左 / 右子节点。  
	返回值： 返回根节点 root。  

## 代码

```
#借助辅助栈
class Solution:
    def mirrorTree(self, root: TreeNode) -> TreeNode:
        if not root:return
        stack = [root]
        while stack:
            node = stack.pop()
            if node.left:stack.append(node.left)
            if node.right:stack.append(node.right)
            node.left,node.right = node.right,node.left
        return root
```

复杂度分析：  
时间复杂度 O(N) ： 其中 NN 为二叉树的节点数量，建立二叉树镜像需要遍历树的所有节点，占用 O(N) 时间。  
空间复杂度 O(N) ： 最差情况下（当为满二叉树时），栈 stack 最多同时存储 N/2个节点，占用 O(N) 额外空间  

