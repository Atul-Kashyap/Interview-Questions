# 1. [Quick Sort](https://www.geeksforgeeks.org/quick-sort/)
  * **QuickSort** is a Divide and Conquer algorithm.
  
  * It picks an element as pivot and partitions the given array around the picked pivot.
  
  * Time Complexity : 
    * Worst Case : O(N^2)
      * The worst case occurs when the partition process always picks greatest or smallest element as pivot. 
      
      * If we consider above partition strategy where last element is always picked as pivot, the worst case 
        would occur when the array is already sorted in increasing or decreasing order. Following is recurrence for worst case.
    * Best Case: 0(NLogN)
      * The best case occurs when the partition process always picks the middle element as pivot.
  * Is QuickSort stable? 
  
    The default implementation is not stable. However any sorting algorithm can be made stable by considering indexes as comparison parameter.
  * Is QuickSort In-place?
  
    As per the broad definition of in-place algorithm it qualifies as an in-place sorting algorithm as it uses extra space only for storing 
    recursive function calls but not for manipulating the input.
    
  * Quick Sort is also a cache friendly sorting algorithm as it has good locality of reference when used for arrays.
  
  * Why Quick Sort is preferred over MergeSort for sorting Arrays?
  
    Quick Sort in its general form is an in-place sort (i.e. it doesn’t require any extra storage) whereas merge sort requires O(N) extra storage,
    N denoting the array size which may be quite expensive. Allocating and de-allocating the extra space used for merge sort increases the running 
    time of the algorithm. Comparing average complexity we find that both type of sorts have O(NlogN) average complexity but the constants differ. 
    For arrays, merge sort loses due to the use of extra O(N) storage space.
    
  * Most practical implementations of Quick Sort use randomized version. The randomized version has expected time complexity of O(nLogn). The worst 
    case is possible in randomized version also, but worst case doesn’t occur for a particular pattern (like sorted array) and randomized Quick Sort 
    works well in practice.
    
  * Why MergeSort is preferred over QuickSort for Linked Lists?
    In case of linked lists the case is different mainly due to difference in memory allocation of arrays and linked lists. Unlike arrays, linked list
    nodes may not be adjacent in memory. Unlike array, in linked list, we can insert items in the middle in O(1) extra space and O(1) time. Therefore 
    merge operation of merge sort can be implemented without extra space for linked lists.
    
    
  
  
  * Code : 
  
  ```cpp
  
#include<bits/stdc++.h>
using namespace std;

void swap(int *a, int *b){
	int t = *a;
	*a = *b;
	*b = t;
}

int partition(int arr[], int l, int r){
	int i = l-1;
	int pivot_val = arr[r];
	for(int j = l; j < r; ++j){
		if(arr[j] < pivot_val){
			i++;
			swap(arr[i], arr[j]);
		}
	}
	swap(arr[i+1], arr[r]);
	return i+1;	
}
void quicksort(int arr[], int low, int high){
	if(low < high){
		int pivot = partition(arr, low, high);
		quicksort( arr, low, pivot-1);
		quicksort( arr, pivot+1, high);
	}
}

void print(int arr[], int n){
	for(int i = 0; i < n; ++i){
		cout << arr[i] << " ";
	}
	cout << endl;
}

int main(){
	int arr[] = {5, 6, 8, 1, 2, 4, 7, 9, 6};
	int n = sizeof(arr) / sizeof(arr[0]);
	quicksort(arr, 0, n-1);
	print(arr, n);
	return 0;
}

```


# 2. [Merge Sort](https://www.geeksforgeeks.org/merge-sort/)

  * **Merge Sort** is a Divide and Conquer algorithm. 
     
  * It divides input array in two halves, calls itself for the two halves and then merges the two sorted halves.
     
  * The merge() function is used for merging two halves. 
     
  * The merge(arr, l, m, r) is key process that assumes that arr[l..m] and arr[m+1..r] are sorted and merges the two sorted sub-arrays into one.
  
  * Time Complexity : O(NLogN)
  
  * Auxiliary Space : O(N)
  
  * Algorithmic Paradigm: Divide and Conquer

  * Sorting In Place: No in a typical implementation

  * Stable: Yes
  
  ```cpp
  
  #include<bits/stdc++.h>
using namespace std;

void merge(int arr[], int l, int m, int r){
	int n1 = m - l + 1;
	int n2 = r - m;
	int left[n1];
	int right[n2];
	for(int i = 0; i < n1; ++i)
	left[i] = arr[l+i];
	for(int i = 0; i < n2; ++i)
	right[i] = arr[m+1+i];
	
	int i = 0, j = 0, k = l;
	while(i < n1 || j < n2){
		if(i < n1 && j < n2){
		 arr[k++] = left[i] < right[j] ? left[i++] : right[j++];
		}
		else
		arr[k++] = i < n1 ? left[i++] : right[j++];
	}

}

void mergesort(int arr[], int low, int high){
	if(low < high){
		int mid = (low + high) / 2;
		mergesort(arr, low, mid);
		mergesort(arr, mid+1, high);
		merge(arr, low, mid, high);
	}
	
}

void print(int arr[], int n){
	for(int i = 0; i < n; ++i)
	cout << arr[i] << " ";
	cout << endl;
}

int main(){
	int arr[] = {5, 6, 2, 8, 9, 3, 2, 1};
	int n = sizeof(arr) / sizeof(arr[0]);
	mergesort(arr, 0, n-1);
	print(arr, n);
	
	return 0;
}

```


# 3. [Heap Sort](https://www.geeksforgeeks.org/heap-sort/)

  * **Heap sort** is a comparison based sorting technique based on Binary Heap data structure. 
  
  * It is similar to selection sort where we first find the maximum element and place the maximum element at the end.
  
  * We repeat the same process for the remaining elements.  
  
  * A **complete binary** tree is a binary tree in which every level, except possibly the last, is completely filled, and all nodes are as far left as possible.
  
  * A **Binary Heap** is a Complete Binary Tree where items are stored in a special order such that value in a parent node is greater(or smaller) than the values
    in its two children nodes. 
    
  * The former is called as **max heap** and the latter is called **min-heap**. The heap can be represented by a binary tree or array.
  
  * Since a Binary Heap is a Complete Binary Tree, it can be easily represented as an array and the array-based representation is space-efficient. 
  
  * If the parent node is stored at index I, the **left child can be calculated by 2 * I + 1 and right child by 2 * I + 2** (assuming the indexing starts at 0).
  
  * Heapify procedure can be applied to a node only if its children nodes are heapified. So the **heapification must be performed in the bottom-up order**.
  




