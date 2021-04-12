**Complexities**
- O(N) means that the rate of growth of complexity of the algorithm as a function of the input size.
- O(N) determines that it is atleast N in growth.

## Amortized Analysis
Suppose there is an unsorted array of size 'n' from which you need to be able to get the kth smallest element. And you will be making say, 'n' retrievals.
- If you sort the array - O(nlogn)
- But this lets access of kth smallest or largest element in O(1) time.
- So on average, the cost of retrieval of one element is nlogn/n = logn.
- This is called as Amortized analysis.

# Arrays

## In an Array of numbers, there is one repeating number. What is that repeating number?.
- Sort using Quick, Merge or Heap sort
- Then a linear pass
- Time Complexity: O(N)
- Space Complexity: O(N)

## In an Array of numbers of size N, there is one repeating element. Find it
- Use the sum of all integers till N to arrive at that number.
- Time Complexity: O(N)
- Space Complexity: O(1)

## In an array, find the element that has occurred the most
- Sort the array using in-place heap sort
- Do a lined pass maintaining two variables - index and value
- The index for the highest value is the one.
- Time Complexity: O(N)
- Space Complexity: O(1)
- Two other ways of solving this problem is by using Hashes and by using an extra count field in a BST.

## There are two arrays, one of size m+n and the other of size n. In the first array, only m elements are used. Devise an algorithm to sort them
```
m+n : 1 4 6 7 9 10 _ _ _ _
n: 2 3 5 11

i = m-1;
j = n-1;
k = 0;
while( k < m+n ) {
  if( a[i] >= a[j] ) {
    a[m+n-1-k] = a[i];
    i--;
  }
  else {
    a[m+n-1-k] = a[j];
    j--;  
  }
  k++;
}
- Time Complexity: O(m+n)
- Space Complexity: O(1)
```

## Find two numbers in an unsorted array whose sum is X
- Sort the array using in-place heap sort
- For each element in the array, do a binary search for X-a[i]
- Time Complexity: O(NlogN)
- Space Complexity: O(1)

## Find two numbers in a sorted array whose sum is X
- Maintain two pointers - one at the start and the other at the end.
- If the sum if greater than X, decrement the larger data pointer
- If the sum is less than X, increment the smaller data pointer
- If the sum is equal, return the small and large pointers
- Time Complexity: O(N)
- Space Complexity: O(1)

## Two elements whose sum is closes to 0
- Sort the elements using heap sort - in-place sort.
- If the first element and the last element are both positive or both negative, 
- Maintain two indexes, one for negative numbers and one for positive numbers and gradually increment them.
- Time Complexity: O(n)
- Space Complexity: O(1)

## Identify three numbers whose sum is equal to K
- Brute force solves this in O(N^3)

Another approach:
- Sort the elements using in-place heap sort
- For each index, do the two pointer approach on the rest of the array
- This reduces the complexity O(N^2). 

## Counting sort
## Bucket sort
## Radix sort

## Rotating the array to the right k times
- Get hold of last number
- Copy from right to left
- Replace the zeroth index with last number.
```
class Solution {
    public void rotate(int[] nums, int k) {
        
        if( nums.length == 0 || nums.length == 1 )
            return;
        
        int count = 0;
        while( count < k )
        {
            count++;
            
            int last = nums[nums.length-1];
            
            for( int inx = nums.length-1; inx > 0; inx-- )
            {
                nums[inx] = nums[inx-1];
            }
            nums[0] = last;
        }        
    }
}
```
- Another implementation that can be done is this:
- Assume that the number is 123456789
- And that we want to rotate after 6th character. So we do this:
  - Break the array into a[0...5] and a[6..8] and name them as X and Y.
  - Invert Y - 123456 987
  - Invert X - 654321 987
  - Invert the entire thing - 789123456

## Find the number that is occurring odd number of times
- XOR all the elements. The one that remains is the element that occurred odd number of times.
- Time Complexity O(N)
- Space Complexity O(1)

## If Array has n-1 elements from 1 to n then find the number that is missing
- XOR all the elements - X.
- XOR all the numbers from 1 to n - Y.
- XOR of X and Y gives the missing element.
- Time Complexity O(N)
- Space Complexity O(1)

## Dutch National Flag Algorithm
- low always points to the last '1' so that if mid encounters a '0', a swap can be made to fix 0s
- mid always skips '1' to fix 1s.
- high always fixes 2s.
```
low = 0;
mid = 0;
high = a.length-1;

while( mid <= high )
{
    switch(mid)
    {
        case 0: swap( a[low], a[mid] ); low++; mid++; break;
        case 1: mid++; break;
        case 2: swap( a[high], a[mid] ); high--; break;
    }
}
```
- Time Complexity O(N)
- Space Complexity O(1)

## Fisher-Yates Shuffle
Pick a random number between 0 and n-1 and replace the n-1th value with that index. After this, decrement the index.
This helps in ensuring that in the worst case, the algorithm does not reset the shuffle.
Also, if the index is 0, no need to in shuffling it.
```
To shuffle an array a of n elements (indices 0..n-1):
  for i from n - 1 downto 1 do
       j = random integer with 0 <= j <= i
       exchange a[j] and a[i]
```
- Time Complexity O(N)
- Space Complexity O(1)

## Sorting Algorithms

### Selection sort
- At each pass, the smallest element in the array will be moved to the first index.
- At each pass, only the first element is considered for swap.
```
  private static void selectionSort(int[] numbers) 
	{	
		int len = numbers.length;

		for(int inx = 0; inx < len-1; inx++)
		{
			for(int jnx = inx + 1; jnx < len; jnx++)
			{
				if(numbers[inx] > numbers[jnx])
				{
					int temp = numbers[jnx];
					numbers[jnx] = numbers[inx];
					numbers[inx] = temp;
				}
				printArray(numbers);
			}
			printArray(numbers);
		}
	}
```
- Time Complexity O(N^2)
- Space Complexity O(1)

### Bubble Sort
- While the selection sort and bubble sort may appear similar at first glance, they are not.
- Bubble sort focusses on bringing the heaviest element or the lighter element to the end of the array.
- Also, in selection sort, the values are indices inx and jnx are considered.
- In bubble sort, the values are jnx and jnx+1 are considered. In selection sort, we consider inx, jnx.
```
	private static void bubbleSort(int[] numbers) 
	{
		int len = numbers.length;

		// 90 10 20 61 100 40
		for( int inx = 0; inx < len; inx++ )
		{
			for(int jnx = 0; jnx < len-1-inx; jnx++)
			{
				if(numbers[jnx] > numbers[jnx+1])
				{
					int temp = numbers[jnx];
					numbers[jnx] = numbers[jnx+1];
					numbers[jnx+1] = temp;
				}
				printArray(numbers);
			}
			printArray(numbers);
		}		
	}
```
- Time Complexity O(N^2)
- Space Complexity O(1)

### Insertion sort

### Quick sort

### Merge sort
Base condition should be low>=high. This is simple because if low == high, the array is just one element size and every array of size 1 is sorted by itself.

![MergeSort](https://user-images.githubusercontent.com/42272776/113928531-931b4700-980c-11eb-9a29-bcf2fae30db3.jpg)

```
private static void mergeSort(int[] numbers, int low, int high)
{
	if( low >= high )
	{
		return;
	}

	int temp[] = new int[9];
	int mid = ( low + high )/2;
	mergeSort( numbers, low, mid);
	mergeSort( numbers, mid+1, high);
	merge(numbers, temp, low, mid, mid+1, high);
	copy(numbers, temp, low, high);
	printArray(numbers);
}

private static void merge(int[] numbers, int[] temp, int low1, int high1, int low2, int high2)
{
	int i = low1;
	int j = low2;
	int k = low1;
	while( i <= high1 && j <= high2 )
	{
		if( numbers[i] < numbers[j])
		{
			temp[k] = numbers[i];
			k++;
			i++;
		}
		else
		{
			temp[k] = numbers[j];
			j++;
			k++;
		}
	}
	while( i <= high1 )
	{
		temp[k] = numbers[i];
		k++;
		i++;
	}
	while( j <= high2 )
	{
		temp[k] = numbers[j];
		k++;
		j++;
	}
}

private static void copy(int[] numbers, int[] temp, int low, int high) 
{
	for(int inx = low; inx <= high; inx++)
	{
		numbers[inx] = temp[inx];
	}
}
```
- Time Complexity O(NlogN) the merge process happens logN time in best/average case. In worst case, this becomes O(N^2).
- Space Complexity O(N) for the array.

### Heap sort

## :gear: AlgoExpert
### Find first non-repeating character

Conventional i=0 and j=i+1 wont work in this case because of strings like this:
*faadabcbbebdf*
If the question had been finding the first repeating character, that i=0 and j=i+1 scheme would have worked out.
```
public int firstNonRepeatingCharacter(String str) 
{
    for( int inx = 0; inx < str.length(); ++inx)
    {
	boolean found = true;
	for( int jnx = 0; jnx < str.length(); ++jnx)
	{
		if(inx==jnx) continue;
		if(str.charAt(inx) == str.charAt(jnx))
		    found = false;
	}
	if(found)
	{
		return inx;
	}
    }
    return -1;
}
```
- Time Complexity O(N)
- Space Complexity O(1)

### Given two arrays, find if the second array is a subsequence of the first array. Ex: a = [1,2,3,4] s = [1,3,4].
```
public static boolean isValidSubsequence(List<Integer> array, List<Integer> sequence) 
{
    for(int inx = 0; inx < array.size(); inx++ )
    {
	int jnx = 0;
	int count = 0;
	for( int knx = inx; knx < array.size(); ++knx)
	{
	    if(array.get(knx) == sequence.get(jnx))
	    {
    		jnx++;
	  	count++;
	    }
	    if( count == sequence.size())
		return true;
	    }			
	}
    return false;
}
```
- Time Complexity O(MN)
- Space Complexity O(1)

### Check if a string is a palindrome

`inx < jnx` is needed because in case of an odd length string, inx and jnx will technically reach same location at one time if the string is a palindrome.
```
public static boolean isPalindrome(String str) {
    
	if( str.length() == 0 || str.length() == 1 )
		return true;

	int inx = 0;
	int jnx = str.length()-1;

	int comparisions = 0;
	while(str.charAt(inx) == str.charAt(jnx) && inx < jnx)
	{
		comparisions++;
		inx++;
		jnx--;
	}

	if( comparisions == str.length()/2 )
    		return true;
		
	return false;
  }
```
- Time Complexity O(N)
- Space Complexity O(1)

### Find the three largest elements in the array
Main thing to note here is that the last ELSE clause should have a condition. Otherwise, a swap with thirdLargest element happens always.
```
public static int[] findThreeLargestNumbers(int[] array) {

	int larger = Integer.MIN_VALUE;
	int secondLarger = Integer.MIN_VALUE;
	int thirdLarger = Integer.MIN_VALUE;

	for( int inx = 0; inx < array.length; inx++)
	{
		if( array[inx] > larger )
		{
			thirdLarger = secondLarger;
			secondLarger = larger;
			larger = array[inx];
		}
	        else if( array[inx] > secondLarger )
		{
			thirdLarger = secondLarger;
			secondLarger = array[inx];
		}
		else if( array[inx] > thirdLarger )
		{
			thirdLarger = array[inx];
		}
	}

	return new int[] { thirdLarger, secondLarger, larger };
  }
```
- Time Complexity O(N)
- Space Complexity O(1)

### Given a competitions array ( hostteam, awayteam ) and the results ( 0/1 ), write an algorithm to identify who the winner is of the whole tournament, given that there are no ties

```
	public static String tournamentWinner( ArrayList<ArrayList<String>> competitions, ArrayList<Integer> results) 
	{
		Map<String, Integer> teamToWinsMap = new HashMap<String, Integer>();
		int winnerWins = Integer.MIN_VALUE;
		String winnerName = "";
		for(int inx = 0; inx < competitions.size(); ++inx)
		{
			boolean homeTeamWon = results.get(inx) == 1;
			String winningTeam = "";
			if( homeTeamWon )
			{
				winningTeam = competitions.get(inx).get(0);								
			}
			else
			{
				winningTeam = competitions.get(inx).get(1);				
			}			

			addToMap( teamToWinsMap, winningTeam );
			if( winnerWins < teamToWinsMap.get(winningTeam) )
			{
				winnerWins = teamToWinsMap.get(winningTeam);
				winnerName = winningTeam;
			}		
		}
		
		// Get the highest value from the Map
		return winnerName;
	}
	
	public static void addToMap(Map<String, Integer> teamToWinsMap, String team)
	{
		if( teamToWinsMap.containsKey(team) )
		{
			teamToWinsMap.put(team, teamToWinsMap.get(team) + 1 );
		}
		else
		{
			teamToWinsMap.put(team, 1 );
		}
	}
```
- Time Complexity O(N) the number of matches.
- Space Complexity O(K) the number of teams.

### A sorted integer array is given, we have to construct its squared array in sorted manner and return it.
Catch here is if it has negative numbers, then the square of negative number will be positive. So we take a new array and use two pointer approach and fill it from the rear.
```
public int[] sortedSquaredArray(int[] a) 
{
	int n = a.length;
	int largestIndex = n-1;
	int smallestIndex = 0;

	int finalArray[] = new int[n];
	int inx = n-1;

	while( smallestIndex <= largestIndex )
	{
			 if( Math.abs( a[smallestIndex]) > Math.abs( a[largestIndex]) )
			 {
			     finalArray[inx] = (int)Math.pow( a[smallestIndex], 2);
					 smallestIndex++;
			 }
			 else
			 {
					 finalArray[inx] = (int)Math.pow( a[largestIndex], 2);
					 largestIndex--;
			 }

			 inx--;
	}

        return finalArray;
}
```
- Time Complexity O(N).
- Space Complexity O(N).

### Branch Sums in a Binary tree
```
public static List<Integer> branchSums(BinaryTree root) {

	List<Integer> allPathSums = new ArrayList<Integer>();
	getPathSumToLeaves( root, 0, allPathSums );
	
	return allPathSums;
}

public static void getPathSumToLeaves( BinaryTree root, int sum, List<Integer> allPathSums)
{
	if( root == null)
	{
			return;
	}
	if( root.left == null && root.right == null )
	{
			allPathSums.add(sum + root.value);
			return;
	}

	getPathSumToLeaves( root.left, sum + root.value, allPathSums);
	getPathSumToLeaves( root.right, sum + root.value, allPathSums);

	return;
}
```
- Time Complexity O(N).
- Space Complexity O(N).

### You are given an array of integers and an integer. Write a function that moves all instances of that integer in the array to the end of the array and returns the array
- Use two pointer approach
```
public static List<Integer> moveElementToEnd(List<Integer> array, int toMove) 
{
	int low = 0;
	int high = array.size()-1;
	
	while( low < high )
	{
		if(array.get(high) == toMove)
		{
				high--;
		}
		else if(array.get(low) == toMove)
		{
			  // swap
				int temp = array.get(low);
				array.set(low, array.get(high));
				array.set(high, temp);

				low++;
				high--;
		}
		else
		{
				low++;
		}
	}
	// Write your code here.
	return array;
}
```
- Time Complexity O(N).
- Space Complexity O(1).

### Two arrays are given - redshirt and blueshirts. They are to be arranged in front and back rows such that the items in the back row are strictly greater than that of the first row. Red and Blue arrays cannot be mixed
- We sort both the arrays in descending order
- We then identify which of the two arrays has the highest value. Because that array has to be the back bencher.
- Then we see if the corresponding columns in the two rows are greater/less and return a true or false accordingly.
```
public boolean classPhotos(
ArrayList<Integer> redShirtHeights, ArrayList<Integer> blueShirtHeights) {

	Collections.sort( redShirtHeights, Collections.reverseOrder() );
	Collections.sort( blueShirtHeights, Collections.reverseOrder() );

	String backRow = redShirtHeights.get(0) > blueShirtHeights.get(0) ? "RED" : "BLUE";

	if( backRow.equals("RED"))
	{
		return compareRows( blueShirtHeights, redShirtHeights );
	}
	else
	{
		return compareRows( redShirtHeights, blueShirtHeights );			
	}
}

private boolean compareRows(ArrayList<Integer> frontRow, ArrayList<Integer> backRow) 
{
	for( int inx = 0; inx < frontRow.size(); ++inx )
	{
		if(frontRow.get(inx) >= backRow.get(inx))
		{
			return false;
		}
	}

return true;
}
```
- Time Complexity O(NlogN) + O(NlogN) + O(N) = O(NlogN).
- Space Complexity O(1).

### Return the first duplicate value in an array given that all the numbers are between 1-n.
- Approach here is to negate the value present at each a[i].
- The index i that has the negative value is the value that we need to return.
- Note that we need to return the absolute value.
```
public static int firstDuplicateValue(int[] array) 
	{
		for(int inx=0; inx<array.length; ++inx)
		{
				if(array[Math.abs(array[inx])-1] < 0)
				{
						// This element has already come earlier
					  return Math.abs(array[inx]);
				}
		    array[Math.abs(array[inx])-1] = -1 * array[Math.abs(array[inx])-1]; 
		}
	  		return -1;
	}
```
- Time Complexity O(N)
- Space Complexity O(1).

### Identify the LCA for a BST
- LCA calculation for a BST is easier than that of a normal BST.
- We rely on the BST principle or node ordering to traverse either left or right.
- Note that the LCA of two nodes is either one of them or the node that splits them into two different nodes.

```
public static TreeNode* getLCAInBST( struct TreeNode* root, struct TreeNode* p, struct TreeNode* q )
{
    if( root ==  NULL ) return NULL;
    
    if( root->value > p->value && root-value > q->value )
    	return getLCAInBST( root->left, p, q );
    else if( root->value < p->value && root-value < q->value )
    	return getLCAInBST( root->right, p, q );
    else
    	return root;
}
```
- Time Complexity O(N)
- Space Complexity O(1).

### Identify the LCA for a BT
- At each node, we have to return an identifier ( NULL or Node itself ) if the subtree holds one or both of the input information.
- This will be rolled back to the root where we see the LST and RST return data and act accrordinly.
- If the return is a NULL from a sub tree, then that sub tree does not have either of the two variables.
```
TreeNode* leastCommonAncestor( struct TreeNode* root, int p, int q )
{
    if( root == NULL )
        return NULL;

    if( root->data == p || root->data == q )
        return root;

    TreeNode* lAncestor = leastCommonAncestor( root->lChild, p, q );
    TreeNode* rAncestor = leastCommonAncestor( root->rChild, p, q );

    if( lAncestor != NULL && rAncestor != NULL ) // This is the ancestor node.
        return root;
    else if( lAncestor == NULL && rAncestor == NULL ) // This is the leaf node.
        return NULL;
    else if( lAncestor != NULL)
    	return lAncestor;
    else
	return rAncestor;
}
```
- Time Complexity O(N)
- Space Complexity O(1).

### Three Number Sort - Similar to Dutch National Flag algorithm, except the sort order is dictated by a second array.
```
import java.util.*;

class Program {
  public int[] threeNumberSort(int[] a, int[] order) {
    
		int low = 0;
		int mid = 0;
		int high = a.length-1;
		
		while( mid <= high )
		{
		    if(a[mid] == order[0] )
				{
						int temp1 = a[mid]; a[mid] = a[low]; a[low] = temp1; low++; mid++;
				}
				else if(a[mid] == order[1] )
				{
						mid++;
				}
				else
				{
						int temp2 = a[mid]; a[mid] = a[high]; a[high] = temp2; high--;
				}
		}
		
    return a;
  }
}
```
---------------------------------------------------------------------------------------------------------------------------------------

## :gear: Scalar Academy Session
## Second largest element in the array
- Maintain two variables and solve it
- large = a[0]
- if( a[1] > a[0] ) large = a[1] and secondLarge = a[0];
- Now iterate forward anre whenever you encounter a value greater than large, swap it and copy largest to secondLargest.
```
 for( i = 2; i < n; i++ ) {
   if( a[i] > largest ) {
     secondLarge = large;
     large = a[i];
   }
   else if ( a[i] > secondLarge ){
     secondLarge = a[i];
   }
   else {
   }
   return secondLarge;
   }
```
- Time Complexity O(N)
- Space Complexity O(1)
`
## Kth largest element in the array ( with no extra space )
- One approach is to sort the array and return kth element
- Approach two:
  - Find the largest element in 0..n-1 and swap it with last index
  - Find the largest element in 0..n-2 and swap it with last but one index
  - In K iterations, this would yield the third largest element
  - This is selection sort.

## Kth largest element in the array ( with constrain that only adjacent elements can be interchanged )
- Bubble sort

## Array in which odd and even values are sorted
- { 3, 9, 2, 4, 15, 10, 19 }
- Create two arrays a[] and b[] and apply merge sort algorithm.
- Merge Sort
  - Time Complexity of merge:
    - At each step we do O(N) computations and the height of the binary tree is O(log N ).
    - The reason why we do equal partition is to ensure that the height of the binary tree is balanced which will result in logN height.
    - What if the array is divided into three parts - height will be O(logn with base 3).
    - This will be smaller than O(logn with base 2). But the number of comparisions will increase.
    - Ex: [7,8,9] [3,4,6] [1,5]
    -      i       j       k
    -      [...............]
    -      This increases the time it takes to identify which index to be added.
    - Dividing the array into n parts will result into selection sort
    - 9 | 8 | 7 | 3 | 6 | 4 | 1 | 10
    - Merge step complexity increases heavily.

## Count inversions in an array
- If i < j, a[i] > a[j] and i<j
- Brute force is two for loop approach
- Another option is to use the merge approach
  - During merge phase, if there is a number in the left set which is greater than the ones in right set, then we have inversions.
  - Complexity is O(nlogn).

## With less number of weighing find the heaviest one ball in 100 no of same colored balls. All balls looking same , but one is heavier than the rest, we are provided with a balance scale on which we can balance balls on both side
- Binary search approach can be used.
- 33 + 33 + 33 + 1
- You just have to identify which bucket to look at.

## Given N nuts of different sizes and N bolts of different size and there is exactly 1:1 match b/w nuts and bolts.
- Brute force is one option O(N2)
- Quick sort

## Stable Sort
If a == b and a comes before b in the unsorted array, then after sorting, a should still be before b.
- Bubble sort: Swap a[i] and a[i+1] only if they are not equal
- Selection sort: Select the last occurrence of the largest element to swap with last element.
- Merge sort: Prefer the element from the left sub array if the current value is same at both left and right side parts.

## Binary Search & its variants

### Basic binary search
```
public static int binarySearch(int[] array, int target) {
    
		int low = 0;
		int high = array.length-1;
				
		while( low <= high )
		{
			int mid = low + ( high - low )/2;
			if( target < array[mid] )
			{
				high = mid-1;
			}
			else if( target > array[mid])
			{
				low = mid+1;
			}
			else
			{
				return mid;
			}			
		}
		
		
    return -1;
  }
```
- Time Complexity O(logN)
- Space Complexity O(1)

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
## :dart: Reverse Linked Lists
![Reverse Linked List](https://user-images.githubusercontent.com/42272776/113765741-4b2bef80-973a-11eb-84d9-a34c837b8f17.jpg)
```
struct Node* reverseList( structNode* node ) {
  if( node == NULL )
    return NULL;
  
  if( node->next == NULL ) {
    head = node;
    return node;  
  }
  
  struct Node* ptr = reverseList( node->next );
  ptr->next = NULL;
  node->next = NULL;
  return node;
}
```
- Time Complexity: O(N)
- Space Complexity: O(N)

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


## Why cant a tree be created from pre/post/inorders?
The following three Trees have the same PRE ORDER - abc.

     (a)
    /  \
   (b) (c)

   (a)
   /
 (b)
 /
(c)

(a)
  \
  (b)
    \
    (c)

The POST ORDERs are bca, cba, cba

- So if PreOrder abc and PostOrder cba are given, then the Tree cannot be uniquely constructed.
- This is because there is no clear demarkation on where the LST ends and the RST starts.


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

# Printing all the root to leaf paths
This approach could be used to identify the Kth node from the root. 
- In this algorithm, after pushing the children of a given level, we also push a NULL.
- This NULL is used to distinguish between the levels.
```
void pathTraversals( struct TreeNode* root, int* array, int* index ) {

  if( root == NULL )
    return;
  
  if( root->lChild == NULL && root->rChild == NULL ) {
    printArray(array, index);
    return
  }
  
  array[*index] = root->data;
  
  pathTraversals( root->lChild, array, index+1 );
  pathTraversals( root->rChild, array, index+1 );
}
```
Time Complexity: O(N)
Space Complexity: O(N)

# Print the diameter of a tree
![Diameter](https://user-images.githubusercontent.com/42272776/113348127-d7fa3600-9353-11eb-9594-eabe742e0e41.jpg)

# Print the LCA of two nodes in a tree

# What are TRIE


# Ternary Search Trees

# Suffix Trees

# How are symbol tables implemented
Symbol tables need quick retrieval times. So the following approaches are OK
- Binary Search Tree
- Binary Search Tree with self balancing
- Ternary Search Trees
- Hashing

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
Searching
Hashing
String problems
Graphs
Queues


# Mistakes to avoid
- Avoid multiple paths in which a variable is incremented or decremented ( inx++ ). This leads to unpredictable results for edge cases.
- More stress on edge cases while writing program.
- In most cases, identifying the largest in a scenario, can be done with out any extra pass by hacking a simple variable that maintains the highest value.
- For array problems, if you do not have any solution or optimal solution, try sorting the array and see if there is any lead.
- Be careful in tree recursion.
  - Always include root == null case. It will come up if the tree has no children in any program/question.
  - When counting in BT, if special processing is needed for leaf cases, like path sums etc, be careful to rethink about leaf case properly.


# Additional resources to explore
- https://github.com/coding-parrot/projects/tree/master/system%20design%20contest
- https://medium.com/refraction-tech-everything/how-netflix-works-the-hugely-simplified-complex-stuff-that-happens-every-time-you-hit-play-3a40c9be254b
- https://www.techhive.com/article/2158040/how-netflix-streams-movies-to-your-tv.html
- What to do first? https://t.me/system_design_interviews/14311
- Grokking design book: https://t.me/system_design_interviews/49
- DDIA book: https://t.me/system_design_interviews/1173
- Design primer: https://github.com/donnemartin/system-design-primer
- Leveling guide - interview: 
- https://t.me/system_design_interviews/3372 
- https://t.me/system_design_interviews/14545
- DDIA notes: https://t.me/system_design_interviews/7133
- DDIA summary: https://t.me/system_design_interviews/6423
- Database internals book: https://t.me/system_design_interviews/5407
- Grokking coding: https://t.me/system_design_interviews/6118
- Offer negotiation: https://t.me/system_design_interviews/9930
- Behavioral / manager interview book: https://t.me/system_design_interviews/13440
- Resource for LLD - https://github.com/prasadgujar/low-level-design-primer/blob/master/solutions.md
- System Design Interview Guide book: https://t.me/system_design_interviews/14132



