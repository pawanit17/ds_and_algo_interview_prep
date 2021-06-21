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
- Time Complexity: O(NlogN)
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
- Maintaing two pointers from the read and traverse to the front.
- If the shorter one is done, we are done. This is because it guarantees that the remaining elements in greater one are in place.
```
m+n : 1 4 6 7 9 10 _ _ _ _
n: 2 3 5 11

i = m-1;
j = n-1;
k = 0;
while( j >= 0 ) {
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

## Two elements whose sum is closest to 0
- Sort the elements using heap sort - in-place sort.
- If the first element and the last element are both positive or both negative, sum can never be zero and the closest ones are the ones at indices 0 and 1. 
- Maintain two indexes, one for negative numbers and one for positive numbers and gradually increment them.
- Time Complexity: O(nlogn)
- Space Complexity: O(1)

## Identify three numbers whose sum is equal to K
- Brute force solves this in O(N^3)

Another approach:
- Sort the elements using in-place heap sort
- For each index, do the two pointer approach on the rest of the array
- This reduces the complexity O(N^2). 

## [TODO] Counting sort
## [TODO] Bucket sort
## [TODO] Radix sort

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

## All elements in an array repeat even number of times, except one that repeats odd number of times. Find the number that is occurring odd number of times.
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

# Sorting Algorithms

## Selection sort
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

## Bubble Sort
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

## BubbleSort vs SelectionSort
- In BubbleSort, the element at the last is what gets updated. The heaviest element gets bubbled to the top.
- In InsertionSort, the element at 0th index is populated with the sorted element.

## Insertion sort
- Best understood using an example where you insert an element into a sorted array.
- Ex: 1 3 7 9 and you need to add 6 and 4 ( original array is 1 3 7 9 6 4 ).
```
public static int[] insertionSort(int[] a) 
{
	for(int inx=1; inx < a.length; ++inx)
	{
		int key = a[inx];

		// 1 3 7 9 6 4
		int jnx = inx - 1;

		while(jnx >= 0 && a[jnx] > key)
		{
		    a[jnx+1] = a[jnx];
		    jnx--;
		}

		// 1 3 7 7 9 4
		a[jnx+1] = key; 
	}

	return a;
}
```
- Time Complexity O(N^2)
- Space Complexity O(1)

## Quick sort
- To sort the elements in descending order, change the comparision order for the below two statements.

```
while( pivot < a[i] && i < high ) // i < high because we want to ensure that i does not spill over
    i++;
while( pivot > a[j] )
    j--;
```

```
import java.util.*;

class Program {
  public static int[] quickSort(int[] array) 
	{
		quickSort( array, 0, array.length - 1 );
    return array;
  }
	
	public static void quickSort( int a[], int low, int high )
	{
		// 8 1 4 9 2 7 6 3
		if( low >= high )
		{
			// TODO: What if low == high
			return;
		}
		
		int pivot = partition( a, low, high );
		quickSort( a, low, pivot-1 );
		quickSort( a, pivot+1, high );
	}

	public static int partition( int a[], int low, int high )
	{
		// 8 1 4 9 2 7 6 3
		int pivot = a[low];
		int i = low + 1;
		int j = high;

		while( i <= j ) // This is needed if there are only two elements to work with  say, 2,7
		{
			while( pivot > a[i] && i < high ) // i < high because we want to ensure that i does not spill over
				i++;

			while( pivot < a[j] )
				j--;

			if( i < j )
			{
				int temp = a[i];
				a[i] = a[j];
				a[j] = temp;
				i++;
				j--;
			}
			else
			{
				i++; // This is to ensure that if pivot is the largest element, i and j dont remain standstill
			}			
		}

		a[low] = a[j];
		a[j] = pivot;
		
		return j;		
	}
}
```
- Time Complexity O(NLogN)
- Space Complexity O(1)

## Merge sort
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

# :gear: AlgoExpert
## Find first non-repeating character

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

## Given two arrays, find if the second array is a subsequence of the first array. Ex: a = [1,2,3,4] s = [1,3,4].
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

## Check if a string is a palindrome

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

## Find the three largest elements in the array
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

## Given a competitions array ( hostteam, awayteam ) and the results ( 0/1 ), write an algorithm to identify who the winner is of the whole tournament, given that there are no ties

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

## A sorted integer array is given, we have to construct its squared array in sorted manner and return it.
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

## Branch Sums in a Binary tree
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

## You are given an array of integers and an integer. Write a function that moves all instances of that integer in the array to the end of the array and returns the array
- Use two pointer approach
- Apart from the approach below, we can use the variant of Dutch National Flag algorithm.
  - If a[i] is 'k', swap a[i] and a[j] and decrement j.
  - Else increment i.
  - Completes in O(N).
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

## Two arrays are given - redshirt and blueshirts. They are to be arranged in front and back rows such that the items in the back row are strictly greater than that of the first row. Red and Blue arrays cannot be mixed
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

## Return the first duplicate value in an array given that all the numbers are between 1-n.
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

## Identify the LCA for a BST
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

## Identify the LCA for a BT
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

## Three Number Sort - Similar to Dutch National Flag algorithm, except the sort order is dictated by a second array.
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
- Time Complexity O(N)
- Space Complexity O(1).

## Find two elements from two different arrays of different sizes that have the least difference
- Brute force O(N^2) is possible, but we can do better.
- We can use two pointer approach and solve it. But usually, two pointer approach needs arrays to be sorted.
```
import java.util.*;

class Program {
  public static int[] smallestDifference(int[] arrayOne, int[] arrayTwo) 
  {
  	// Sort both the arrays
	Arrays.sort( arrayOne );
	Arrays.sort( arrayTwo );

	int low1 = 0;
	int low2 = 0;
	int difference = Integer.MAX_VALUE;
	int num1 = 0;
	int num2 = 0;

	while( low1 < arrayOne.length && low2 < arrayTwo.length )
	{
			int currDiff = Math.abs( arrayOne[low1] - arrayTwo[low2] );
			if( currDiff < difference )
			{
					difference = currDiff;
				  num1 = arrayOne[low1];
				  num2 = arrayTwo[low2];
			}

		  if( arrayOne[low1] > arrayTwo[low2] )
			{
				low2++;
			}
			else
			{
				low1++;
			}
	}

	return new int[]{ num1, num2 };
  }
}
```
- Time Complexity O(NlogN) + O(MlogM)
- Space Complexity O(1).

## Validate if a tree is a BST
- Checking if each LST and RST are BSTs has a flaw.
- It does not cover cases like these below.
![image](https://user-images.githubusercontent.com/42272776/114563641-3648e200-9c8d-11eb-8583-d98c5edac0f9.png)
- Basically, this approach does not really guarantee that the root BST is actually a BST.
- Correct approach is actually ensuring that the maximum value at LST is < root and minimum value in RST is > root.
```
import java.util.*;

class Program {
  public static boolean validateBst(BST tree) 
  {	
	return isBST( tree, Integer.MIN_VALUE, Integer.MAX_VALUE);		
  }
	
  public static boolean isBST(BST root, int min, int max)
  {
	if( root == null )
	return true;
		
	System.out.println( "Comparing at root.value " + root.value + " min " + min + " max " + max);
	return root.value >= min && 
               root.value < max && 
	       isBST( root.left, min, root.value ) &&
	       isBST( root.right, root.value, max  );
  }

  static class BST 
  {
      public int value;
      public BST left;
      public BST right;

      public BST(int value) 
      {
          this.value = value;
      }
  }
}
```

## Three Number Sum
- Use two pointer approach for solving this.
- In this case, the array contents are distinct. So incrementing low and high when there is a match does not make a difference. Otherwise, it is better to increment only one of them.
```
import java.util.*;

class Program 
{
  public static List<Integer[]> threeNumberSum(int[] a, int targetSum) 
  {
  	List<Integer[]> response = new ArrayList<Integer[]>();
		
  	Arrays.sort(a);
	for(int inx=0; inx<a.length-1;++inx)
	{
		int low = inx+1;
		int high = a.length-1;

		while( low < high ) // To prevent counting of the same index twice.
		{
			if( a[inx] + a[low] + a[high] == targetSum )
			{
				Integer integers[] = new Integer[3];
				integers[0] = a[inx];
				integers[1] = a[low];
				integers[2] = a[high];

			  response.add( integers );

				low++;
				high--;
			}
		  	else if(a[inx] + a[low] + a[high] < targetSum)
			{
				low++;	
			}
			else
			{
				high--;
			}						
		}				
	}

    return response;
    }
}
```
- Time Complexity O(N^2)
- Space Complexity O(1).

## Sum of linked lists which have their head pointers pointing to least significant digit of an array - 3479 and 945 should return 29201.
```
import java.util.*;

class Program {
  // This is an input class. Do not edit.
  public static class LinkedList {
    public int value;
    public LinkedList next;

    public LinkedList(int value) {
      this.value = value;
      this.next = null;
    }
  }

  public LinkedList sumOfLinkedLists(LinkedList linkedListOne, LinkedList linkedListTwo) 
  {
 	LinkedList headNode = null;
	LinkedList lastNode = null;
	int carry = 0;

	while( linkedListOne != null || linkedListTwo != null)
	{
	    int digit = 0;
	    int digitSum = ( linkedListOne != null ? linkedListOne.value : 0 ) 
			 + ( linkedListTwo != null ? linkedListTwo.value : 0 )
		         + carry;
	    if( digitSum > 9 )
	    {
	        // Ex: 14
		digit = digitSum % 10;
		carry = 1;
	    }
	    else
	    {
	        // Ex: 8
		carry = 0;
		digit = digitSum;
	    }

            LinkedList node = new LinkedList(digit);
	    if( headNode == null )
	    {
		headNode = node;
		lastNode = node;
	    }
	    else
	    { 
		lastNode.next = node;
		lastNode = node;
	    }

	    if( linkedListOne != null)
	    linkedListOne = linkedListOne.next;

            if(linkedListTwo != null)
	    linkedListTwo = linkedListTwo.next;
	}

	if( carry > 0 )
	{
	    LinkedList node = new LinkedList(carry);
	    lastNode.next = node;
	    lastNode = node;
	}

	return headNode;
  }
}
```
- Time Complexity O(M+N)
- Space Complexity O(1).

## Nth Fibonacci Number

public static int getNthFib(int n) {
	if( n == 1 )
		return 0;
	else if( n == 2 )
		return 1;
	else
	{
		return getNthFib( n - 1 ) + getNthFib( n - 2 );
	}
}

- Time Complexity O(N)
- Space Complexity O(1).

## Merge two sorted Linked List
Be careful with incrementing the pointer and setting the front and rear of the new list.
```
public static LinkedList mergeLinkedLists(LinkedList headOne, LinkedList headTwo) {
    
	LinkedList mergedListHead = null;
	LinkedList mergedListLast = null;
	while( headOne != null && headTwo != null)
	{
		LinkedList temp = null;
		if( headOne.value > headTwo.value )
		{
			temp = new LinkedList( headTwo.value );
			headTwo = headTwo.next;
		}
		else
		{
			temp = new LinkedList( headOne.value );
			headOne = headOne.next;
		}

		if( mergedListHead == null )
		{
			mergedListHead = temp;
			mergedListLast = temp;
		}
		else
		{
			mergedListLast.next = temp;
			mergedListLast = temp;
		}
	}

	while( headOne != null )
	{
		LinkedList temp = new LinkedList( headOne.value );

		if( mergedListHead == null )
		{
			mergedListHead = temp;
			mergedListLast = temp;
		}
		else
		{
			mergedListLast.next = temp;
			mergedListLast = temp;
		}

		headOne = headOne.next;
	}

	while( headTwo != null )
	{
		LinkedList temp = new LinkedList( headTwo.value );

		if( mergedListHead == null )
		{
			mergedListHead = temp;
			mergedListLast = temp;
		}
		else
		{
			mergedListLast.next = temp;
			mergedListLast = temp;
		}

		headTwo = headTwo.next;
	}

    return mergedListHead;
  }
```
- Time Complexity O(M+N)
- Space Complexity O(1)

##  Find closest value in BST
Use Binary Search algorithm to find the node that has the least difference.
```
import java.util.*;

class Program {
  public static int findClosestValueInBst(BST tree, int target) {
    // Write your code here.
    return closestValue( tree, target, Integer.MAX_VALUE, Integer.MAX_VALUE);
  }

public static int closestValue( BST root, int target, int lastLeastDiff, int lastLeastValue)
{
	if( root == null )
	{
			return lastLeastValue;
	}

	if( root.value == target )
	{
			return root.value;
	}

	int currDifference = Math.abs( target-(root.value) );
	if( currDifference < lastLeastDiff )
	{
			lastLeastDiff = currDifference;
			lastLeastValue = root.value;
	}

	if( root.value < target )
	{
			return closestValue( root.right, target, lastLeastDiff, lastLeastValue);
	}
	else
	{
			return closestValue( root.left, target, lastLeastDiff, lastLeastValue);
	}
}


  static class BST {
    public int value;
    public BST left;
    public BST right;

    public BST(int value) {
      this.value = value;
    }
  }
}
```
- Time Complexity O(logN)
- Space Complexity O(logN)

## Remove duplicates in a Linked List
Be careful with the pointer increments.
```
public LinkedList removeDuplicatesFromLinkedList(LinkedList head)
{
	LinkedList curr = head.next;
	LinkedList prev = head;

	while( curr != null )
	{
		if( prev.value == curr.value)
		{
		        // Do not increment the PREV pointer to next of CURR when CURR is to be removed.
			prev.next = curr.next;
			curr = curr.next;
		}
		else
		{
		        // Increment PREV and CURR as normal
			prev = curr;
			curr = curr.next;
		}
	}

	return head;		
}
```
- Time Complexity O(N)
- Space Complexity O(1)

## Invert a Binary Tree
- Capture the updated LST and RST into variables instead of directly assigning them.
```
public static BinaryTree invertTree( BinaryTree tree)
{
	if( tree == null )
	{
		return null;
	}

	BinaryTree leftSubTree = invertTree( tree.left );
	BinaryTree rightSubTree = invertTree( tree.right );

	tree.right = leftSubTree;
	tree.left = rightSubTree;

	return tree;
}
```
- Time Complexity O(N)
- Space Complexity O(N)

## Diameter of a BT
```
import java.util.*;

class Program 
{
	  // This is an input class. Do not edit.
	  static class BinaryTree {
	    public int value;
	    public BinaryTree left = null;
	    public BinaryTree right = null;

	    public BinaryTree(int value) 
	    {
	      this.value = value;
	    }
}

public int binaryTreeDiameter(BinaryTree root) 
{
	return diameter( root ) - 1;
}

public int diameter(BinaryTree root)
{
	if( root == null )
		return 0;

	// get the diameter of left and right sub-trees
	int ldiameter = diameter(root.left);
	int rdiameter = diameter(root.right);

	int lheight = height(root.left);
	int rheight = height(root.right);

	return Math.max( lheight + rheight + 1, Math.max( ldiameter,  rdiameter ));
}

public int height( BinaryTree root )
{
	if( root == null )
		return 0;

	int lheight = height(root.left);
	int rheight = height(root.right);
	return ( 1 + Math.max( lheight, rheight ) );
}
}

```
- Time Complexity O(N^2)
- Space Complexity O(N)

Approach 2

```
using namespace std;

// This is an input class. Do not edit.
class BinaryTree {
public:
  int value;
  BinaryTree *left;
  BinaryTree *right;

  BinaryTree(int value) {
    this->value = value;
    left = nullptr;
    right = nullptr;
  }
};

int diameterOpt(BinaryTree* root, int* height)
{
    // lh --> Height of left subtree
    // rh --> Height of right subtree
    int lh = 0, rh = 0;
 
    // ldiameter  --> diameter of left subtree
    // rdiameter  --> Diameter of right subtree
    int ldiameter = 0, rdiameter = 0;
 
    if (root == NULL) {
        *height = 0;
        return 0; // diameter is also 0
    }
 
    // Get the heights of left and right subtrees in lh and
    // rh And store the returned values in ldiameter and
    // ldiameter
    ldiameter = diameterOpt(root->left, &lh);
    rdiameter = diameterOpt(root->right, &rh);
 
    // Height of current node is max of heights of left and
    // right subtrees plus 1
    *height = max(lh, rh) + 1;
 
    return max(lh + rh + 1, max(ldiameter, rdiameter));
}

int binaryTreeDiameter(BinaryTree *tree) {
  // Write your code here.
	int height = 0;
  return diameterOpt(tree, &height) - 1;
}
```
- Time Complexity O(N)
- Space Complexity O(1)

## Kth largest element in a BST
- Note that we have to maintain a variable that is outside of the recursion stack.
- We employ a reverse inorder traversal - Right, Root, Left.
```
import java.util.*;

class Program {
  // This is an input class. Do not edit.
	int found_value = 0;
	int master_count = 0;

  static class BST {
    public int value;
    public BST left = null;
    public BST right = null;

    public BST(int value) {
      this.value = value;
    }
  }

  public int findKthLargestValueInBst(BST tree, int k) {
    // Write your code here.
		kthHighestNode( tree, k);
    return found_value;
  }
	
public void kthHighestNode( Program.BST root, int k )
{
	if( root == null)
		return;

	if( master_count < k)
	kthHighestNode( root.right, k );

	master_count++;
	if( master_count == k )
	{
		found_value = root.value;
		return;
	}

	if( master_count < k)
	kthHighestNode( root.left, k );
}
}
```
- Time Complexity O(h+k) where h is height of the tree and k is the input parameter
- Space Complexity O(h)

## Write an API to return a boolean indicating whether the binary tree is height balanced
```
import java.util.*;

class Program {
  // This is an input class. Do not edit.
  static class BinaryTree {
    public int value;
    public BinaryTree left = null;
    public BinaryTree right = null;

    public BinaryTree(int value) {
      this.value = value;
    }
  }

static class Violations 
{
	public boolean found;

	public Violations() {
		found = false;
	}
}

public int heightBalancedBinaryTree(BinaryTree root, Violations violations) 
{
	if( root == null )
		return 0;

	if( violations.found )
	{
		return Integer.MIN_VALUE;
	}

	int leftHeight = 1 + heightBalancedBinaryTree( root.left, violations );
	int rightHeight = 1 + heightBalancedBinaryTree( root.right, violations );

	if( Math.abs( leftHeight - rightHeight ) > 1 )
	{
		violations.found = true;
		return Integer.MIN_VALUE;
	}

	return Math.max( leftHeight, rightHeight );
}

public boolean heightBalancedBinaryTree(BinaryTree root)
{
	Violations violations = new Violations();
	heightBalancedBinaryTree(root, violations );

	return !violations.found;
}
}
```
- Time Complexity O(N)
- Space Complexity O(N)

## Find the sum of the depths of all the nodes in a Binary Tree.
- Traverse all the nodes with a counter that maintains the levels as well.
```
using namespace std;

class BinaryTree {
public:
  int value;
  BinaryTree *left;
  BinaryTree *right;

  BinaryTree(int value) {
    this->value = value;
    left = nullptr;
    right = nullptr;
  }
};


// depth = 0
int nodeDepths(BinaryTree *root, int depth) 
{
		if( root == NULL )
		{
				return 0;
		}
	
		int lDepth = nodeDepths( root->left, depth+1 );
		int rDepth = nodeDepths( root->right, depth+1 );

		return lDepth + rDepth + depth;
}

int nodeDepths(BinaryTree *root)
{
		return nodeDepths(root, 0);
}
```
- Time Complexity O(N)
- Space Complexity O(1)

## Get the inorder successor for a given node in a Binary Tree
- Things to consider
  - If the node has right sub tree, the left most node in that sub tree will be the inorder successor
  - If the node does not have right sub tree, then one of the ancestors of the node will be the inorder successor
    - If the node that we are searching for is the right most node, then the above case needs to be handled carefully to avoid NULL dereference.
    - In this case, it will traverse back to the root of the tree and its parent is NULL. Hence the condition temp != NULL.
```
using namespace std;

// This is an input class. Do not edit.
class BinaryTree {
public:
  int value;
  BinaryTree *left = nullptr;
  BinaryTree *right = nullptr;
  BinaryTree *parent = nullptr;

  BinaryTree(int value) { this->value = value; }
};

BinaryTree* findSuccessor(BinaryTree *root, BinaryTree *node) 
{
	// If the node has right sub tree, the left most node in that sub tree will be the inorder successor
	// If the node does not have right sub tree, then one of the ancestors of the node will be the inorder successor.

	// Case 1
	if( node == NULL )
	return NULL;

	else if( node->right != NULL )
	{
		BinaryTree* temp = node->right;

		while( temp->left != NULL )
		{
			temp = temp->left;
		}

		return temp;
	}
	else
	{
		BinaryTree* temp = node->parent;

		while( temp != NULL && node != temp->left )
		{
			node = temp;
			temp = temp->parent;
		}

		return temp;
	}
}
```
- Time Complexity O(h) where h is the height of the tree
- Space Complexity O(1)

## You are given a sorted array. You have to build a BST that shall have the smallest height possible. This function should minimize the height.
```
import java.util.*;

class Program {
  public static BST minHeightBst(List<Integer> array) 
	{
			return buildBST( array, 0, array.size()-1 );
  	}
	
	public static BST buildBST( List<Integer> array, int low, int high )
	{
			if( low > high )
			{
					return null;
			}
		
			int mid = (low + high) / 2;
			BST root = new BST(array.get(mid));
			root.left = buildBST(array, low, mid-1);
			root.right = buildBST(array, mid+1, high);

			return root;		
	}
	
  static class BST {
    public int value;
    public BST left;
    public BST right;

    public BST(int value) {
      this.value = value;
      left = null;
      right = null;
    }

    public void insert(int value) {
      if (value < this.value) {
        if (left == null) {
          left = new BST(value);
        } else {
          left.insert(value);
        }
      } else {
        if (right == null) {
          right = new BST(value);
        } else {
          right.insert(value);
        }
      }
    }
  }
}
```
- Time Complexity O(N)
- Space Complexity O(N)

## You are given two arrays. Build a new array, which has the product of all the numbers excepting 'inx'.
- This is not a straightforward problem.
- If the array has no zeroes, then the solution is trivial.
- If the array has 1 zero, then product should not include that 0 value.
- If the array has more than one zero, then every possible product will be zero.
```
class Solution {
    public int[] productExceptSelf(int[] nums) 
    {
        int product = 1;
        boolean nonZeroesExist = false;
        int zeroCount = 0;
        int productArray[] = new int[nums.length];
        for(int inx =0; inx < nums.length; inx++)
        {
            if( nums[inx] != 0 )
            {
                product = product * nums[inx];
                nonZeroesExist = true;
            }
            else
                zeroCount++;
        }

        for(int inx =0; inx < nums.length; inx++)
        {
            if( zeroCount > 1 )
                productArray[inx] = 0;
            else if( zeroCount > 0 )
            {
                if( nums[inx] != 0 )
                    productArray[inx] = 0;
                else
                    productArray[inx] = product;
            }
            else
            {
                productArray[inx] = product/nums[inx];
            }
        }
        
        return productArray;
    }
}
```
- Time Complexity O(N)
- Space Complexity O(N)

## Given an array of positive integers, find the least sum that you cannot make
- This works because the sequence is positive.
- And because if change+1 is less than coins[inx], then we cannot make change+1.

public int nonConstructibleChange(int[] coins) 
{
	Arrays.sort(coins);

	int change = 0;

	for(int inx = 0; inx < coins.length; ++inx )
	{
		if( change + 1 < coins[inx])
			return change + 1;

		change = change + coins[inx];
	}

	return change + 1;
}
- Time Complexity O(N)
- Space Complexity O(1)

### You are given an array of query execution times. Return the minimum waiting time for the execution of all the queries.
Ex: 3, 2, 1, 2, 6.

```
import java.util.*;

class Program 
{
  public int minimumWaitingTime(int[] queries)
  {
	Arrays.sort(queries);

	int waitingTime = 0;
	int totalWaitingTime = 0;

	for(int inx = 1; inx < queries.length; inx++)
	{
		waitingTime += queries[inx-1];
		totalWaitingTime += waitingTime;
	}

	return totalWaitingTime;
  }
}
```
- Time Complexity O(NLogN)
- Space Complexity O(1)

## You are given two different arrays of same size that are not sorted. These represent the velocity of bikers on a tandem bike. Based on an input boolean variable determine the maximum and minimum velocity possible.
```
import java.util.*;

class Program {

  public int tandemBicycle(int[] red, int[] blue, boolean fastest) 
  {    
	Arrays.sort( red );
	Arrays.sort( blue );

	int speed = 0;
	for(int inx = 0; inx < red.length; inx++)
	{
		if(fastest)
			speed += Math.max( red[inx], blue[blue.length-1-inx]);
		else
			speed += Math.max( red[inx], blue[inx]);
	}

	return speed;
  }
}
```
- Time Complexity O(NLogN)
- Space Complexity O(1)

## Delete Kth node of a Linked List from the back.
- Always count the head as 1 during this problem.
```
import java.util.*;

class Program 
{
	public static void removeKthNodeFromEnd(LinkedList head, int k) 
	{
		if( head == null)
			return;

		LinkedList ptr = head;

		// k = 2
		// a  b  c  d  e  f
		int count = 1;
		while(count < k)
		{
				ptr = ptr.next;

				if(ptr == null)
						return;

				count++;
		}

		LinkedList slowPtr = null;
		LinkedList prevPtr = null;

		while( ptr != null )
		{
				ptr = ptr.next;

				if(slowPtr == null)
				{
						slowPtr = head;
				}
				else
				{
						prevPtr = slowPtr;
						slowPtr = slowPtr.next;
				}
		}

		if(slowPtr == head)
		{
				LinkedList tmp = head.next;
				head.value = tmp.value;
				head.next = tmp.next;
		}
		else
		{
				prevPtr.next = slowPtr.next;
		}
		return;
	}

  static class LinkedList {
    int value;
    LinkedList next = null;

    public LinkedList(int value) {
      this.value = value;
    }
  }
}
```
- Time Complexity O(N)
- Space Complexity O(1)

## Write a DFS Traversal for an acyclic graph
```
import java.util.*;

class Program {
  // Do not edit the class below except
  // for the depthFirstSearch method.
  // Feel free to add new properties
  // and methods to the class.
  static class Node {
    String name;
    List<Node> children = new ArrayList<Node>();

    public Node(String name) {
      this.name = name;
    }

    public List<String> depthFirstSearch(List<String> array) 
		{
				dfs( this, array);
				return array;
    }
		
		public void dfs( Node root, List<String> dfsTraversal )
		{
				if( root == null )
					return;

				dfsTraversal.add( root.name );

				for( int inx = 0; root.children != null && inx < root.children.size(); ++inx )
				{
						dfs( root.children.get(inx), dfsTraversal );
				}

				return;
		}

    public Node addChild(String name) {
      Node child = new Node(name);
      children.add(child);
      return this;
    }
  }
}
```
- Time Complexity: O(N)
- Space Complexity: O(N)

## Implement a MinMax Stac
import java.util.*;
```
class Program {
  // Feel free to add new properties and methods to the class.
  static class MinMaxStack 
  {

	class StackElement
	{
		int minTillNow;
		int maxTillNow;
		int value;

		StackElement(int value, int min, int max )
		{
			this.value = value;
			this.minTillNow = min;
			this.maxTillNow = max;
		}
	}
		
	List<StackElement> stackContent = new ArrayList<StackElement>();

    	public int peek() 
	{
		return stackContent.get(stackContent.size()-1).value;
    	}

    	public int pop() 
	{
		StackElement element = stackContent.get(stackContent.size()-1);
		stackContent.remove(stackContent.size()-1);
  	    	return element.value;
    	}

    	public void push(Integer number)
	{
		int min, max;
		if( stackContent.size() == 0 )
		{
			min = number;
			max = number;
		}
		else
		{
			min = stackContent.get(stackContent.size()-1).minTillNow < number ? stackContent.get(stackContent.size()-1).minTillNow : number;
			max = stackContent.get(stackContent.size()-1).maxTillNow > number ? stackContent.get(stackContent.size()-1).maxTillNow : number;
		}
			
    	  	stackContent.add( new StackElement( number, min, max ) );
  	    	return;
    	}

    	public int getMin()
	{
    	  	return stackContent.get(stackContent.size()-1).minTillNow;
    	}

    	public int getMax()
	{
      		return stackContent.get(stackContent.size()-1).maxTillNow;
    	}
  }
}
```
- Time Complexity: O(N)
- Space Complexity: O(N)

## Caesar Cipher Encryption - xyz with two rotations becomes zab
- Important thing to note here is to do a modulo operation to reduce traversals.
- And logically making the additions to fall within a-z range.
```
import java.util.*;

class Program {

	public static String caesarCypherEncryptor(String str, int key) 
	{
		StringBuilder sBuilder = new StringBuilder(str);
		key = key % 26;

		int zCharLocation = (int) 'z';
		int aCharLocation = (int) 'a';
		for(int inx = 0; inx < sBuilder.length(); ++inx)
		{
			int currChar = (int) sBuilder.charAt(inx);
			int newChar = currChar + key;

			if( newChar > zCharLocation )
			{
				int spillOver = newChar - zCharLocation;

				newChar = aCharLocation - 1 + spillOver;
			}

			sBuilder.setCharAt(inx, (char)newChar);
		}

		return sBuilder.toString();
  	}	
}
```
- Time Complexity: O(N)
- Space Complexity: O(N)

## You are given an array and a value. From the array, you need to build combination of two integers whose sum is smallest.
- Ex: k = 3 and tasks[] = { 1, 3, 5, 3, 1, 4 } 
- The trick here is you cant sort.
- You cant also remove elements from the array list as it would invalidate other entries down the line.
- So the ones that you have visited, mark with -1 as this array is always positive.
- Also, if you start from array index 0 for finding both the numbers for a given iteration, equal elements which may lie at the end will miss.
- Ex: for the above array, you would get { {0,2}, {4,5}, {1,1} }. Notice the last pair which should have been {1,3}.
```
import java.util.*;

class Program 
{
  	public static ArrayList<ArrayList<Integer>> taskAssignment(int k, ArrayList<Integer> tasks) 
	{  	
		ArrayList<ArrayList<Integer>> assignments = new ArrayList<ArrayList<Integer>>();

		while(assignments.size() < k)
		{
			int min = Integer.MAX_VALUE;
			int smallIndex = -1;
			int max = Integer.MIN_VALUE;
			int largeIndex = -1;

			for( int inx = 0, jnx = tasks.size()-1; inx < tasks.size() && jnx >= 0; )
			{
				if( tasks.get(inx) == -1)
				{
					inx++;
					continue;
				}
				
				if( tasks.get(jnx) == -1)
				{
					jnx--;
					continue;
				}
				
				if( min > tasks.get(inx))
				{
					min = tasks.get(inx);
					smallIndex = inx;
				}
				if( max < tasks.get(inx))
				{
					max = tasks.get(inx);
					largeIndex = inx;
				}
				
				inx++;
				jnx--;
			}

			tasks.set(smallIndex, -1);
			tasks.set(largeIndex, -1);
		
			ArrayList<Integer> assignment = new ArrayList<Integer>();
			assignment.add( smallIndex );
			assignment.add( largeIndex );	
			assignments.add(assignment);
		}

    		return assignments;
  	}
}
```
- Time Complexity: O(N)
- Space Complexity: O(N)

## Breadth First Search in a Graph with no cycles ( Generic tree )
```
import java.util.*;

class Program {
  // Do not edit the class below except
  // for the breadthFirstSearch method.
  // Feel free to add new properties
  // and methods to the class.
  static class Node {
    String name;
    List<Node> children = new ArrayList<Node>();

    public Node(String name) {
      this.name = name;
    }

    	public List<String> breadthFirstSearch(List<String> array) 
	{
		// Add the current node to the queue
		List<Node> queue = new ArrayList<Node>();
		queue.add(this);
		bfs( array, queue );
  	    	return array;
    	}
		
	public void bfs( List<String> bfs, List<Node> queue )
	{
		// Remove content from queue until its empty and visit them
		while( !queue.isEmpty() )
		{
			Node currNode = queue.get(0);
			bfs.add(currNode.name);
			queue.remove(0);

			// Once you visit a node, add its children to the queue.
			// queue.add( null );
			for( int inx = 0; currNode.children != null && inx < currNode.children.size(); ++inx )
			{
				queue.add( currNode.children.get(inx) );
			}
		}
	}

    public Node addChild(String name) {
      Node child = new Node(name);
      children.add(child);
      return this;
    }
  }
}
```
- Time Complexity: O(v+e)
- Space Complexity: O(v) where v is the number of vertices and e is the number of edges in the graph.

## Validating a string for brackets ({[]})
- There are three possible cases here
  - More left braces, in which case, the stack will not be empty at the end of the processing.
  - More right braces, in which case, we will hit stack underflow.
  - Equal number of left and right braces.

```
import java.util.*;

class Program 
{
	static List<Character> stack = new ArrayList<Character>();

	public static int pop()
	{
		if( stack.size() == 0 )
				return -1;

		char ch = stack.get(stack.size()-1);
		stack.remove(stack.size()-1);

		return (int)ch;
	}

	public static void push( char ch )
	{
		stack.add( ch );							
	}
	// ([{]}])
	public static boolean balancedBrackets(String str) 
	{
		boolean bracketsBalanced = true;

		for(int inx = 0; inx < str.length(); ++inx )
		{
			char currChar = str.charAt(inx);

			switch( currChar )
			{
				case '(':
				case '{':
				case '[': push( currChar );
								  break;

				case ')':	
				case '}':
				case ']':	int tosCharInt = pop();
						if( tosCharInt == -1)
						{
								bracketsBalanced = false;
								break;
						}

						if(( (char)tosCharInt == '(' && currChar == ')') || 
							 ( (char)tosCharInt == '{' && currChar == '}') || 
							 ( (char)tosCharInt == '[' && currChar == ']') )
							break;
						else
						{
								bracketsBalanced = false;
								break;
						}
				default: break; // ignore
			}
		}

		if( !stack.isEmpty())
		{
			bracketsBalanced = false;
		}

		stack.clear();
		return bracketsBalanced;
	}
}
```
- Time Complexity: O(N)
- Space Complexity: O(N)

## Run length encoding
- Ex ************^^^^^^^$$$$$$%%%%%%%!!!!!!AAAAAAAAAAAAAAAAAAAA
- Ex AAAAAAAAAAAAAAAAABBBBB should be 9A8A5B
- Better alternative at the end of the for loop can be done, but this is the general code.
```

import java.util.*;

class Program {
  public String runLengthEncoding(String string) {

		StringBuilder sb = new StringBuilder();
		
		int count = 1;
		char currChar = string.charAt(0);
		for(int inx = 1; inx < string.length(); inx++)
		{
				// AAA
				// AAB
				// AAAAAAAAAAAABBCCC
				if( currChar == string.charAt(inx) )
				{
						count++;
				}
				else
				{
						if( count > 9 )
						{
									// Ex 1: 18 - 9A9A
									// Ex 2: 23 - 9A9A5A
									int rem = count % 9;
									count = count / 9;

									for( int jnx = 0; jnx < count; jnx++ )
									{
											sb.append( "9" + 	currChar );						
									}

									if( rem> 0 )
											sb.append( rem + "" + currChar );								
						}
						else
						{
								sb.append( count + "" + currChar );
						}

						count = 1;
						currChar = string.charAt(inx);
				}
		}
		
		if( count > 9 )
		{
			// Ex 1: 18 - 9A9A
			// Ex 2: 23 - 9A9A5A
			int rem = count % 9;
			int multiple = count / 9;

			for( int jnx = 0; jnx < multiple; jnx++ )
			{
					sb.append( "9" + 	currChar );						
			}

			sb.append( rem + "" + currChar );
		}
		else
		{
				sb.append( count + "" + currChar );
		}
  
		return sb.toString();
	}
}
```
- Time Complexity: O(N)
- Space Complexity: O(N)

## Generate Document - Check if the String 'document' can be formed from the String 'characters'
```
import java.util.*;

class Program {

  public boolean generateDocument(String characters, String document) 
  {
	if( document.length() == 0 )
		return true;

	if( characters.length() < document.length() )
		return false;

	Map<Character, Integer> characterDictionary = new HashMap<Character, Integer>();

	// Cache population
	for( int inx = 0; inx < characters.length(); ++inx )
	{
			char _char = characters.charAt(inx);

			if( !characterDictionary.containsKey( _char ))
			{
				// Add with value 1
				characterDictionary.put( _char, 1 );
			}
			else
			{
				// Increment the value
				characterDictionary.put( _char, characterDictionary.get( _char ) + 1 );
			}
	}

	// Cache look up
	for( int inx = 0; inx < document.length(); ++inx )
	{
		char _char = document.charAt(inx);
		System.out.println( _char + " " + characterDictionary.containsKey( _char ) );
		if( !characterDictionary.containsKey( _char ))
		{
			return false;
		}
		else
		{
			int frequency = characterDictionary.get( _char );
			if( frequency == 0 )
				return false;

			characterDictionary.put( _char, characterDictionary.get( _char ) - 1 );
		}
	}

	return true;
  }
}
```
- Time Complexity: O(M+N)
- Space Complexity: O(c) where M is Characters length, N is Document length, and c is the number of unique characters in Characters string.

## Find the least index in an array, where a[index] = index. If no such index is available, return -1.
- Basically, even if we find an index where a[index] == index, there is every chance for a smaller index where the same can hold true.
- So we need to check the previous index location in case of a match to not miss it.
```
import java.util.*;

class Program {
  public int indexEqualsValue(int[] array) {
    // Write your code here.
    return search( array, 0, array.length-1);
  }

public int search( int a[], int low, int high )
{
	if( low > high )
	{
		return -1;
	}

	int mid = ( low + high ) / 2;

	if( a[mid] > mid)
		return search( a, low, mid-1);
	else if( a[mid] < mid)
		return search( a, mid+1, high);
	else
	{
		if( mid > 0)
		{
			if( a[mid-1] == mid-1 )
				return search( a, low, mid-1 );
		}
		return mid;
	}
   }
}
/*
-5  -3  0  1  4  5  9
 0   1  2  3  4  5  6
low  =  0   5
mid  =  3   4
high =  6   6
	*/
	
```
- Time Complexity: O(logN)
- Space Complexity: O(1)

## Kadane's algorithm
```
public static int kadanesAlgorithm(int[] array) 
{
    int maxSumTillNow = array[0];
    int cummulativeSum = array[0];
    for( int inx = 1; inx < array.length; ++inx )
    {
	cummulativeSum = Math.max( array[inx], cummulativeSum + array[inx] );
	maxSumTillNow = Math.max( maxSumTillNow, cummulativeSum );				
    }		
    return maxSumTillNow;
}
```
- Time Complexity: O(N)
- Space Complexity: O(1)

## Detecting infinite linked list
- Start both the pointers from head node.
![Cycle In LinkedList](https://user-images.githubusercontent.com/42272776/116383769-cada4500-a834-11eb-8f44-dde455b2f1bb.jpg)

```
import java.util.*;

class Program {
public static LinkedList findLoop(LinkedList head) 
{
	if( head == null || head.next == head )
		return head;

	LinkedList slowPtr = head;
	LinkedList fastPtr = head;

	do
	{
		slowPtr = slowPtr.next;
		fastPtr = fastPtr.next;
		fastPtr = fastPtr.next;
	} while( slowPtr != fastPtr );

	fastPtr = head;

	while( fastPtr !=  slowPtr )
	{
		slowPtr = slowPtr.next;
		fastPtr = fastPtr.next;
	}

	return slowPtr;
  }

  static class LinkedList {
    int value;
    LinkedList next = null;

    public LinkedList(int value) {
      this.value = value;
    }
  }
}
```
- Time Complexity: O(N)
- Space Complexity: O(1)

## Selection algorithm
- Selection algorithm for finding the kth largest element involves comparision in descending order and searching.
```
while( pivot < a[i] && i < high ) // i < high because we want to ensure that i does not spill over
    i++;
while( pivot > a[j] )
    j--;
```
- Selection algorithm for finding the kth smallest element involves comparision in ascending order and searching.
```
import java.util.*;

class Program 
{
	public static int quickselect(int[] array, int k) {
		// Write your code here.
		return partition( array, 0 , array.length-1, k-1 );
	}

	public static int partition( int a[], int low, int high, int pos )
	{
		while( true )
		{
			int pivot = a[low];
			int i = low + 1;
			int j = high;

			while( i <= j )
			{
				while(pivot > a[i] & i < high)
					i++;

				while(pivot < a[j])
					j--;

				if( i < j )
				{
					int temp = a[i];
					a[i] = a[j];
					a[j] = temp;
					i++;
					j--;
				}
				else
				{
					i++;	
				}
			}

			a[low] = a[j];
			a[j] = pivot;

			if( pos == j )
				return a[j];
			else if( pos < j)
			{
				high = j - 1;
			}
			else
			{
				low = j + 1;
			}
		}
	}
}
```
- Time Complexity: O(N) to O(N2)
- Space Complexity: O(1)

## Build BST from a Pre-Order array using iteration
```
import java.util.*;

class Program 
{
	// This is an input class. Do not edit.
	static class BST 
	{
	    public int value;
	    public BST left = null;
	    public BST right = null;

	    public BST(int value) 
	    {
		this.value = value;
	    }
	}

  	public BST reconstructBst(ArrayList<Integer> preOrder) 
	{
		BST root = null;
		for( int inx = 0; inx < preOrder.size(); ++inx )
		{
			BST node = buildTree( preOrder.get(inx), root );
			if( root == null )
				root = node;					
		}				

		return root;
  	}
	
	public BST buildTree( int value, BST root )
	{
		BST node = new BST(value);

		if( root == null )
		{
			root = node;
			return root;
		}
	
		BST parentNode = root;
		BST prevNode = null;

		while( parentNode != null )
		{
			if( node.value >= parentNode.value )
			{
				prevNode = parentNode;
				parentNode = parentNode.right; 
			}
			else
			{
				prevNode = parentNode;
				parentNode = parentNode.left;
			}
		}

		if(prevNode.value > node.value) 
		{
			prevNode.left = node;
		}
		else
		{
			prevNode.right = node;
		}

		return node;
	}	
}
```
- Time Complexity: O(NlogN)
- Space Complexity: O(1)

## Build BST from a Pre-Order array using recursion
```
import java.util.*;

class Program {
  // This is an input class. Do not edit.
  static class BST {
    public int value;
    public BST left = null;
    public BST right = null;

    public BST(int value) {
      this.value = value;
    }
  }

	public BST reconstructBst(ArrayList<Integer> preOrderTraversalValues) 
	{
		if( preOrderTraversalValues.size() == 0 )
			return null;

		BST node = new BST( preOrderTraversalValues.get(0) );

		ArrayList<Integer> leftChildContent = new ArrayList<Integer>();
		ArrayList<Integer> rightChildContent = new ArrayList<Integer>();

		for( int inx = 1; inx < preOrderTraversalValues.size(); ++inx )
		{
			if( preOrderTraversalValues.get(0) <= preOrderTraversalValues.get(inx))
			{
				rightChildContent.add( preOrderTraversalValues.get(inx) );
			}
			else
			{
				leftChildContent.add( preOrderTraversalValues.get(inx) );
			}
		}

		node.left = reconstructBst( leftChildContent );
		node.right = reconstructBst( rightChildContent );
		return node;
	}
}
```
- Time Complexity: O(N)
- Space Complexity: O(N)

## Product Sum - [5,2, [7, -1], 3, [6, [-13, 8], 4]]
- This will evaluate to 5 + 2 + 2(7-1) + 3 + 2 ( 6 + 3 ( -13 + 8 ) + 4 ) = 12.
- Ex: [1,2,[3],4,5] = 18
- Ex: [[[[[5]]]]] = 600
- Be careful to multiply the result of the recursion sum with productIncrement as well.
```
import java.util.*;

class Program 
{
	// Tip: You can use `element instanceof ArrayList` to check whether an item
	// is an array or an integer.
	public static int productSum(List<Object> array) 
	{
			return productSum( array, 1 );
	}

	public static int productSum(List<Object> array, int productIncrement ) 
	{
		int numberSum = 0;
		for( Object element : array )
		{
			if( element instanceof List )
			{
				numberSum += productSum( (List)element, productIncrement+1 ) * productIncrement;
			}
			else
			{
				numberSum += ((Integer)element).intValue() * productIncrement;
			}				
		}
		return numberSum;
	}
}
```
- Time Complexity: O(N)
- Space Complexity: O(N) where N is the number of elements in the array list.

## Reverse a sentence keeping the words in the same order
- Ex: *Pavan is Kool* becomes *Kool is Pavan*
- We reverse the entire string and then we reverse the words.
```
public static String reverseWordsInString(String str) 
{
	if( str.length() == 1 )
		return str;

	StringBuffer buff = new StringBuffer();

	// Pavan    Kumar

	for( int inx = str.length()-1; inx >= 0 ; inx-- )
	{
			buff.append(str.charAt(inx));
	}

	int startIndex = -1;
	int endIndex = -1;
	for( int inx = 0; inx < buff.length(); inx++ )
	{
		char ch = buff.charAt(inx);

		if( ch == '\t' || ch == ' ' || inx == buff.length()-1 )
		{
			if( startIndex == -1 )
				continue;

			if( inx == buff.length()-1 )
				endIndex = inx;

			if( endIndex == -1 )
				endIndex = inx-1;

			for( int jnx = startIndex, knx = endIndex ; jnx < knx; ++jnx, --knx )
			{
				char ch1 = buff.charAt(jnx);
				char ch2 = buff.charAt(knx);
				buff.setCharAt( jnx, ch2 );
				buff.setCharAt( knx, ch1 );
			}
			startIndex = -1;
			endIndex = -1;
		}
		else
		{
			if( startIndex == -1 )
				startIndex = inx;
		}
	}

	return buff.toString();
}
```
- Time Complexity: O(N)
- Space Complexity: O(N) where N is the length of the string.

## Given two arrays that represent BSTs obtained by inserting each integer in the array, from left to right, see if their resulting tree is same.
- In this case, we pick the first element and try to identify what all elements go into the left and right subtrees.
- If we recuse this to all the nodes, we will be able to determine if they all represent the same thing.
- This code first catches the case where the two failure conditions do not match.
```
return tree1LST.size() == tree2LST.size() && tree1RST.size() == tree2RST.size()
       && sameBsts( tree1LST, tree2LST) 
       && sameBsts( tree1RST, tree2RST);
```

```
import java.util.*;

class Program {
public static boolean sameBsts(List<Integer> arrayOne, List<Integer> arrayTwo) 
{
	// Check array lenghts
	if( arrayOne.size() != arrayTwo.size() )
			return false;

	if( arrayOne.size() == 0 && arrayTwo.size() == 0 )
			return true;

	if( arrayOne.get(0) != arrayTwo.get(0) )
			return false;

	List<Integer> tree1LST = buildLST( arrayOne );
	List<Integer> tree2LST = buildLST( arrayTwo );
	List<Integer> tree1RST = buildRST( arrayOne );
	List<Integer> tree2RST = buildRST( arrayTwo );

	return tree1LST.size() == tree2LST.size() && tree1RST.size() == tree2RST.size()
					&& sameBsts( tree1LST, tree2LST) 
					&& sameBsts( tree1RST, tree2RST);
  }
	
public static List<Integer> buildLST( List<Integer> content )
{
	List<Integer> treeLST = new ArrayList<Integer>();

	Integer root = content.get(0);

	for( int inx = 1; inx < content.size(); ++inx )
	{
		if( content.get(inx) < root)
			treeLST.add( content.get(inx) );
	}

	return treeLST;
}
	
public static List<Integer> buildRST( List<Integer> content )
{
	List<Integer> treeRST = new ArrayList<Integer>();

	if( content == null || content.size() == 0 )
		return treeRST;

	Integer root = content.get(0);

	for( int inx = 1; inx < content.size(); ++inx )
	{
		if( content.get(inx) >= root)
			treeRST.add( content.get(inx) );
	}

	return treeRST;
}
}
```
- Time Complexity: O(N^2)
- Space Complexity: O(d) where N is the length of the string.

## Searching in a sorted matrix
- You can either start with left most column, bottom row and navigate to the top or vice versa.
- The other two corners would not be optimal because you cant say if the target is in that row looking at them.
```
|1	4	7	12	15	1000|
|2	5	19	31	32	1001|
|3	8	24	33	35	1002|
|40	41	42	44	45	1003|
|99	100	103	106	128	1004|
```
```
import java.util.*;
class Program 
{
   public static int[] searchInSortedMatrix(int[][] matrix, int target) 
   {
	int x = matrix.length - 1;
	int y = 0;

	while( x >= 0 && y <= matrix[0].length - 1 )
	{
		int val = matrix[x][y];
		if( val == target )
			return new int[] { x, y };
		else if( val > target )
			x--;
		else
			y++;
	}
	return new int[] {-1, -1};
    }
}
```
- Time Complexity: O(N+M)
- Space Complexity: O(1).

## Spiral traversal of a matrix
- When there are odd rows or odd columns, there are chances that the same elements covered in for loop 1 / for loop 2 are repeated.
- That is why we take care in for loop 3 / for loop 4.
- Maintain 4 pointers, two for rows and columns each.
```
public static List<Integer> spiralTraverse(int[][] a) 
{			
	int rTop = 0;
	int rBottom = a.length-1;
	int cLeft = 0;
	int cRight = a[0].length-1;

	int m = a.length;
	int n = a[0].length;

	List<Integer> traversal = new ArrayList<Integer>();
	while( rTop <= rBottom && cLeft <= cRight )
	{
		for(int inx = cLeft; inx <= cRight; ++inx )
			traversal.add( a[rTop][inx]);

		for(int inx = rTop+1; inx <= rBottom; ++inx )
			traversal.add( a[inx][cRight]);

		for(int inx = cRight-1; inx >= cLeft; --inx )
		{
			if( rTop == rBottom) break;
			traversal.add( a[rBottom][inx]);	
		}

		for(int inx = rBottom-1; inx >= rTop+1; --inx )
		{
			if( cLeft == cRight ) break;
			traversal.add( a[inx][cLeft]);
		}

		rTop++;
		rBottom--;
		cLeft++;
		cRight--;
	}

	return traversal;
}
```
- Time Complexity: O(M*N)
- Space Complexity: O(M+N).

## Do a zigzag traversal on a two dimensional array
- Basically the path follows like this.
```
Down Traversal	Sum 0 - a[0][0]
Up   Traversal	Sum 1 - a[1][0] a[0][1]
Down Traversal	Sum 2 - a[0][2] a[1][1] a[2][0]
Up   Traversal  Sum 3 - a[3][0] a[2][1] a[1][2] a[0][3]
Down Traversal	Sum 4 - a[1][3] a[2][2] a[3][1] a[4][0]
Up   Traversal  Sum 5 - a[4][1] a[3][2] a[2][3]
Down Traversal	Sum 6 - a[3][3] a[4][2]
Up   Traversal  Sum 7 - a[4][3]
```
- So you maintain a Map from an Integer (sum) to an ArrayList of numbers (array values).
```
public static List<Integer> zigzagTraverse(List<List<Integer>> array) 
{
	int rows = array.size();
	int cols = array.get(0).size();

	Map<Integer, ArrayList<Integer>> map = new HashMap<Integer, ArrayList<Integer>>();
	for( int inx = 0; inx < rows; ++inx )
	{
		for( int jnx = 0; jnx < cols; ++jnx )
		{
			if( !map.containsKey(inx+jnx) )
			{
				ArrayList<Integer> list = new ArrayList<Integer>();
				list.add( array.get(inx).get(jnx));
				map.put( inx+jnx, list );
			}
			else
			{
				ArrayList<Integer> list = map.get(inx+jnx);
				// This check ensures that the direction changes
				if( (inx+jnx)% 2 != 0 )
				{
					list.add(0, array.get(inx).get(jnx));
				}
				else
				{
					list.add(array.get(inx).get(jnx));
				}

				map.put( inx+jnx, list);
			}
		}
	}

	List<Integer> list = new ArrayList<Integer>();

	for (Map.Entry<Integer, ArrayList<Integer>> entry : map.entrySet()) 
	{
	    List<Integer> numbers = entry.getValue();

	    list.addAll(numbers);
	}

	return list;
}
```
- Time Complexity: O(M*N)
- Space Complexity: O(M+N).

## Sunset Views.
- You are given an array of buildings in the form of an array where a[i] determines its height. You are also given a direction - EAST or WEST.
- EAST determines reading array from right and WEST determines reading array from left.
- Edge cases here is if there are two buildings with the same height, we have to pick the one that faces the sun first and not pick the next one.
- Another Edge case here is that it is not just enough to compare the adjacent elements. Reason is if there is a tall building at the beginning of the array, it would block the view for everybody else. So we need to maintain a variable that tracks the last building we considered.
![image](https://user-images.githubusercontent.com/42272776/117722210-69d04b00-b1fe-11eb-8d0c-24c7c82af49e.png)

```
import java.util.*;
class Program 
{
public ArrayList<Integer> sunsetViews(int[] a, String direction) 
{
	// Strictly increasing numbers are the ones that we need to pick.
	ArrayList<Integer> indexes = new ArrayList<Integer>();
	if( a.length == 0 )
		return indexes;

	// The first one is always going to face the sun.
	if( direction.equals("EAST"))
	{
		indexes.add(a.length-1);
		int lastIdentifiedEntry = a[a.length-1];
		for( int inx = a.length-2; inx >= 0; inx-- )
		{
			if( a[inx] > a[inx+1] && a[inx] > lastIdentifiedEntry )
			{
				indexes.add(inx);
				lastIdentifiedEntry = a[inx];
			}
		}
	}
	else
	{
		indexes.add(0);
		int lastIdentifiedEntry = a[0];
		for( int inx = 1; inx < a.length; inx++ )
		{
			if( a[inx] > a[inx-1] && a[inx] > lastIdentifiedEntry )
			{
				indexes.add(inx);
				lastIdentifiedEntry = a[inx];
			}
		}
	}
	Collections.sort( indexes );

	return indexes;
}
}
```
- Time Complexity: O(N)
- Space Complexity: O(N)

## Listing all permutations of a given string

public class Questions 
{
	public static void main(String args[])
	{
		permutationRecurse("abc");
	}
	
	public static void permutationRecurse( String str )
	{
		permutationRecurse("",str);
	}
	
	public static void permutationRecurse( String prefix, String str )
	{
		int n = str.length();
		
		if( n == 0 )
			System.out.println(prefix);
		else
		{
			for(int inx = 0; inx < n; ++inx)
			{
				permutationRecurse( prefix + str.charAt(inx), str.substring(0, inx) + str.substring(inx+1, n));
			}
		}
	}
}
- Time Complexity: O(N* N!)
- Space Complexity: O(N* N!)

## Youngest Common Ancestor
- Iterating the two nodes simultaneously is not a viable solution. This is because if the input nodes are at different levels in the tree, then they ascend differently
and the common will always come up as root node.
- The best option is calculate the difference between the node depths and move the deepest one to be on the same level as the other.
- Then we just increment both of them until they are equal.
- https://www.algoexpert.io/questions/Youngest%20Common%20Ancestor

![image](https://user-images.githubusercontent.com/42272776/119121669-51a4cb00-ba4b-11eb-9207-3d93bff9ccb3.png)

```
import java.util.*;

class Program {
  public static AncestralTree getYoungestCommonAncestor(
      AncestralTree rootAncestor, AncestralTree descendantOne, AncestralTree descendantTwo) 
    {
    	// Get depth
	int depthOne = getDepth( descendantOne );
	int depthTwo = getDepth( descendantTwo );

	// Get delta
	int delta = Math.abs( depthOne - depthTwo );

	// Move the lower one up
	if( depthOne < depthTwo )
	{
		int count = 0;
		while( count < delta )
		{
			descendantTwo = descendantTwo.ancestor;
			count++;
		}
	}
	else
	{
		int count = 0;
		while( count < delta )
		{
			descendantOne = descendantOne.ancestor;
			count++;
		}
	}

	// Increment together
	while( descendantOne != descendantTwo )
	{
		descendantOne = descendantOne.ancestor;
		descendantTwo = descendantTwo.ancestor;
	}
			
    	        return descendantOne;
        }

	public static int getDepth( AncestralTree node )
	{
		if( node == null )
			return 0;

		AncestralTree tmp = node;
		int count = 1;
		while( tmp != null )
		{
			count++;
			tmp = tmp.ancestor;
		}
		return count;
	}
	
  static class AncestralTree {
    public char name;
    public AncestralTree ancestor;

    AncestralTree(char name) {
      this.name = name;
      this.ancestor = null;
    }

    // This method is for testing only.
    void addAsAncestor(AncestralTree[] descendants) {
      for (AncestralTree descendant : descendants) {
        descendant.ancestor = this;
      }
    }
  }
}

```
- Time Complexity: O(D) where D is the Depth of the deepest node among the two.
- Space Complexity: O(1)

## Left view of a Binary Tree
![image](https://user-images.githubusercontent.com/42272776/119236545-a03e8c00-bb55-11eb-9040-d4a01606ceed.png)
- Do a level order traversal but only print the left most node at each level.
- Important things
  - We dont push ```null``` onto the queue if the left or right sub tree of any node is ```null```. This avoids an infinite loop.
  - Because we need to delimit the levels in the tree with a ```null``` in the queue, we need to add a condition to ensure that we do not keep adding ```null``` back to the queue.
  - The following is the condition:
```
if( queue.size() == 0 )
    break;
```
- To get the right view of the tree, we need to first process the right subtree over the left subtree.
```
queue.add( root );
queue.add( null );

leftVisible = true;
leftView.add( root.value );
while( !queue.isEmpty() )
{
    Node node = queue.deQueue();
    
    if( node == null ) // End of the current level
    {
        // This signifies that we are done with the tree processing.
    	if( queue.size() == 0 )
	  break;

    	queue.add( null ); // Beginning of the new level
	leftVisible = true;
    }
    else
    {
    	if( node.lChild != null )
	{
    		queue.add( node.lChild );
		
		if( leftVisible )
		{
			leftView.add( node.value );
			leftVisible = false;
		}
	}
	if( node.rChild != null )
	{
		queue.add( node.rChild );
		
		if( leftVisible )
		{
			leftView.add( node.value );
			leftVisible = false;
		}
	}
    }
}
```
- Time Complexity: O(n)
- Space Complexity: O(n)

## Boat example
![image](https://user-images.githubusercontent.com/42272776/119250649-20e5a280-bbbf-11eb-8e72-3a0097b1d3d7.png)
![image](https://user-images.githubusercontent.com/42272776/119250660-34910900-bbbf-11eb-9bbe-ba15a32d61b1.png)
![image](https://user-images.githubusercontent.com/42272776/119250676-54c0c800-bbbf-11eb-918f-3cf155097071.png)
![image](https://user-images.githubusercontent.com/42272776/119250667-45da1580-bbbf-11eb-96d5-bd41b1f5ffa9.png)
- Example: You came to say, town 8, and you realized that you should have gone to town 15. Then add to a collection, the town values 8, 4, 2, 1. Since you need to go to 15, add its predecessor towns to another array - 15,7,3,1. The first matching between these two arrays from the right, is the town to which you need to come back. In this case, it it town 1. So distance from 8 to town 1 + town 1 to town 15 is what you should be calculating.
- Time Complexity: O(n)
- Space Complexity: O(n)

## Four sum problem
- Solution 1
```
import java.util.*;
// Brute force O(N^4) algorithm
class Program {
public static List<Integer[]> fourNumberSum(int[] a, int targetSum) 
{
	List<Integer[]> list = new ArrayList<Integer[]>();
	for( int inx =0; inx < a.length-3; ++inx )
	{
		for( int jnx =inx+1; jnx < a.length-2; ++jnx )
		{
			for( int knx =jnx+1; knx < a.length-1; ++knx )
			{
				for( int lnx =knx+1; lnx < a.length; ++lnx )
				{
					if( a[inx] + a[jnx] + a[knx] + a[lnx] == targetSum )
					{
	      				        Integer[] array = new Integer[4];
						array[0] = a[inx];
						array[1] = a[jnx];
						array[2] = a[knx];
						array[3] = a[lnx];
						list.add( array );
					}
				}
			}
		}
	}

    return list;
  }
}
```
- Time Complexity: O(n^4)
- Space Complexity: O(1)

- Solution 2
- The binary search that we trigger should start after 
```
import java.util.*;

// O(N^2 logN) solution
class Program {
public static List<Integer[]> fourNumberSum(int[] a, int targetSum) 
{
	Arrays.sort(a);
	List<Integer[]> list = new ArrayList<Integer[]>();
	for( int inx =0; inx < a.length-3; ++inx )
	{
		for( int jnx =inx+1; jnx < a.length-2; ++jnx )
		{
			for( int knx =jnx+1; knx < a.length-1; ++knx )
			{
				 int indexL = Arrays.binarySearch( a, knx+1, a.length, targetSum-a[inx]-a[jnx]-a[knx]);
				 if( indexL >= 0 )
				{
					Integer[] array = new Integer[4];
					array[0] = a[inx];
					array[1] = a[jnx];
					array[2] = a[knx];
					array[3] = a[indexL];
					list.add( array );
				 }
			}
		}
	}
	return list;  
  }
}
```
- Time Complexity: O(n^2 logn + n logn) = O(n^2 logn) + O(nlogn) = O(n^2+n)logn = ~ O(n^2 logn)
- Space Complexity: O(1)

- Solution 3


## Find if a Graph has any cycles in it.

```
import java.util.*;

public class CycleInGraph
{
	public static void main(String args[])
	{
		int edges[][] = { {1, 3}, {2, 3, 4}, {0}, {}, {2, 5}, {}};
		System.out.println(cycleInGraph(edges));
	}
	
	public static boolean cycleInGraph(int[][] edges) 
	{
  		for( int inx = 0; inx < edges.length; ++inx )
		{
			Set<Integer> visitedNodes = new HashSet<Integer>();
			boolean isCyclic = isGraphCyclic( edges, inx, visitedNodes );
			if( isCyclic )
				return true;
		}
	
		return false;
	}
	
	public static boolean isGraphCyclic( int[][] edges, int startingVertex, Set<Integer> visitedNodes )
	{
		if( visitedNodes.contains(startingVertex) )
			return true;

		visitedNodes.add(startingVertex);

		int neighbours[] = edges[startingVertex];
		for( int inx = 0; inx < neighbours.length; ++inx )
		{
			boolean icCyclic = isGraphCyclic( edges, neighbours[inx], visitedNodes );
			if( icCyclic )
				return true;
		}

		visitedNodes.remove(startingVertex);
		return false;
	}	
}
```
- Time Complexity: O(VE) because all the endpoints of the edges i.e., vertices are to be visited.
- Space Complexity: O(V) because we need to store all the vertices.

## Check if the array has a cycle
- Note that this question only asks about cycles that start from index 0.
- So we can do alternate implementations to avoid the extra memory used for SET.
```
import java.util.*;

public class SingleCycleCheck 
{
	public static void main(String args[])
	{
		System.out.println(hasSingleCycle(new int[] { 10, 11, -6, -23, -2, 3, 88, 909, -26 } ));
	}

	public static boolean hasSingleCycle(int[] array) 
	{
		Set<Integer> set = new HashSet<Integer>();

		int inx = 0;
		int counter = 0;
  		while( true )
		{
			if( array[inx] > 0 )
			{
				inx = (inx + array[inx]) % array.length;
			}
			else
			{
				
				inx = ( array.length + inx +  ( array[inx] ) % array.length ) % array.length;
			}

			System.out.println("Processing index " + inx);
			counter++;

			if( set.contains( inx ) )
				break;

			set.add( inx );

			if( set.size() == array.length && counter == array.length )
				return true;
		}
	    return false;
	}
}
```
- Time Complexity: O(N)
- Space Complexity: O(N)

---------------------------------------------------------------------------------------------------------------------------------------
# LeetCode
## Diagnol sum of a matrix
https://leetcode.com/problems/matrix-diagonal-sum/submissions/
```
class Solution {
    public int diagonalSum(int[][] mat) 
    {
        int sum = 0;
        int linx = 0, ljnx = 0;
        int rinx = 0, rjnx = mat.length-1;

        while( linx < mat.length )
        {
            sum += mat[linx][ljnx];

            if( linx != rinx || ljnx != rjnx )
            	sum += mat[rinx][rjnx];

            linx++;
            ljnx++;
            rinx++;
            rjnx--;
        }

        return sum;
    }
}
```
- Time Complexity: O(N)
- Space Complexity: O(N)

## Middle element of a Linked List - If list is even, return the second middle element.
- Key, initialize ptr1 to head.
- Initialize ptr2 to null.
- Increment ptr1, ptr2 and then ptr1.
```
class Solution {
    public ListNode middleNode(ListNode head) 
    {
        // 1 2 3 4 5
        // 1 2 3 4 5 6
        ListNode ptr1 = head;
        ListNode ptr2 = null;
        
        while( ptr1 != null )
        {
            ptr1 = ptr1.next;
            
            if( ptr2 == null )
                ptr2 = head;
            else
                ptr2 = ptr2.next;
            
            if( ptr1 == null )
                return ptr2;

            ptr1 = ptr1.next;
        }
        
        return ptr2.next;
    }
}
```
- Time Complexity: O(N)
- Space Complexity: O(1)

## Univalued Binary Tree - if all the values of all the nodes in the tree are the same.
```
class Solution 
{
    public boolean isUnivalTree(TreeNode root) 
    {
        return isUnivalTree( root, root.val );
    }
    
    public boolean isUnivalTree(TreeNode root, int rootVal )
    {
        if( root == null )
            return true;
        
        return ( root.val == rootVal ) &&
               isUnivalTree( root.left, rootVal ) &&
               isUnivalTree( root.right, rootVal );
    }
}
```
- Time Complexity: O(N)
- Space Complexity: O(N)

## Average of Levels in Binary Tree
- https://leetcode.com/problems/average-of-levels-in-binary-tree/submissions/
```
public static List<Double> averageOfLevels(TreeNode root) 
{
List<TreeNode> queue = new ArrayList<TreeNode>();
List<Integer> levelNodeValues = new ArrayList<Integer>();
List<Double> levelAvgs = new ArrayList<Double>();
queue.add(root);
queue.add(null);

while( queue.size() != 0 )
{
	TreeNode node = queue.get(0);
	queue.remove(0);

	if( node == null )
	{
		double sum = 0;
		for(int inx = 0; inx < levelNodeValues.size(); ++inx)
			sum = sum + levelNodeValues.get(inx);

		levelAvgs.add( sum / levelNodeValues.size());
		levelNodeValues.clear();

		if( queue.size() == 0 )
			break;

		queue.add( null );
	}
	else
	{
		levelNodeValues.add(node.val);

		if( node.left != null )
			queue.add(node.left);

		if( node.right != null )
			queue.add(node.right);
	}
}
return levelAvgs;
}
```

## Delete values from an array
- https://leetcode.com/problems/remove-element/submissions/
```
class Solution {
    public int removeElement(int[] nums, int val) 
    {
        // 1 2 3 4 5 4 5 6 7     
        
        int currMaxIndex = nums.length;
        for(int inx = 0; inx < currMaxIndex;)
        {
            if( nums[inx] == val)
            {
                for( int jnx = inx+1; jnx < currMaxIndex; jnx++ )
                {
                    nums[jnx-1] = nums[jnx];
                }
                
                currMaxIndex--;
            }
            else
            	inx++;
        }
        
        return currMaxIndex;
    }
}
```
- Time Complexity: O(N)
- Space Complexity: O(1)

## Merging array intervals
- https://leetcode.com/problems/merge-intervals/
```
class Solution
{
    public int[][] merge(int[][] intervals) 
    {
        sortIntervals(intervals);
		return mergeOverlappingIntervalsInternal(intervals);    
    }
	
    public void sortIntervals(int[][] intervals) 
    {
            Arrays.sort( intervals, new Comparator<int[]>() {

            @Override
            public int compare(int[] o1, int[] o2) {
                // TODO Auto-generated method stub
                return Integer.compare(o1[0], o2[0]);
            }    		
            });
    }

	public int[][] mergeOverlappingIntervalsInternal(int[][] intervals) 
	{
    	List<int[]> intervalList = new LinkedList<int[]>(Arrays.asList(intervals));
    	for( int inx = 0; inx < intervalList.size() - 1; )
    	{
    		// 1 6			8 10		15 18
    		// 1 3     2 6
    		// 1 6
    		if( intervalList.get(inx)[1] >= intervalList.get(inx+1)[0]) // This means that we can do a merge
    		{    			
    			int[] mergedEntry = new int[2];
    			mergedEntry[0] = intervalList.get(inx)[0];
    			mergedEntry[1] = Math.max(intervalList.get(inx)[1], intervalList.get(inx+1)[1]);
    			intervalList.set(inx, mergedEntry);
    			intervalList.remove(inx+1);
    		}
    		else
    			inx++;
    	}
    	
    	int[][] mergedIntervals = new int[intervalList.size()][];
    	return intervalList.toArray(mergedIntervals);
	}
}
```
- Time Complexity: O(N)
- Space Complexity: O(N)

## Generate powerset of a given number
- Note the similarity in logic for this one and the code for generating Permutations of a number.
```
import java.util.*;
import java.util.stream.Collectors;
import java.util.stream.Stream;

class Program {
  public static List<List<Integer>> powerset(List<Integer> array) 
	{
	    List<List<Integer>> sequences = new ArrayList<List<Integer>>();
			generatePowerSet("",array.stream().map(String::valueOf)
		    .collect(Collectors.joining("")), sequences);
			return sequences;
	}
	
	public static void generatePowerSet( String prefix, String str, List<List<Integer>> sequences )
	{
		add( prefix, sequences );
		int n = str.length();
		for( int inx = 0; inx < n; ++inx )
		{
			generatePowerSet( prefix + str.charAt(inx), str.substring(inx+1), sequences );
		}
	}
	
	private static void add(String prefix, List<List<Integer>> sequences) 
	{
		List<Integer> aSequence = new ArrayList<Integer>();
		for( int inx = 0; inx < prefix.length(); ++inx )
		{
			aSequence.add( prefix.charAt(inx) - '0' );
		}
		sequences.add(aSequence);
	}
}
```

## Rotated Array Binary Search
- https://leetcode.com/problems/rotate-image/
- The key thing is, we can only be sure of the part of the array that is sorted. We cant say for the other half.
- At each iteration, we discard one half of the array.
```
public static int shiftedBinarySearch(int[] a, int target) 
{
	if( a.length == 0 )
		return -1;

	int low = 0;
	int high = a.length - 1;

	while( low <= high )
	{
		int mid = (high + low) /2;

		if( a[mid] == target )
			return mid;
		else
		{
			if( a[low] <= a[mid]) // Left part is sorted.
			{
				if( a[low] <= target && target < a[mid] )
					high = mid-1;
				else
					low = mid+1;
			}
			else	// Right part is sorted.
			{
				if( a[mid] < target && target <= a[high] )
					low = mid+1;
				else
					high = mid-1;
			}
		}
	}
	return -1;
}
```
- Time Complexity: O(logN)
- Space Complexity: O(1)

## Least index and greatest index of an element in a sorted array with repitions. 
- Binary search in an array of repeating elements
- For right most index, low == high represents a case where the trailing elements are the same and is the one that we are looking for.
  - 1 2 3 4 4 4 4 4 4 4 4 4 4 4 4 4
- For left most index, mid = 0, represents a case where the first few elements are the same and are the ones that we are searching for.
  - 1 1 1 1 2 4 5 6 7 8 9 
```
class Solution 
{
    public int[] searchRange(int[] a, int target) 
    {
        return new int[] {binarySearchLeftIndex(a, target), binarySearchRightIndex(a, target)};
    }
    
    public int binarySearchLeftIndex(int[] a, int target)
	{
        int low = 0;
        int high = a.length - 1;
        
        while(low<=high)
        {
        	int mid = (low+high)/2;
        	
            if( a[mid] == target && ( mid == 0 || a[mid-1] != target ))
                return mid;
            else
            {
                if( a[mid] == target && a[mid-1] == target )
                    high = mid - 1;
                else
                {
                    if( a[mid] < target )
                        low = mid+1;
                    else
                        high = mid - 1;
                }
            }
        }
        
        return -1;
    }
    
    public int binarySearchRightIndex(int[] a, int target)
    {
        int low = 0;
        int high = a.length - 1;
        
        
        while(low<=high)
        {
        	int mid = (low+high)/2;
        	
            if( a[mid] == target && ( low == high || a[mid+1] != target ))
                return mid;
            else
            {
                if( a[mid] == target && a[mid+1] == target )
                    low = mid + 1;
                else
                {
                    if( a[mid] < target )
                        low = mid+1;
                    else
                        high = mid - 1;
                }
            }
        }
        
        return -1;
    }
}
```
- Time Complexity: O(logN)
- Space Complexity: O(1)

## Rotate an Array by 90 degrees
- https://leetcode.com/problems/rotate-image/submissions/
### Approach 1:
```
00 01 02
10 11 12
20 21 22 
```
when rotated becomes
```
20 10 00
21 11 01
22 12 02
```
```
for(i=0;i<n;i++)
  for(j=n-1;j>=0;j--)
    std::cout << a[j][i];
```
- Time Complexity: O(N^2)
- Space Complexity: O(N) because if you want to store the content, you cant do it in place using this version of the algorithm.

### Approach 2:
- Rotate diagonally the matrix
- Then rotate columns.
- This approach helps in doing this activity in place.
```
00 01 02
10 11 12
20 21 22
--------
00 10 20
01 11 21
02 12 22
--------
20 10 00
21 11 01
22 12 02
```

```
public class RotateArray90
{
	public static void main(String args[])
	{
		int a[][] = {{1,2,3}, {4,5,6}, {7,8,9}};
		printArray(a);
		rotate(a);
	}

	public static void printArray( int[][] a)
	{
		System.out.println("--------");
		for( int inx = 0; inx < a.length; ++inx )
        {
            for( int jnx = 0; jnx < a.length; ++jnx )
            {
        		System.out.print(a[inx][jnx]);
        		System.out.print(" ");
            }
            System.out.println();
        }
	}
	
    public static void rotate(int[][] arr) 
    {
    	 int n = arr.length;
         
	    // first rotation
	    // with respect to main diagonal
        for(int i=0;i<n;++i)
        {
            for(int j=0;j<i;++j)
            {
                int temp = arr[i][j];
                arr[i][j]=arr[j][i];
                arr[j][i]=temp;
            }
        }
        
        printArray(arr);
        
        // Second rotation
    	// with respect to middle column
        for(int i=0;i<n;++i)
        {
            for(int j=0;j<n/2;++j)
            {
                int temp =arr[i][j];
                arr[i][j] = arr[i][n-j-1];
                arr[i][n-j-1]=temp;
            }
        }
        
        printArray(arr);
    }
}
```
- Time Complexity: O(N^2)
- Space Complexity: O(1) this approach does not need any extra space.

## Find if there are two elements in a Binary Search Tree that add up to a given sum
- Use a SET to enter all the nodes and see if we already have visited k-nodevalue.
```
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode() {}
 *     TreeNode(int val) { this.val = val; }
 *     TreeNode(int val, TreeNode left, TreeNode right) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
class Solution 
{
    public boolean findTarget(TreeNode root, int k)
    {
        Set<Integer> numbers = new HashSet<Integer>();
        return findTarget(root, numbers, k);
    }

    public boolean findTarget(TreeNode root, Set<Integer> numbers, int k)
    {
        if( root == null )
            return false;

        if( numbers.contains(k-root.val) )
            return true;

        numbers.add(root.val);

        return findTarget(root.left, numbers, k) || findTarget(root.right, numbers, k);
    }
}
```
- Time Complexity: O(N)
- Space Complexity: O(N) this approach needs a SET data structure.

## Find the maximum consecutive ones in an array
- https://leetcode.com/problems/max-consecutive-ones/
```
class Solution 
{
    public int findMaxConsecutiveOnes(int[] a) 
    {
        // 1 1 1 1 1 1 0 1 1 0 1 1 1 1 0 0 0
        int maxTillNow = 0;
        int counter = 0;
        for(int inx = 0; inx < a.length; inx++)
        {
            if( a[inx] == 1)
            {
                counter++;
                maxTillNow = Math.max(maxTillNow,counter);
            }
            else
            {                
                counter = 0;
            }
        }
        return maxTillNow;
    }
}
```
- Time Complexity: O(N)
- Space Complexity: O(1)

## Find pivot index in an array. Pivot index is the index in an array where the left and right sums are the same.
- https://leetcode.com/problems/find-pivot-index/
```
class Solution {
    public int pivotIndex(int[] nums) 
    {
        for( int inx = 0; inx < nums.length; ++inx )
        {
            // Get left sum, Get right sum
            int leftSum = 0;
            for( int jnx = inx-1; jnx >=0 ; --jnx )
            {
                leftSum = leftSum + nums[jnx];
            }

            int rightSum = 0;
            for( int knx = inx+1; knx<nums.length; ++knx )
            {
                rightSum = rightSum + nums[knx];
            }
            
            if(leftSum == rightSum)
                return inx;
        }
        
        return -1;
    }
}
```
- Time Complexity: O(N)
- Space Complexity: O(1)

## Missing number in an array
- https://leetcode.com/problems/missing-number/
```
class Solution {
    public int missingNumber(int[] nums) 
    {
        int n = nums.length;
        
        int expectedSum = n * ( n+1) / 2;
        
        int observedSum = 0;
        for(int inx=0; inx<nums.length;inx++)
            observedSum += nums[inx];
        
        return expectedSum - observedSum;
    }
}
```
- Time Complexity: O(N)
- Space Complexity: O(1)

## How to generate a transpose of a given matrix
- https://leetcode.com/problems/transpose-matrix/
```
class Solution {
    public int[][] transpose(int[][] matrix) 
    {
        int newMatrix[][] = new int[matrix[0].length][matrix.length];
        
        for(int row=0; row<matrix.length; ++row)
            for(int col=0; col<matrix[0].length; ++col)
            {
                newMatrix[col][row] = matrix[row][col];
            }
        
        return newMatrix;
    }
}
```
- Time Complexity: O(NM)
- Space Complexity: O(NM)

## Flipping an image horizontally and then inverting it. 
- https://leetcode.com/problems/flipping-an-image
```
class Solution {
    public int[][] flipAndInvertImage(int[][] image) 
    {
        for( int inx = 0 ; inx < image.length; ++inx )
            for( int jnx = 0 ; jnx < image.length/2; ++jnx )
        {
            int temp = image[inx][jnx];
            image[inx][jnx] = image[inx][image.length-1-jnx];
            image[inx][image.length-1-jnx] = temp;
        }
        
        for( int inx = 0 ; inx < image.length; ++inx )
            for( int jnx = 0 ; jnx < image.length; ++jnx )
        {
            image[inx][jnx] = (image[inx][jnx] == 0 ? 1 : 0);            
        }
        
        return image;
    }
}
```
- Time Complexity: O(N^2)
- Space Complexity: O(1)

## Next element greater than the current one.
- https://leetcode.com/problems/next-greater-element-i/
```
class Solution {
    public int[] nextGreaterElement(int[] nums1, int[] nums2) 
    {
        int elements[] = new int[nums1.length];
        int counter = 0;
        for(int inx=0; inx<nums1.length;++inx)
        {
            boolean foundElement = false;
            for(int jnx=0; jnx<nums2.length;++jnx)
            {
                if( !foundElement )
                {
                    if( nums2[jnx] == nums1[inx] )
                    {
                        foundElement = true;
                        
                        // If the element is at the right most end, then we don't have any more elements to the right.
                        if( jnx == nums2.length - 1 )
                        {
                        	elements[counter] = -1;
                        	counter++;
                        	break;
                        }
                    }
                }
                else
                {
                    if( nums2[jnx] > nums1[inx] )
                    {
                        elements[counter] = nums2[jnx];
                        counter++;
                        break;
                    }

                    // Once again, if the element is last index, it means no element greater than the current element was found.
                    if( jnx == nums2.length - 1 )
                    {
                        elements[counter] = -1;
                        counter++;
                        break;
                    }
                }
            }
        }
        return elements;
    }
}
```
- Time Complexity: O(1)
- Space Complexity: O(1)

## https://leetcode.com/problems/count-negative-numbers-in-a-sorted-matrix
- Start at the last row last column element and move up carefully.
```
class Solution 
{
    public int countNegatives(int[][] grid) 
    {
        int m = grid.length;
        int n = grid[0].length;
        
        int specimen = -0;
        
        int row = m-1;
        int col = n-1;
        int count = 0;
        
        while( row >= 0 )
        {
            specimen = grid[row][col];

            if( specimen >= 0 )
                row--;
            else
            {
                for( int jnx=col; jnx >=0; jnx--)
                {
                    if(grid[row][jnx] < 0)
                        count++;
                    else
                    {
                        break;
                    }
                }
                
                row--;
            }            
        }

        return count;
    }
}
```
- Time Complexity: O(M+N)
- Space Complexity: O(1)

## Convert sorted array to Binary Search Tree
- https://leetcode.com/problems/convert-sorted-array-to-binary-search-tree
```
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode() {}
 *     TreeNode(int val) { this.val = val; }
 *     TreeNode(int val, TreeNode left, TreeNode right) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
class Solution 
{
    public TreeNode sortedArrayToBST(int[] nums) 
    {
        return recurseTreeBuild( nums, 0, nums.length-1 );
    }
    
    TreeNode recurseTreeBuild( int[] nums, int low, int high )
    {
        if( low > high )
            return null;

        int mid = (low + high)/2;
        TreeNode root = new TreeNode( nums[mid] );
    
        root.left = recurseTreeBuild( nums, low, mid-1 );
        root.right = recurseTreeBuild( nums, mid+1, high );
    
        return root;
    }
}
```
- Time Complexity: O(N)
- Space Complexity: O(N)

## Array of elements of size 'n' whose sum is 0.
```
class Solution 
{
    public int[] sumZero(int n) 
    {
        int numbers[] = new int[n];
        if( n == 1 )
            return new int[] { 0 };
        else
        {
            boolean odd = ( n%2 != 0 );
            
            // n = 7
            // n = 8
            for(int inx = 0; inx < n/2; ++inx)
            {
                numbers[inx] = inx+1;
                numbers[n-1-inx] = -1 * (inx+1);
            }
            
            if(odd)
                numbers[n/2] = 0;
        }

        return numbers;        
    }
}
```
- Time Complexity: O(1)
- Space Complexity: O(1)

## Median Algorithms
- Median of a sorted array is the mid element in the array
  - If the size is odd, it is the mid element
  - If the size is even, it is the average of the two mid elements.
    - Time Complexity: O(N)
    - Space Complexity: O(1)
- Median of two sorted arrays
  - Approach 1: Merge both of them into a single array and then find the median.
    - Time Complexity: O(M+N)
    - Space Complexity: O(M+N)
  - Approach 2:
- Median of an unsorted array
  - Sort the array and look up median
    - Time Complexity: O(NlogN)
    - Space Complexity: O(1)


## Combining two tables using SQL
- https://leetcode.com/problems/combine-two-tables/
```
select distinct pers.firstname, pers.lastname, address.city, address.state  
from Person pers
left join Address address on address.personid = pers.personid;
```

## Designing a hashmap ( simple )
- https://leetcode.com/problems/design-hashmap/
```
class MyHashMap {

    int bucket[];
    int size;
    /** Initialize your data structure here. */
    public MyHashMap() {
        size = 1000000;
        bucket = new int[size];
        
        for( int inx = 0 ; inx < size; ++inx )
            bucket[inx] = -1;
    }
    
    /** value will always be non-negative. */
    public void put(int key, int value) {
        bucket[key%size] = value;
    }
    
    /** Returns the value to which the specified key is mapped, or -1 if this map contains no mapping for the key */
    public int get(int key) {
        return bucket[key%size];
    }
    
    /** Removes the mapping of the specified value key if this map contains a mapping for the key */
    public void remove(int key) {
        bucket[key%size] = -1;
    }
}
```
- Time Complexity: O(1)
- Space Complexity: O(1)

## Designing a Hashset ( simple )
- https://leetcode.com/problems/design-hashset
```
class MyHashSet {

    int bucket[];
    int size;

    /** Initialize your data structure here. */
    public MyHashSet() {
        size = 1000000;
        bucket = new int[size];
        
        for( int inx = 0 ; inx < size; ++inx )
            bucket[inx] = -1;
    }
    
    public void add(int key) {
        bucket[key%size] = key;
    }
    
    public void remove(int key) {
        bucket[key%size] = -1;
    }
    
    /** Returns true if this set contains the specified element */
    public boolean contains(int key) {
        return bucket[key%size] != -1;
    }
}
```
- Time Complexity: O(1)
- Space Complexity: O(1)

## Sum of unique elements in the array 
- https://leetcode.com/problems/sum-of-unique-elements
```
class Solution {
    public int sumOfUnique(int[] nums) 
    {
        Map<Integer, Integer> numbers = new HashMap<Integer, Integer>();
        for(int inx = 0 ;inx < nums.length; ++inx)
        {
            if( numbers.containsKey( nums[inx]) )
                numbers.put(nums[inx], 0);
            else
                numbers.put(nums[inx], nums[inx]);
        }
        
        int sum = 0;
        for(Map.Entry<Integer, Integer> entry : numbers.entrySet())
        {
            sum = sum + entry.getValue();
        }        
        
        return sum;
    }
}
```
- Time Complexity: O(N)
- Space Complexity: O(N)

## Calculate Tilt of a Binary Tree
- https://leetcode.com/problems/binary-tree-tilt/
- The important thing in this problem is that the summation should include all the children too.
```
class Solution {
    int sum = 0;
    public int findTilt(TreeNode root) 
    {
        findTiltInternal( root );
        
        return sum;
    }
    
    public int findTiltInternal(TreeNode root) 
    {
        if( root == null )
        {
            return 0;
        }

        int leftTilt = findTiltInternal( root.left );
        int rightTilt = findTiltInternal( root.right );
        sum = sum + Math.abs( leftTilt - rightTilt );
        
        return root.val + leftTilt + rightTilt;
    }
}
```
- Time Complexity: O(N)
- Space Complexity: O(N)

## Tribonacci Number
```
class Solution
{
    public int tribonacci(int n) 
    {
        int f0 = 0;
        int f1 = 1;
        int f2 = 1;

        switch(n)
        {
            case 0: return f0;
            case 1: return f1;
            case 2: return f2;
            default:

            int currentNumber = 2;

            int fn = 0;
            while( currentNumber < n )
            {
                fn = f0 + f1 + f2;
                currentNumber++;

                f0 = f1;
                f1 = f2;
                f2 = fn;
            }

            return fn;
        }
    }
}
```
- Time Complexity: O(N)
- Space Complexity: O(1)

## Generate Parenthesis
- https://leetcode.com/problems/generate-parentheses/

## SQL - Group Count
- https://leetcode.com/problems/duplicate-emails
```
select p.Email
from Person p
group by p.Email
having count(p.Email) > 1;
```

## SQL - Inner Query
https://leetcode.com/problems/customers-who-never-order
```
select customers.name as Customers
from Customers customers
where customers.id not in ( select distinct orders.customerid
from Orders orders );
```

## Mitochondria

## TODO
## https://leetcode.com/problems/sort-the-matrix-diagonally/
## https://leetcode.com/problems/maximum-product-subarray/

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
```
import java.util.ArrayList;

public class Stack 
{
	public static void main(String args[])
	{
		ArrayList<Integer> stack = new ArrayList<Integer>();
		stack.add(1);
		stack.add(-1);
		stack.add(12);
		stack.add(81);
		stack.add(19);
		stack.add(23);
		stack.add(58); // Top
		
		printStack(stack);
		sortStack(stack);
		printStack(stack);
		
	}

	private static void printStack(ArrayList<Integer> stack) 
	{
		for(int inx = stack.size()-1; inx >= 0; --inx)
		{
			System.out.print(stack.get(inx) + " ");			 
		}
		System.out.println();
	}

	public static void sortStack(ArrayList<Integer> stack)
	{
		if( stack.size() == 0 )
			return;
		
		// Pop the element
		int element = stack.get( stack.size()-1 );
		stack.remove(stack.size()-1);
		sortStack( stack );
		
		// Push the element, but now in sorted order
		sortPush( stack, element);		
	}

	private static void sortPush(ArrayList<Integer> stack, int element)
	{
		if( stack.size() == 0 )
			stack.add(element);
		else
		{
			int topOfStack = stack.get(stack.size()-1);
			if( topOfStack <= element )
			{
				stack.add(element);
			}
			else
			{
				// Pop the top of the element
				stack.remove(stack.size()-1);
				sortPush( stack, element);
				stack.add(topOfStack);
			}
		}		
	}
}
```
- Time Complexity: O(N^2)
- Space Complexity: O(N)

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

# Graphs ( Scaler Academy )
- Made up of vertices and edge.
- Example is the network of users connected directly or indirectly in LinkedIn.
- May or may not have cycles or some nodes may even not be connected.
- Directed ( LinkedIn Follow functionality ) or Undirected Graph ( LinkedIn friend connections between two users ).

## How are Graphs stored
- Adjacency Matrix: If there are V profiles in LinkedIn, then V^2 is the size.
- Time Complexity - O(V^2)
- Space Complexity - O(V^2) 
- Adjacency List: Adjacency Matrices usually has lots of 0s in it. Ex: even in LinkedIn. Number of users is around 10M but typicallly a user will have only 500-1000 max connections. This makes the Adjacency Matrix, a sparse matrix.
- A -> 

# Dynamic Programming
- When dealing with certain problems, there will be overlapping sub propblems that are to be solved to realize the larger problem.
- Best example is fibonacci series calculation.
- To realize f(n), we keep calculating f(n-1) and f(n-2) and this results in several f(3) or f(4) for larger values of 'n'.
![image](https://user-images.githubusercontent.com/42272776/118016952-a5d8ec80-b373-11eb-93d2-468565961b5e.png)
- Dynamic programming is a way of solving problems that have these overalapping sub problems.
- Instead of calculating them again and again, we keep a memory and store the results there. This brings the complexity of a lot of algorithms from 2^n to just n^2 etc.
- There are two variants of Dynamic problem and in general the bottom up variant performs better as it does not re-calcuate the smaller sub problems again[?].
## Example
- The normal recursive function for fibonacci series taking long time to evaluate for larger values of n. E.g fib(50)
- Recursive Representation
```
void fib(int n)
{
    if( n <= 2 ) return 1;
    return fib( n-1 ) + fib( n-2 );
}
```
Time Complexity: O(2^n). Actually O(2^1.6) as the left tree is typically larger than the right tree.
Space Complexity: O(n)

## Coin-row problem
![image](https://user-images.githubusercontent.com/42272776/118527296-c5e72200-b75e-11eb-8820-94d62db0287b.png)
- There are several coins lined up and we need to pick the set that gives maximum sum with the condition that no two adjacent coins can be selected.
- F(n) = Max( Cn + F(n-2), F(n-1) for n>1
- F(0) = 0
- F(1) = C1.
- Code
```
F[0] = 0;
F[1] = C1;
for( int i = 2; i <= n; i++ )
    F[i] = Math.max( Ci + F(i-2), F(i-1) );
return F[n]
```
- Note that the size of the array in the above implementation is N+1.
![image](https://user-images.githubusercontent.com/42272776/118527233-b5cf4280-b75e-11eb-9b0d-9d37c4932783.png)
```
import java.util.*;

class Program {
	public static int maxSubsetSumNoAdjacent(int[] array) 
	{
		 if( array.length == 0)
			 return 0;

		 // Let F(n) be the function that returns the maximum subset sum till index n-1.
		 // Then F(0) = 0
		 // F(1) = array[0]
		 // F(n) = max( array[n-1] + F(n-2), F(n-1) )
		 int memory[] = new int[array.length+1];
		 memory[0] = 0;
		 memory[1] = array[0];

		 for( int inx = 2; inx <= array.length; ++inx )
		 {
		 	memory[inx] = Math.max( array[inx-1] + memory[inx-2], memory[inx-1] );
		 }
		 return memory[array.length];
	}
}
```
- Time Complexity: O(n)
- Space Complexity: O(n)

## Change making problem
- You have unlimited number of coins of certain denomination and you need to identify the minimum number of coins that make up
a given sum.
![image](https://user-images.githubusercontent.com/42272776/118539012-87f0fa80-b76c-11eb-98ae-e16eb39434f5.png)
- Note that the size of the array in the above implementation is N+1.
![image](https://user-images.githubusercontent.com/42272776/118539191-bf5fa700-b76c-11eb-85d7-94c2badb8a33.png)

- Time Complexity: O(nm)
- Space Complexity: O(n)

# Still to go
Searching
Hashing
String problems
Queues


# Mistakes to avoid
- Avoid multiple paths in which a variable is incremented or decremented ( inx++ ). This leads to unpredictable results for edge cases.
- More stress on edge cases while writing program.
- In most cases, identifying the largest in a scenario, can be done with out any extra pass by hacking a simple variable that maintains the highest value.
- For array problems, if you do not have any solution or optimal solution, try sorting the array and see if there is any lead.
  - You can use two pointer approach for sorted arrays.
  - In two pointer approach, always ensure that you are adjusting pointers in all cases, example, Three Sum Problem, when there is a match.
  - In few cases, it may be sensible to start the two pointers from the different ends instead of from the same end.
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
- Java Interview Questions https://www.interviewbit.com/java-interview-questions/
- Dynamic Programming https://www.youtube.com/watch?v=oBt53YbR9Kk



