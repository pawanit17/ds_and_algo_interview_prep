# ds_and_algo_interview_prep

**Abstract Data Type**
- Representing a user defined data type in layman terms is ADT.
- ADT defines what type of operations can be done, what behavior is exhibited by this data type etc.
- Ex: Stack

**Linked Lists vs Arrays**
LLs help in storing more amount of data as there is not hard requirement for storing them in continous memory locations. Arrays fail here.
Arrays are faster and lets you access a given element at an index. LLs do not have that feasibility.

# Linked Lists
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

```
void printInReverse( Node* head )
{
  if( head == NULL ) return;
  printInReverse( head->next );
  printf( head->data );
  return;
}
```



