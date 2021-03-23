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

## Circulate Linked Lists
## Reverse Linked Lists
## Replace adjacent nodes in a Linked List

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
## How to sort the elements in the Stack using push, pop, peek?.

## How to reverse the elements in the stack using push and pop?.

# Recursion
- Check if the content of the array is a palindrome

```
bool isPalindrome( int arr, int len, int index ) {
    if( index > len/2 )
    return true;

    return arr[index] == arr[len-1-index] && isPalindrome( arr, len, index + 1 );
}
```

- Check if the Array sum is even

```
bool isEvenSum( int arr, int len, int index, int sum ) {
    if( index == len )
        if( sum % 2 == 0 ) return true;
        return false;
    
    return isEven( arr, len, index + 1, sum + arr[index] );
}
```


# Sorting
Stable sort are algorithms where the order of two array elements at indexes is preserved in the final outcome if those two elements are same.
Ex: Merge Sort and Insertion Sort










