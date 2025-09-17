------------------------------------------------------
Week 5: Sorting, Divide & Conquer, Greedy
------------------------------------------------------
Day 29: Bubble, insertion, selection sort (implement)
Day 30: Merge sort, quick sort implementation
Day 31: Greedy basics: activity selection problem
Day 32: Merge intervals (LC #56)
Day 33: Minimum arrows to burst balloons (LC #452)
Day 34: Gas station (LC #134)
Day 35: Practice greedy problems


"""
Day 29: Implement Basic Sorting Algorithms
Author: [Your Name]
Date: [Today's Date]

Algorithms Implemented:
1. Bubble Sort
2. Insertion Sort
3. Selection Sort
"""

# ----------------------------------------------------
# 1. Bubble Sort
# ----------------------------------------------------
"""
Idea:
- Repeatedly swap adjacent elements if they are in the wrong order.
- Largest element "bubbles up" to the end in each pass.

Time Complexity: O(n^2)
Space Complexity: O(1)
"""

def bubble_sort(arr):
    n = len(arr)
    for i in range(n-1):
        for j in range(n-1-i):
            if arr[j] > arr[j+1]:
                arr[j], arr[j+1] = arr[j+1], arr[j]
    return arr


# ----------------------------------------------------
# 2. Insertion Sort
# ----------------------------------------------------
"""
Idea:
- Divide array into sorted and unsorted part.
- Pick one element from unsorted part and insert it in the correct place in sorted part.

Time Complexity: O(n^2)
Best Case: O(n) when already sorted
Space Complexity: O(1)
"""

def insertion_sort(arr):
    for i in range(1, len(arr)):
        key = arr[i]
        j = i-1
        while j >= 0 and key < arr[j]:
            arr[j+1] = arr[j]
            j -= 1
        arr[j+1] = key
    return arr


# ----------------------------------------------------
# 3. Selection Sort
# ----------------------------------------------------
"""
Idea:
- Repeatedly find the minimum element from the unsorted part and put it at the beginning.
- After i-th iteration, first i elements are sorted.

Time Complexity: O(n^2)
Space Complexity: O(1)
"""

def selection_sort(arr):
    n = len(arr)
    for i in range(n):
        min_index = i
        for j in range(i+1, n):
            if arr[j] < arr[min_index]:
                min_index = j
        arr[i], arr[min_index] = arr[min_index], arr[i]
    return arr


# ----------------------------------------------------
# Example Usage
# ----------------------------------------------------
if __name__ == "__main__":
    nums = [64, 25, 12, 22, 11]
    
    print("Original Array:", nums)
    print("Bubble Sort:", bubble_sort(nums.copy()))
    print("Insertion Sort:", insertion_sort(nums.copy()))
    print("Selection Sort:", selection_sort(nums.copy()))


# ----------------------------------------------------
# Time Complexity Summary:
# ----------------------------------------------------
# Bubble Sort:    O(n^2), Space: O(1)
# Insertion Sort: O(n^2), Best Case: O(n), Space: O(1)
# Selection Sort: O(n^2), Space: O(1)
# ----------------------------------------------------
