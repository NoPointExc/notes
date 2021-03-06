MorrisTravel
----------------------------------------
我们知道，在深度搜索遍历的过程中，之所以要用递归或者是用非递归的栈方式，参考二叉树非递归中序遍历，都是因为其他的方式没法记录当前节点的parent,而如果在每个节点的结构里面加个parent 分量显然是不现实的，那么Morris是怎么解决这一问题的呢？好吧，他用得很巧妙，实际上是用叶子节点的空指针来记录当前节点的位置，然后一旦遍历到了叶子节点，发现叶子节点的右指针指向的是当前节点，那么就认为以当前节点的左子树已经遍历完成。Morris 遍历正是利用了线索二叉树 的思想。

以inorder为例，初始化当前节点为root，它的遍历规则如下：

如果当前节点为空，程序退出。  
如果当前节点非空，  
如果当前节点的左儿子为空，那么输出当前节点，当前节点重置为当前节点的右儿子。
如果当前节点的左儿子非空，找到当前节点左子树的最右叶子节点（此时最右节点的右儿子有两种情况，一种是指向当前节点，一种是为空,你也许感到奇怪，右节点的右儿子怎么可能非空，注意，这里的最右叶子节点只带的是原树中的最右叶子节点。），若其最右叶子节点为空，令其指向当前节点，将当前节点重置为其左儿子，若其最右节点指向当前节点，输出当前节点，将当前节点重置为当前节点的右儿子,并恢复树结构，即将最右节点的右节点再次设置为NULL