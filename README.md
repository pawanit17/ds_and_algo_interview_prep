**Complexities**
- O(N) means that the algorithm needs N in growth. 

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

## How to find if a Linked List has a loop?.
- Maintain two pointers with unequal increment and make them iterate. If they meet at any point, there is a loop.
- O(1) space complexity and O(N) time complexity.

## How to find starting point of the loop?.
- Continuation to the problem above.
- Initialize q to head and p to meeting point and increment both by a single step. The node on which they meet is the beginning of the loop.

## How to find the 'k'th node from the end in a Linked List?.
- Add an external counter on the number of nodes in the Linked list.
  - Needs update during addition and deletion.
- Maintain two pointers with an increment of 1 but after a distance of 'k'.
- O(1) space complexity and O(N) time complexity.

## Adding a node to a sorted linked list
- Initialize ```temp``` to beginning of the list
- Iterate while the input number is less than that of the current node's data field.
- Insert adjusting pointers
  - ```temp->next = ptr->next```
  - ```ptr->next = temp```
- Time complexity (N) and space complexiy O(1).

## Print the contents of an Linked List in the reverse manner?.

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

## How to achieve O(1) access time for Linked Lists?.
- Maintain a seperate HashTable - < Integer Index to Memory Address or Object >
- Every addition/removal to the Linked List should be registered in the HashTable
- Adds extra space complexity of O(N)
- Adds extra processing of O(N) for maintaining this cache

## Finding the common merging point of two Linked Lists

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

## How to get previous nodes if the HEAD is at Kth node in a Linked List
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

## How to check if the Linked List is a Palindrome

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
## Reverse Linked Lists(Open)
## Replace adjacent nodes in a Linked List(Open)

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

## How to get the maximum value in a Stack in O(1) time complexity
- Maintain a secondary stack that will hold the largest value till the same index in the corresponding Stack.
- Time Complexity - O(N) for building the stack, but once built, getting Max value is O(1).
- Space Complexity - O(N).

## How to store two stacks in an array
- Have the first stack grow left and the other grow right.

## How to store k stacks in an array of size m
- Each m/k section of the array should be a stack
- Whenever a stack reaches size m/k, then it reached its alloted size
## How to sort the elements in the Stack using push, pop, peek?.(Open)

## How to reverse the elements in the stack using push and pop?.(Open)

# Recursion
## Check if the content of the array is a palindrome
```
bool isPalindrome( int arr, int len, int index ) {
    if( index > len/2 )
    return true;

    return arr[index] == arr[len-1-index] && isPalindrome( arr, len, index + 1 );
}
```

## Check if the Array sum is even
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
## Printing contents of a Binary Tree
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

## Find the width of a binary tree(Open)



## Create Binary Tree from inorder and preorder or inorder and postorder traversals(Open)

# Binary Search Tree
![image](https://user-images.githubusercontent.com/42272776/112369196-ed42e500-8d01-11eb-94de-f8301b39cf91.png)

BST is a BT where nodes are sorted to facilitate easier searches.
At each iteration half of the tree can be discarded making the search space smaller.

## Creating a BST from a list of number
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

## Search in a BST
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

### Adding in a BST
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

## Deletion in a BST(Open)

## Finding the largest / smallest element in the BST
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







