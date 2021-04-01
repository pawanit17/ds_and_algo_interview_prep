**Complexities**
- O(N) means that the algorithm needs N in growth.
- O(N) determines that it is atleast N in growth.

**Abstract Data Type**
- Representing a user defined data type in layman terms is ADT.
- ADT defines what type of operations can be done, what behavior is exhibited by this data type etc.
- Ex: Stack

**Linked Lists vs Arrays**
LLs help in storing more amount of data as there is not hard requirement for storing them in continous memory locations. Arrays fail here.
Arrays are faster and lets you access a given element at an index. LLs do not have that feasibility.

# Linked Lists

![image](https://user-images.githubusercontent.com/42272776/112369014-bbca1980-8d01-11eb-948f-d62dfdc61615.png)

## Representation
```
struct node {
  int data;
  struct node* next;
} *list = NULL;
```

## :dart: How to find if a Linked List has a loop?.
- Maintain two pointers with unequal increment and make them iterate. If they meet at any point, there is a loop.
- O(1) space complexity and O(N) time complexity.

## :dart: How to find starting point of the loop?.
- Continuation to the problem above.
- Initialize q to head and p to meeting point and increment both by a single step. The node on which they meet is the beginning of the loop.

## :dart: How to find the 'k'th node from the end in a Linked List?.
- Add an external counter on the number of nodes in the Linked list.
  - Needs update during addition and deletion.
- Maintain two pointers with an increment of 1 but after a distance of 'k'.
- O(1) space complexity and O(N) time complexity.

## :dart: Adding a node to a sorted linked list
- Initialize ```temp``` to beginning of the list
- Iterate while the input number is less than that of the current node's data field.
- Insert adjusting pointers
  - ```temp->next = ptr->next```
  - ```ptr->next = temp```
- Time complexity (N) and space complexiy O(1).

## :dart: Print the contents of an Linked List in the reverse manner?.

Time Complexity: O(N)
Space Complexity: O(N)
```
void printInReverse( Node* head )
{
  if( head == NULL ) return;
  printInReverse( head->next );
  printf( head->data );
  return;
}
```

## :dart: How to achieve O(1) access time for Linked Lists?.
- Maintain a seperate HashTable - < Integer Index to Memory Address or Object >
- Every addition/removal to the Linked List should be registered in the HashTable
- Adds extra space complexity of O(N)
- Adds extra processing of O(N) for maintaining this cache

## :dart: Finding the common merging point of two Linked Lists

- Use Two stacks
  - Time complexity O(M+N)
  - Space complexity O(M+N)
  
- Use a single Hashtable
  - Time complexity O(M+N)
  - Space complexity O(M) or O(N)

- Use pointers
  - Get size of two Linked Lists
  - Move pointer of the smaller Linked List by |M-N|
  - Move each of the two pointers one step at the time
  - Their meeting point is the merge location
  - Time complexity O(M+N)
  - Space complexity O(1)

## :dart: How to get previous nodes if the HEAD is at Kth node in a Linked List
- Not possible with conventional linked lists.
- XOR Linked Lists to be employed
- Each node maintains an XOR information of the previous and next Node's address
- They are XORed with the other node ( either the previous or the next node ) to get the other node
- Time Complexity O(N)
- Space Complexity O(1)
- Logic:
  ```
  Node *curNode = head;
  Node *prevNode = NULL;

  while( true ) {
    prevNode = curNode->npx ^ curNode->next;

    if( prevNode == NULL ) {
    // head = prevNode
    break;
    }

    printf( prevNode->data );
    curNode = prevNode;
  }
  ```

## :dart: How to check if the Linked List is a Palindrome

- Pointer Increments
  - Maintain two pointer approach to get Mid of the linked list and the size
  - Adjust accordingly for odd/even to get to proper Mid
  - Iterate with increment of one for Head and Mid
  - Start comparing them
  - Time Complexity: O(N)
  - Space Complexity: O(1)

- Using Reversing
  - Get the middle of the linked list
  - Reverse the second half of the linked list
  - Compare the first and second half of the lists
  - Construct the linked list again after re-reversing
  - Time Complexity: O(N)
  - Space Complexity: O(1)
  - This alters the linked list. This is not a practical solution.

## Circulate Linked Lists(Open)
## :dart: Reverse Linked Lists(Open)
## :dart: Replace adjacent nodes in a Linked List(Open)

# Stacks
## Usecases
- Code editors for matching braces, XML elements
- Method calls, recursions

## Representation
```
struct node {
  int data;
  struct node* link;
} *stack = NULL;
```

## :dart: How to get the maximum value in a Stack in O(1) time complexity
- Maintain a secondary stack that will hold the largest value till the same index in the corresponding Stack.
- Time Complexity - O(N) for building the stack, but once built, getting Max value is O(1).
- Space Complexity - O(N).

## :dart: How to store two stacks in an array
- Have the first stack grow left and the other grow right.

## :dart: How to store k stacks in an array of size m
- Each m/k section of the array should be a stack
- Whenever a stack reaches size m/k, then it reached its alloted size
## :dart: How to sort the elements in the Stack using push, pop, peek?.(Open)

## :dart: How to reverse the elements in the stack using push and pop?.(Open)

# Recursion
## :dart: Check if the content of the array is a palindrome
```
bool isPalindrome( int arr, int len, int index ) {
    if( index > len/2 )
    return true;

    return arr[index] == arr[len-1-index] && isPalindrome( arr, len, index + 1 );
}
```

## :dart: Check if the Array sum is even
```
bool isEvenSum( int arr, int len, int index, int sum ) {
    if( index == len )
        if( sum % 2 == 0 ) return true;
        return false;
    
    return isEven( arr, len, index + 1, sum + arr[index] );
}
```

# Hashing
- Mapping from key to value.
- Typically either Open Hashing or Closed Hashing.
- Closed Hashing
  - The values are stored in the array itself.
  - So more memory is needed.
  - A hash function is used to transform a key value to an index within the Hash table.
  - Collisions are always possible and can be dealt with one of the approaches below.
  - Linear probing, Quadratic probing, double hashing - each comes with their problems like clustering, slowness etc.
- Open Hashing
  - In this case, the values are stored in a seperate linked list.
  - When two keys are mapped to the same location, they are writeen to a sorted linked list.
  - In this case, the HashTable will hold the addresses to linked lists and not the content itself and so need lesser memory.
 ![image](https://user-images.githubusercontent.com/42272776/112218216-7c3ff680-8c49-11eb-8052-49322108d806.png)

# Trees
- Non-linear datastructure
- Has faster search time compared to Stacks or Queues or Linked Lists

# Binary Trees

![image](https://user-images.githubusercontent.com/42272776/112368937-9dfcb480-8d01-11eb-8a29-59cee97b4df5.png)

If every node in a Tree has atmost two children, it is a binary tree
- Maximum number of nodes at any level is 2^i
- Maximum nodes for a binary tree of height h is 2^h - 1
- Minimum number of nodes possible in a binary tree of height h is equal to h
- If there are n nodes, you can create a binary tree with minimum height of log(n+1) or a 
  maximum height of node
  
## Extended Binary Trees
All the leaf nodes have different types of nodes.

## Strictly Binary Tree
All nodes have either zero children or two children. No node with a single child.

## Complete Binary Tree
All levels have maximum number of nodes except possibly the last level.

## Full Binary Tree
A binary tree with maximum number of nodes.

## Implementation
- Array implementation is not efficient.
  - Only useful completely if the binary tree is full.
  - Constrained by memory limit and so not suitable for larger trees.
  - Dynamic memory representation is better.

```
struct node {
  struct node* left;
  int data;
  struct node* right;
} *root = NULL;
```
## :dart: Printing contents of a Binary Tree
  - Inorder L, Ro, R
  ```
  void printInOrder( struct Node* root ) {
  
    if( root == NULL ) return;

    printInOrder( root->left );
    print( root->data );
    printInOrder( root->right );
  }
  ```
  
  - Preorder Ro, L, R
  ```
  void printPreOrder( struct Node* root ) {
  
    if( root == NULL ) return;

    print( root->data );
    printPreOrder( root->left );
    printPreOrder( root->right );
  }
  ```
  
  - Postorder L, R, Ro
  ```
  void printPostOrder( struct Node* root ) {
  
    if( root == NULL ) return;

    printPostOrder( root->left );
    printPostOrder( root->right );
    print( root->data );
  }
  ```

- Print the maximum depth of a binary tree
```
int maxDepth( struct Node* root ) {

  if( root == NULL ) return 0;
  
  int leftMaxDepth = 1 + maxDepth( root->left );
  int rightMaxDepth = 1 + maxDepth( root->right );
  
  return Max( leftMaxDepth, rightMaxDepth );
}
```

## :dart: Find the width of a binary tree(Open)



## Create Binary Tree from inorder and preorder or inorder and postorder traversals(Open)

# Binary Search Tree
![image](https://user-images.githubusercontent.com/42272776/112369196-ed42e500-8d01-11eb-94de-f8301b39cf91.png)

BST is a BT where nodes are sorted to facilitate easier searches.
At each iteration half of the tree can be discarded making the search space smaller.

## :dart: Creating a BST from a list of number
- Call the below method incrementally for each of the elements in the list
```
struct TreeNode* buildBST( struct TreeNode* root, int data ) {
  if( root == NULL ) {
    root = (struct TreeNode*)malloc(sizeof(struct TreeNode));
    root->info = data;
    root->lchild = NULL;
    root->rchild = NULL;
    return root;
  }
  else if( root->info < data ) {
    root->right = buildBST( root->right, data );
  }
  else {
    root->left = buildBST( root->left, data );
  }
  return root;
}
```

## :dart: Search in a BST
```
struct Node* searchRecursively( struct Node* root, int data ) {

  if( root == null )
  return null;

  if( root->info == data ) {
    return root;
  }
  else if( root->info < data ) {
    // Search in Right Sub Tree
    return searchRecursively( root->rchild );
  }
  else {
    // Search in Left Sub Tree
    return searchRecursively( root->lchild );
  }
}
```

### :dart: Adding in a BST
```
struct Node* add( struct Node* root, int data ) {

  if( root == null ) {
    root = (struct Node*)malloc(sizeof(struct Node));
    root->info = data;
    root->lchild = NULL;
    root->rchild = NULL;
  }

  if( root->info == data ) {
    // Duplicate key being inserted case
    return root;
  }
  else if( root->info < data ) {
    // Search in Right Sub Tree
    return searchRecursively( root->rchild );
  }
  else {
    // Search in Left Sub Tree
    return searchRecursively( root->lchild );
  }
}
```

## :dart: Deletion in a BST
- Case 1: Node being deleted is leaf
  - In this case, just set the pointer of parent to NULL.
  - Delete the node.
- Case 2: Node being deleted has one child
  - In this case, replace the node being deleted with its child ( right or left subtree )
  - Delete the node.
- Case 3: Node being deleted has two childs
  - Replace the node being deleted with its inorder successor or inorder predecessor
  - Delete the node.

## :dart: Finding the largest / smallest element in the BST
Largest will the right most element in the right subtree and the smallest will be the left most element in the left subtree.
Time complexity is O(h), where h is the height of the tree.

- Smallest
```
while( lChild->left != NULL )
lChild = lChild->left;
printf( lChild->data );
```
- Largest
```
while( rChild->right != NULL )
rChild = rChild->right;
printf( rChild->data );
```

# Threaded Binary Trees
![image](https://user-images.githubusercontent.com/42272776/112369128-ddc39c00-8d01-11eb-9264-fee80df693fe.png)

In a Binary Tree, the leaves do not have the use of the rChild and lChild fields. Also, traversal in tree can be improved with quick references.
These fields of children can be tweaked to point to their inorder predecessor or inoder successor for better performance.
Such type of trees as shown above are called as Threaded Binary Trees.

```
struct ThreadedNode {
  struct ThreadedNode* left;
  boolean lThread;
  int info;
  struct ThreadedNode* right;
  boolean rThread;
}
```

# AVL Trees
- AVL Trees are self balancing trees. This helps in performing the search operation in a BST optimally.
- A random insertion without maintenance into a BST results in a BST that is never balanced. In the worst case, this causes the search time to slip from O(logN) to O(N).
![image](https://user-images.githubusercontent.com/42272776/112682926-c964d800-8e96-11eb-892e-ffcda3e48c13.png)

- AVL tree works by balancing the right and left subtrees if the difference between their heights at any level is more than 1.
- This ensures that the BST is balanced. This delta is referred to as Balance Factor.
- After every insert or deletion from an AVL tree, the heights at each node from the new node all the way to the root node has to be calculated.
- If the delta is more than 1, then restructuring has to happen.
- Easiest way to understand this restructing is as follows:
  - Identify the node where this delta exceeds 1
  - Pick the median value from that node to the place where the newly added node is. ( This distance will be atmost 3 nodes ).
  - The median value becomes the new root of that subtree and the other two nodes become the left and right subtrees.
  - Adjust their children accordingly.
  - Continue with the next insertion or deletion.

- Following snippets are a manual workthrough for these scenario:
## Insertion into an AVL Tree
- ![AVL Tree Insertion](https://user-images.githubusercontent.com/42272776/112682593-50fe1700-8e96-11eb-9a0f-a5b8f6d62aac.jpeg)

## Deletion from an AVL Tree
- ![AVL Tree Deletion](https://user-images.githubusercontent.com/42272776/112682595-522f4400-8e96-11eb-99a5-58452cc63043.jpeg)

Time complexity is O(logN).

# Heap (Open Revisit)
Heap is a Tree that has two properties:
1. It is an almost complete binary tree.
2. Every element in a subtree is smaller - maxheap or larger - minheap than its children.

A heap is never a binary search tree.

## Implementation
O(log N) and O(N) approach

# Splay Trees
- A BST in which the most frequently queried data is splayed to appear closer to the root.
- Splaying is moving the data that you searched for to the root of the tree to reduce search time.
- If it happens to be the root, then querying that data the next time is O(1).
- In general the search complexity is O(log N).
- But the process of splaying involved left and right rotations to the tree which may even cause the tree to be skewed to one side.
- In such cases, the search may degrade to O(N).
- In general, the following cases arise:
  - Root Element: No splaying needed
  - Child of Root Element: Either a right rotation or a left rotation
  - Has a grandparent and current node, its parent and its grand parent are all on the same side: Two left rotations or two right rotations
  - Has a grandparent and current node, its parent and its grand parent are on diferent sides: Two rotations are needing, in which one is left and the other is right.

![Splay Trees](https://user-images.githubusercontent.com/42272776/113131515-f1f42580-923a-11eb-8717-a78c1012f534.jpg)

# Treap
https://en.wikipedia.org/wiki/Treap

# Trie
https://en.wikipedia.org/wiki/Trie

# Suffix Trees
https://en.wikipedia.org/wiki/Suffix_tree

# Tournament Tree
https://en.wikipedia.org/wiki/K-way_merge_algorithm#Tournament_Tree

# Disk Organization
Logically a disk looks like this:
- It is made up of concentric circles and sectors
- The intersection is called as Block.
- READ / WRITE to disk is always in Block.
- Typically each block is 512 bytes
- Offsets are used to get the address of a particular byte within the Block.
  - Ex: 17th byte in a block is at ```( block's starting address + 16 )```
  - Offset varies from 0 to 511.
- To get to a specific block, we need the cyclinder information, the track information and the sector information.
- By spinning the sectors are changed and by moving the READ/WRITE Head, the tracks are changed.
![image](https://user-images.githubusercontent.com/42272776/112713228-3493c600-8efa-11eb-9dfb-d0e894d5a48f.png)

- Having a multi level index drastically reduces the number of look ups / blocks to seek.
![Multi Level Index](https://user-images.githubusercontent.com/42272776/112715910-3f098c00-8f09-11eb-85d1-d172c3088200.jpg)

READ: https://stackoverflow.com/questions/1108/how-does-database-indexing-work#:~:text=Indexing%20is%20a%20way%20of,to%20be%20performed%20on%20it.

# Multi-way search trees
- Multi way search trees are extensions of Binary search trees.
- Each node can contain more than 1 key. Infact as many as you need, but once defined all nodes contain atmost that amount of keys.
- An M-way search tree has M-1 keys in a node and M paths from it.
- So a 2-way search tree is a Binary search tree.
![image](https://user-images.githubusercontent.com/42272776/112716249-3914aa80-8f0b-11eb-9c5c-1190c697ea34.png)

- Most implementations have an extra pointer field that points to the actual record.
- Drawback of these trees is that there is no formal definition on whether keys are to be populated first in a node or if the childrent are to be created first in the tree.
- That is where a formalized Multi way tree, called B-Trees are introduced.

# B-Trees
- Every node needs to have CEIL(M/2) nodes.
- Root can have minimum two children / minimum one key.
- All leaves must be at the same level.
- Creation process is bottom up.
- https://www.youtube.com/watch?v=aZjYr87r1b8

# B+ Trees
- B Tree to begin with
- Record pointers will only be available in Leaf node only.
- Keys are duplicated in leaf nodes.
- Leaf nodes are connected via links like a linked list.
![B Tree and B+ Trees](https://user-images.githubusercontent.com/42272776/112728821-1c01cb00-8f4f-11eb-954e-aa64948cca6d.jpg)


# :dart: Problems on Trees
## How to find the largest element in a Binary Tree
```
int getLargetInBinaryTree( struct node* root ) {
    if( root == NULL ) {
        return IN_MIN;
    }
    
    int lMax = getLargestInBinaryTree( root->left );
    int nodeValue = root->data;
    int rMax = getLargestInBinaryTree( root->right );
    
    return max( lMax, nodeValue, rMax );
}
```
Time Complexity: O(N)
Space Complexity: O(N)

## How to find the number of nodes in a Binary Tree
```
int getNodeCountInBinaryTree( struct node* root ) {
    if( root == NULL ) {
        return 0;
    }
    
    int lMax = getNodeCountInBinaryTree( root->left );
    int rMax = getNodeCountInBinaryTree( root->right );
    
    // 1 is for the current node.
    return lMax + 1 + rMax;
}
```
Time Complexity: O(N)
Space Complexity: O(N)

## How to find the sum of all nodes in a Binary Tree
```
int getNodeCountInBinaryTree( struct node* root ) {
    if( root == NULL ) {
        return 0;
    }
    
    int lMax = getNodeCountInBinaryTree( root->left );
    int rMax = getNodeCountInBinaryTree( root->right );
    
    return lMax + root->data + rMax;
}
```
Time Complexity: O(N)
Space Complexity: O(N)

## How do you search in a Binary Tree
```
boolean search( struct node* root, int searchKey ) {
  if( root == NULL ) {
    return false;
  }
  
  if( root->data == searchKey ) {
    return true;
  }
  
  return search( root->left, searchKey ) || search( root->right, searchKey );
}
```
Time Complexity: O(N)
Space Complexity: O(N)

## How would you achieve level order traversal of a Tree
- Use a queue
- Add the root to it
- While the queue is not empty
  - Dequeue from Queue
  - Print the Dequeued element
  - Get the children of the element
  - Enqueue them to the queue
Time Complexity: O(N)
Space Complexity: O(N)

## Search in a Binary Tree / Add in a Binary Tree
- Use the level order traversal as discussed above
- If you want to add, add at the first instance where a node does not have either LST or RST.
- This can be understood by ptr->lChild being NULL or ptr->rChild being NULL.

## Print the levels in reverse in a Binary Tree
- Use both a Stack and a Queue
- Queue is used for level traversal
- When you pop element from Queue, add it to the stack.
- Once done, pop all the elements from the Stack.

![Reverse Level Order](https://user-images.githubusercontent.com/42272776/112762505-9b5dd000-901d-11eb-945a-536be9b5493c.jpg)

## Delete Tree
- Post order traversal is the only traversal that is fit for Tree deletion.
- Ex:

```
struct Tree* deleteTree( struct Tree* root ) {

  // If this is a LEAF node, then delete it.
  if( root->left == NULL && root->right ==  NULL ) {
     free( root );
     root = NULL;
     return root;
  }
  
  root->lChild = deleteTree( root->lChild );
  root->rChild = deleteTree( root->rChild );
  return root;
}
```
Time Complexity: O(N)
Space Complexity: O(N)

## Number of Leaf nodes, single child nodes and complete nodes

```
int numLeaves( struct Tree* root ) {
  // Change this condition according to what you want to find - leaves, half child nodes, complete nodes.
  if( root->lChild == NULL && root->rChild == NULL ) {
    return 1;  
  }
  if( root == NULL ) {
    return 0;
  }
  return numLeaves( root->lChild ) + numLeaves( root->rChild );
}
```
Time Complexity: O(N)
Space Complexity: O(N)

# How to check if two Binary Trees are identical?.

```
bool areTreesIdentical( struct TreeNode* root1, struct TreeNode* root2 ) {
  if( root1 == NULL && root2 == NULL ) {
    return true;
  }

  if( root1 == NULL || root2 == NULL ) {
    return false;
  }
  
  bool leftTreeIdentical = areTreesIdentical( root1->lChild, root2->lChild );
  bool rightTreeIdentical = areTreesIdentical( root1->rChild, root2->rChild );
  bool currentNodeIdentical = root1->data == root2->data;

  // The LST, the current node and the RST have to be identical.
  return leftTreeIdentical && currentNodeIdentical && rightTreeIdentical;
}
```
Time Complexity: O(N)
Space Complexity: O(N)

# How to check if two Binary Trees are mirror to each other?.

```
bool areTreesMirrors( struct TreeNode* root1, struct TreeNode* root2 ) {
  if( root1 == NULL && root2 == NULL ) {
    return true;
  }

  if( root1 == NULL || root2 == NULL ) {
    return false;
  }
  
  bool leftTreeIdentical = areTreesMirrors( root1->lChild, root2->rChild );
  bool rightTreeIdentical = areTreesMirrors( root1->rChild, root2->lChild );
  bool currentNodeIdentical = root1->data == root2->data;

  // The LST and the RST have to be mirrors while the current node value has to be the same.
  return areTreesMirror && currentNodeIdentical && rightTreeareTreesMirrorIdentical;
}
```
Time Complexity: O(N)
Space Complexity: O(N)

# How to traverse a tree in a Zig Zag order

![Zig Zag Traversal](https://user-images.githubusercontent.com/42272776/113134530-890eac80-923e-11eb-87bb-09cce36ca207.jpg)

Time Complexity: O(N)
Space Complexity: O(N) + O(N) = O(N) 

# Print ancestors for a given node

```
bool printAncestors( struct TreeNode* root, int key ) {

  if( root == NULL )
    return false;
  if( root->data == key )
    return false;
  // If the LST already identified the node, then the right subtree need not be parsed.
  // That is why we follow this approach of 'if'.
  if( printAncestors( root->lChild, key ) ) {
    printf( root->data );
    return true;
  }
  if( printAncestors( root->rChild, key ) ) {
    printf( root->data );
    return true;
  }
  return false;
}
```
Time Complexity: O(N)
Space Complexity: O(logN) - this is because, we store the hierarchy, which is typically log N.

# Common Ancestor for two nodes

**Approach 1: Using two stacks**
- Use a Stack for storing the hierarchy from the node in question to its root.
- Use the second stack for storing the hierarchy for the second node as well.
- Now we have two stacks which are to be popped up until their top of stack is equal.
- This is the common ancestor of the two nodes in question.

Time Complexity: O(N)
Space Complexity: O(logN) - this is because, we store the hierarchy, which is typically log N.

**Approach 2: Using recursion itself**

# Method to create a mirror from a tree
The below approach can also be used to create a clone of a Tree.
```
struct TreeNode* createMirror( struct TreeNode* root )
{
  if( root == NULL ) return NULL;
  
  struct TreeNode* leftSubTree = createMirror( root->lChild );
  struct TreeNode* rightSubTree = createMirror( root->rChild );
  
  struct TreeNode* temp = (struct TreeNode*)malloc(sizof(struct TreeNode));
  temp->data = root->data;
  temp->lChild = rightSubTree;
  temp->rChild = leftSubTree;
  return temp;
}
```
Time Complexity: O(N)
Space Complexity: O(N)

# Method to find a path in the tree amounting to a given sum
```
boolean pathFinder( struct TreeNode* root, int sum ) {

  if( root == NULL ) return false;
  
  boolean lVerdict = pathFinder( root->lChild, sum - root->data );
  if( lVerdict ) return true; // This is to skip the unnecessary processing of the other subtree.
  
  boolean rVerdict = pathFinder( root->rChild, sum - root->data );
  if( rVerdict ) return true; // This is to skip the unnecessary processing of the other subtree.
  
  if( sum - root->data == 0 ) return true;
  
  return false;
}
```
![path finder](https://user-images.githubusercontent.com/42272776/113190229-b75dad80-9279-11eb-9ac9-0dff003d92fe.jpg)
Time Complexity: O(N)
Space Complexity: O(N)

# Method to find a path in the tree amounting to a given sum
```
boolean pathFinder( struct TreeNode* root, int sum ) {

  if( root == NULL ) return false;
  
  boolean lVerdict = pathFinder( root->lChild, sum - root->data );
  if( lVerdict ) return true; // This is to skip the unnecessary processing of the other subtree.
  
  boolean rVerdict = pathFinder( root->rChild, sum - root->data );
  if( rVerdict ) return true; // This is to skip the unnecessary processing of the other subtree.
  
  if( sum - root->data == 0 ) return true;
  
  return false;
}
```
![path finder](https://user-images.githubusercontent.com/42272776/113190229-b75dad80-9279-11eb-9ac9-0dff003d92fe.jpg)
Time Complexity: O(N)
Space Complexity: O(N)

# How to find the deepest node and its value
This algorithm can be reused to find the largest/smallest value in a Binary Tree as well.
```
void findDeepestNode( struct TreeNode* root, int* currentLevel, int* maxLevel, int* data )
{
  if( root == NULL )
  {
    currentLevel = maxLevel = data = -1;
    return;
  }
  
  findDeepestNode( root->lChild, *currentLevel+1, maxLevel, data );
  findDeepestNode( root->rChild, *currentLevel+1, maxLevel, data );
  
  if( currentLevel > maxLevel )
  {
    *maxLevel = *currentLevel;
    *data = root->data;
  }
}
```
Time Complexity: O(N)
Space Complexity: O(N)

# Determining the level at which the sum is maximum

- In this algorithm, after pushing the children of a given level, we also push a NULL.
- This NULL is used to distinguish between the levels.
```
int sum = 0;
int currentMax = INT_MIN;
q = createQueue();
q->enqueue( root );
q->enqueue( NULL );

while( !q->empty() ) {

  tmp = q->dequeue();
  
  // Two cases arise, either TMP is NULL or it is not NULL.
  if( tmp == NULL ) {
    
    if( currentMax < sum )
      currentMax = sum;
    
    sum = 0;
    if( !q->empty() )
    q->enqueue( NULL );
  
  } else {
  
    sum = sum + tmp->data;
    if( tmp->lChild )
    q->enqueue( tmp->lChild );
    
    if( tmp->rChild )
    q->enqueue( tmp->rChild );
  }
}
```
Time Complexity: O(N)
Space Complexity: O(N)

# What do they solve

Data Structure or Algorithm | Problems used for | Complexities
------------ | ------------- | -------------
Arrays | The need for having more than one variable for a set of inputs |
Linked Lists | Arrays have to occupy continous memory locations. So there are chances where Array memory allocation can fail |
AVL Tree | Uncontrolled insertions lead to skewed binary trees which have O(N) search complexity. AVL Trees are self adjusting BST which ensure that the BST performance does not degrade to O(N) by doing restructuring automatically.
B Tree| Helps in multi Level Indexing for databases. Whem compared with BSTs, B Tree and B+ Trees are better in terms of RAM/cache usage. This is because in a B Tree / B+ Tree, each node would have more than one key and the corresponding pointers that are to be followed. Also the node size is almost always made equal to the cache WORD size. This means that in each READ cycle, after the node is READ, the processing can be done on different keys / follow up path decisions are made. Ex: If the block is loaded onto the memory, then you can compare it with 3-5 keys in the memory itself thereby, reducing time delays. If this were to happen in BSTs, in each READ cycle, only one node is returned and for the same 3-5 key comparisions, we may need 3-5 READs ( disk -> main memory -> caches ) which are slow.| 
B+ Tree | In addition to benefits of B Trees, B+ Trees offer one more advantage. If you have a query that is to sweep the entire table, then the algorithm can follow the linked list referenced in the leaf nodes. If this were to be done on B Tree, the entire tree would have to be checked again.|
Heap | Selecting Kth largest or smallest element in O(N) / Efficient priority queue implementations / Heap Sorts |

# Sorting
Stable sort are algorithms where the order of two array elements at indexes is preserved in the final outcome if those two elements are same.
Ex: Merge Sort and Insertion Sort


# Still to go
Sorting
Searching
Hashing
Arrays problems
String problems
Graphs
Queues







