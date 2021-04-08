---
title: Interpolation Search
slug: /searching-algorithms/interpolation-search
---

## Introduction

Interpolation Search is a technique to search a key in an array consisting of sorted and uniformly distributed values. By Uniformly distributed we mean, the difference between two adjacent elements must be consistent. For example:

**Sorted but non-uniformly distributed array:**

The following array is sorted but not uniform distributed as the difference between adjacent elements is not the same.

| 1   | 5   | 8   | 9   | 12  |
| --- | --- | --- | --- | --- |

**Sorted and uniformly distributed array:**

The following array is sorted and uniformly distributed as the difference between adjacent items is the same.

| 1   | 2   | 3   | 4   | 5   |
| --- | --- | --- | --- | --- |

## Why Interpolation Search ?

The interpolation search is an improvement over Binary Search where the values in a sorted array are uniformly distributed. In Binary Search, we always check the middle element to find the desired key. Unlike binary search, interpolation searches are performed at various locations depending on the value of the key being searched. For example, if the value of the key is closer to the last item, the interpolation search may start near the end.

The position to be searched is determined using the _probe position_ formula.

```
pos = low + [ (x - arr[low]) * (high - low) / (arr[high] - arr[low])]

arr[] -> Array where elements need to be searched
x     -> Element to be searched
lo    -> Starting index in arr[]
hi    -> Ending index in arr[]
```

## Algorithm

- Step 1: Calculate the value of "pos" using the probe position formula.
- Step 2: If it is a match, return the index of the item, and exit.
- Step 3: If the item is less than arr[pos], calculate the probe position of the left sub-array. Otherwise, calculate the same in the right sub-array.
- Step 4: Repeat Step 1 to Step 3 until a match is found or the size of the sub-array reduces to zero.

## Code

### C++

```cpp
//INTERPOLATION SEARCH
#include<bits/stdc++.h> //Importing library (This is the special type of library which will include all basic libraries)

using namespace std;

// If the searching element is present it will return its index, else it will return -1.

int interpolationSearch(int arr[], int n, int x) {
  int low = 0, high = (n - 1); //Assigning lower index as 0 and higher index as n-1

  while (low <= high && x >= arr[low] && x <= arr[high]) {
    if (low == high) {
      if (arr[low] == x) return low;
      return -1;
    }
    // Probing the position with keeping uniform distribution in mind.
    int pos = low + (((double)(high - low) /
      (arr[high] - arr[low])) * (x - arr[low]));

    // Condition of element to be found
    if (arr[pos] == x)
      return pos;

    // If x is larger, x is in upper part
    if (arr[pos] < x)
      low = pos + 1;

    // If x is smaller, x is in the lower part
    else
      high = pos - 1;
  }
  return -1;
}

int main() //Starting our main function
{

  int num, x, loc;
  std::cout << "Enter size of an array: ";
  std::cin >> num;
  int arr[num]; //Creating array of the size num
  std::cout << "Enter elements: " << std::endl;

  for (int i = 0; i < num; i++) //Enter the elements in the array
  {
    std::cin >> arr[i];
  }

  //Sorting our array

  int n = sizeof(arr) / sizeof(arr[0]);
  sort(arr, arr + n);

  cout << "\nArray after sorting using "
  "default sort is : \n" << std::endl;
  for (int i = 0; i < n; ++i) {
    cout << arr[i] << " ";

  }
  cout << std::endl;

  //Entering the searching element
  std::cout << "Enter element to be searched: " << std::endl;
  cin >> x; //Element to be searched
  int index = interpolationSearch(arr, n, x);
  //If element was found
  if (index != -1)
    cout << "Element found at index " << index; //Returning the index pf the element
  else
    cout << "Element not found."; //Returning -1 as element has not found

  return 0;
}
```

#### Sample Input:

```
5
1
7
4
9
2
4
```

#### SAMPLE OUTPUT:

Enter size of an array:  
Enter elements:  
Array after sorting using default sort is :  
1 2 4 7 9  
Enter element to be searched:  
4  
Element found at index 2

### Python

```python
# INTERPOLATION SEARCH

# If the searching element is present in array,
# then it returns index of it, else returns -1


def interpolationSearch(arr, size, search_element):
    # Assigning indexes
    low = 0
    high = size - 1
    # As array is going to be sorted
    # an element present in array must be in range defined by corner
    while low <= high and search_element >=
    arr[low] and search_element <= arr[high]:
        if low == high:
            if arr[low] == search_element:
                return low
            return -1

        position = low + int(float(high - low) /
        (arr[high] - arr[low])*(search_element - arr[low]))

        # Condition of element found

        if arr[position] == search_element:
            return position

        # If x is larger, x is in upper part

        if arr[position] < search_element:
            low = position + 1
        else:
            # If x is smaller, x is in lower part
            high = position - 1

    return -1


# Starting with the main code
# Creating array of the size n
# Size would be taken into the variable n from user
def main():
    arr = []
    size = int(input('Enter the size of array : '))

    # Entering the elements in the array

    print ('Enter elements :')
    for index in range(0, size):
        ele = int(input())
        arr.append(ele)
    print ('The elements entered are:\n', arr, '\n')

    # Sorting our array

    print ('The sorted array is: ')
    arr.sort()
    print (arr, '\n')

    # Entering the searching element

    search_element = int(input('Enter the element to be searched: '))

    index = interpolationSearch(arr, size, search_element)

    # If element was found

    if index != -1:
        # Returning the index of the element
        print ('Element found at index', index)
    else:
        # Returning -1 as element has not found
        print ('Element not found')
main()
```

#### Sample Input:

```
5
1
5
7
2
9
7
```

#### Sample Output:

Enter the size of array :  
Enter elements :  
The elements entered are: [1, 5, 7, 2, 9]  
The sorted array is: [1, 2, 5, 7, 9]  
Enter the element to be searched:  
Element found at index 3

## Complexity Analysis

n : number of the elements in the array

### Time Complexity:

- **Best Case**: O (1)
- **Average Case**: O (log log n)
- **Worst Case**: O (N)

### Space Complexity: O (1)

**_Credits _**: _[Sharvari Raut](https://github.com/sharur7)_