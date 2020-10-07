# Binary Search
  * Binary Search is divide and conquer algorithm.
  * Search a sorted array by repeatedly dividing the search interval in half.
  * Begin with an interval covering the whole array.
  * If the value of the search key is less than the item in the middle of the interval, narrow the interval to the lower half. 
  * Otherwise narrow it to the upper half. Repeatedly check until the value is found or the interval is empty.


* Recursive Approach :
  * Time Complexity : O(NLogN)
  * Space Complexity : O(LogN)

```cpp

#include<bits/stdc++.h>
using namespace std;
bool binarysearch(int arr[], int l, int r, int val){
	if(l <= r){
		
		int mid = l + (r-l)/2;
		
		if(arr[mid] == val)
		return true;
		
		if(arr[mid] > val)
		return binarysearch(arr, l, mid-1, val);
		else
		return binarysearch(arr, mid+1, r, val);
	}
	return false;
}
int main(){
	int arr[] = {41, 58, 68, 75, 84, 87, 99};
	int n = sizeof(arr) / sizeof(arr[0]);
	cout << (binarysearch(arr, 0, n-1, 51) == true ? "51 is Present" : "51 is Not Present") << endl;
	cout << (binarysearch(arr, 0, n-1, 58) == true ? "58 is Present" : "58 is Not Present") << endl;
	return 0;
}

```

* Iterative Approach :
   * Time Complexity : O(NLogN)
   * Space Complexity : O(1)

```cpp

#include<bits/stdc++.h>
using namespace std;
bool binarysearch(int arr[], int l, int r, int val){
	while(l < r){
		
		int mid = l + (r-l) / 2;
		
		if(arr[mid] == val)
		return true;
		
		if(arr[mid] > val)
			r = mid - 1;
		else
		    l = mid + 1;
	}
	return false;
}

int main(){
	int arr[] = {41, 58, 68, 75, 84, 87, 99};
	int n = sizeof(arr) / sizeof(arr[0]);
	cout << (binarysearch(arr, 0, n-1, 51) == true ? "51 is Present" : "51 is Not Present") << endl;
	cout << (binarysearch(arr, 0, n-1, 58) == true ? "58 is Present" : "58 is Not Present") << endl;
	return 0;
}


```
