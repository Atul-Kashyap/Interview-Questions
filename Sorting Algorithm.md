# 1. [Quick Sorting](https://www.geeksforgeeks.org/quick-sort/)
  * QuickSort is a Divide and Conquer algorithm.
  
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


int main(){
	int arr[] = {5, 6, 2, 3, 1, 9, 7, 8};
	int n = sizeof(arr)/sizeof(arr[0]);
	quicksort(arr, 0, n-1);
	Print(arr, n);
    return 0;
}

```


