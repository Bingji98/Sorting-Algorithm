# Sorting-Algorithm
![image](https://user-images.githubusercontent.com/61017530/208302854-deaa4802-2ef5-4881-a5de-dbb81edaf194.png)

# Table of Contents
1. [Bubble Sort](#bs)
2. [Selection Sort](#ss)
3. [Insertion Sort](#is)
4. [Quick Sort](#qs)

# Bubble sort <a name="bs"></a>
The basic idea of bubble sorting is that it repeatedly swaps adjacent elements if they are not in the desired order. **As a result, after the N<sup>th</sup> round, the N<sup>th</sup> largest number will be switched to the N<sup>th</sup> place.**

If a given array of elements has to be sorted in ascending order, bubble sorting will start by comparing the first element of the array with the second element and immediately swap them if it turns out to be greater than the second element, and then move on to compare the second and third element, and so on. Below is an example:
![image](https://www.crio.do/blog/content/images/size/w1000/2022/01/Bubble-sort-algorithm-example-1.png)

Implementation in Python:
```python
def bubble_sort(arr):
    arr_len = len(arr)
    finished = True
    for i in range(arr_len-1):
        for j in range(arr_len-i-1):
            if arr[j] > arr[j+1]:  # move the larger element backwards
                finished = False
                arr[j], arr[j+1] = arr[j+1], arr[j]
        if finished: # if all elements in arr[:arr_len-i] are in order, then stop and return
            return
    return

arr = [24, 37, 25, 7, 99, 11, 90]
bubble_sort(arr)
print(arr)
```
>[7, 11, 24, 25, 37, 90, 99]

Time Complexity:
- Worst Case: O(n<sup>2</sup>) 
- Average Case: O(n<sup>2</sup>) 
- Best case: O(n)

Auxiliary Space Complexity:
- O(1)

Stability:
- Stable

# Selection sort <a name="ss"></a>
Selection sort is a sorting algorithm in which the given array is divided into two subarrays, the sorted left section, and the unsorted right section. Initially, the sorted portion is empty and the unsorted part is the entire list. **In each iteration, we fetch the minimum element from the unsorted list and push it to the end of the sorted list thus building our sorted array.** This operation can also be in-place. Below is an example:
![image](https://www.crio.do/blog/content/images/size/w1000/2022/01/Selection-sort-algorithm-example-1.png)

Implementation in Python:
```python
def selection_sort(arr):
    arr_len = len(arr)
    for i in range(arr_len):
        min_index = i
        for j in range(i+1, arr_len):
            if arr[j] < arr[min_index]:  # find the minimum point from the unsorted list
                min_index = j
        arr[i], arr[min_index] = arr[min_index], arr[i]
    return
arr = [24, 37, -1, 25, 7, 99, 11, 45]
selection_sort(arr)
print(arr)
```
>[-1, 7, 11, 24, 25, 37, 45, 99]


Time Complexity:
- Worst Case: O(n<sup>2</sup>) 
- Average Case: O(n<sup>2</sup>) 
- Best case: O(n<sup>2</sup>) 

Auxiliary Space Complexity:
- O(1)

Stability:
- Unstable

Stability explantion: think about an array [8, 3, 8, 1, 9], and after the first round, the first 8(array[0]) will be swapped with 1(array[3]). 

# Insertion sort <a name="is"></a>
Insertion sort is a sorting algorithm in which the given array is **divided into a sorted and an unsorted section**. In each iteration, the element to be inserted has to find its optimal position in the sorted subsequence and is then inserted while shifting the remaining elements to the right. Below is an example:
![image](https://www.crio.do/blog/content/images/2022/01/Insertion-sort-algorithm-example-1.png)

Implementation in Python:
```python
def insertion_sort(arr):
    arr_len = len(arr)
    for i in range(1, arr_len):
        val = arr[i]
        j = i - 1
        while j >= 0 and val < arr[j]: # find the place to insert arr[i]
            arr[j+1] = arr[j]
            j -= 1
        arr[j+1] = val
    return

arr = [12, 24, 37, -1, -20, 7, 99, 11, 45]
insertion_sort(arr)
print(arr)
```
>[-20, -1, 7, 11, 12, 24, 37, 45, 99]

Time Complexity:
- Worst Case: O(n<sup>2</sup>) 
- Average Case: O(n<sup>2</sup>) 
- Best case: O(n) 

Auxiliary Space Complexity:
- O(1)

Stability:
- Stable

# Quick sort <a name="qs"></a>
Quick Sort is a divide and conquer algorithm. The intuitive idea behind quick sort is it picks an element as the pivot(usually the last element) from a given array of elements and then partitions the array around the pivot element. Subsequently, it calls itself recursively and partitions the two subarrays thereafter. Below is an example:
![image](https://www.crio.do/blog/content/images/size/w1000/2022/01/Quick-Sort-Algorithm-flow.png)

```python
def partition(arr, low, high):
    pivot = arr[high]
    i = low
    for j in range(low, high):
        if arr[j] <= pivot:
            arr[i], arr[j] = arr[j], arr[i]  # switch the smaller value to the left
            i+=1
    arr[i], arr[high] = arr[high], arr[i]  # put the pivot in the middle
    return i

def quick_sort(arr, low, high):
    if low < high:
        pi = partition(arr, low, high)
        quick_sort(arr, low, pi - 1)
        quick_sort(arr, pi + 1, high)  # pivot is in the correct place, so no need to include pivot again
    return

arr = [12, 24, 37, -1, -20, 7, 99, 11, 103, 45]
quick_sort(arr, 0, len(arr)-1)
print(arr)
```
> [-20, -1, 7, 11, 12, 24, 37, 45, 99, 103]


Time Complexity:
- Worst Case: O(n<sup>2</sup>) 
- Average Case: O(n*logn) 
- Best case: O(n*logn) 

Auxiliary Space Complexity:
- O(logn)

Stability:
- Stable

Quicksort with in-place and unstable partitioning uses only constant additional space before making any recursive call. Quicksort must store a constant amount of information for each nested recursive call.
