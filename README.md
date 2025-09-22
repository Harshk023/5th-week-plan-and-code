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


"""
Day 30: Merge Sort & Quick Sort Implementation
Author: [Your Name]
Date: [Today's Date]

Algorithms Implemented:
1. Merge Sort
2. Quick Sort
"""

# ----------------------------------------------------
# 1. Merge Sort
# ----------------------------------------------------
"""
Idea:
- Divide the array into two halves
- Recursively sort both halves
- Merge the two sorted halves

Time Complexity: O(n log n)
Space Complexity: O(n) (extra array for merging)
"""

def merge_sort(arr):
    if len(arr) <= 1:
        return arr
    
    mid = len(arr) // 2
    left = merge_sort(arr[:mid])
    right = merge_sort(arr[mid:])
    
    return merge(left, right)

def merge(left, right):
    result = []
    i = j = 0
    
    # Merge two sorted arrays
    while i < len(left) and j < len(right):
        if left[i] <= right[j]:
            result.append(left[i])
            i += 1
        else:
            result.append(right[j])
            j += 1
    
    # Append remaining elements
    result.extend(left[i:])
    result.extend(right[j:])
    return result


# ----------------------------------------------------
# 2. Quick Sort
# ----------------------------------------------------
"""
Idea:
- Choose a pivot element
- Partition array into two parts:
    left (elements <= pivot), right (elements > pivot)
- Recursively apply quick sort to both parts

Time Complexity:
- Average: O(n log n)
- Worst Case: O(n^2) (when pivot is always min/max)
Space Complexity: O(log n) recursion stack
"""

def quick_sort(arr):
    if len(arr) <= 1:
        return arr
    
    pivot = arr[len(arr)//2]  # choose middle element as pivot
    left = [x for x in arr if x < pivot]
    mid = [x for x in arr if x == pivot]
    right = [x for x in arr if x > pivot]
    
    return quick_sort(left) + mid + quick_sort(right)


# ----------------------------------------------------
# Example Usage
# ----------------------------------------------------
if __name__ == "__main__":
    nums = [38, 27, 43, 3, 9, 82, 10]
    
    print("Original Array:", nums)
    print("Merge Sort:", merge_sort(nums.copy()))
    print("Quick Sort:", quick_sort(nums.copy()))


# ----------------------------------------------------
# Time Complexity Summary:
# ----------------------------------------------------
# Merge Sort: O(n log n), Space: O(n)
# Quick Sort: Average O(n log n), Worst O(n^2), Space: O(log n)
# ----------------------------------------------------


"""
Day 31: Greedy Basics – Activity Selection Problem
Author: [Your Name]
Date: [Today's Date]

Problem:
You are given n activities with start and finish times. 
Select the maximum number of activities that can be performed by a single person, 
assuming the person can work on only one activity at a time.

Approach (Greedy):
1. Sort activities by their finish time.
2. Always pick the next activity whose start time is >= finish time of the last selected activity.
3. This greedy strategy ensures maximum number of activities.

Time Complexity: O(n log n) [for sorting]
Space Complexity: O(1)
"""

# ----------------------------------------------------
# Function to perform Activity Selection
# ----------------------------------------------------
def activity_selection(activities):
    # Sort activities by finish time
    activities.sort(key=lambda x: x[1])
    
    selected = []
    last_finish = -1
    
    for start, finish in activities:
        if start >= last_finish:
            selected.append((start, finish))
            last_finish = finish
    
    return selected


# ----------------------------------------------------
# Example Usage
# ----------------------------------------------------
if __name__ == "__main__":
    activities = [(1, 3), (2, 4), (0, 6), (5, 7),
                  (8, 9), (5, 9)]
    
    print("Activities (start, finish):", activities)
    result = activity_selection(activities)
    print("Selected Activities:", result)
    # Expected Output: [(1, 3), (5, 7), (8, 9)]


# ----------------------------------------------------
# Key Notes:
# ----------------------------------------------------
# - Sort by finish times.
# - Always pick the earliest finishing activity available.
# - Greedy choice ensures global optimal solution.
# ----------------------------------------------------


"""
Day 32: Merge Intervals (LC #56)
Author: [Your Name]
Date: [Today's Date]

Problem Statement (LC #56):
Given an array of intervals where intervals[i] = [start, end], 
merge all overlapping intervals, and return an array of the non-overlapping intervals.

Example:
Input: intervals = [[1,3],[2,6],[8,10],[15,18]]
Output: [[1,6],[8,10],[15,18]]
"""

# ----------------------------------------------------
# Approach:
# ----------------------------------------------------
"""
1. Sort intervals by start time.
2. Traverse through intervals:
   - If current interval overlaps with the last one in result → merge them.
   - Else, add it as a new interval.
3. Return merged intervals.

Time Complexity: O(n log n) (for sorting)
Space Complexity: O(n) (for result)
"""

def merge(intervals):
    if not intervals:
        return []
    
    # Step 1: Sort intervals by start time
    intervals.sort(key=lambda x: x[0])
    
    merged = [intervals[0]]
    
    for current in intervals[1:]:
        prev = merged[-1]
        if current[0] <= prev[1]:  # Overlap
            merged[-1][1] = max(prev[1], current[1])
        else:
            merged.append(current)
    
    return merged


# ----------------------------------------------------
# Example Usage
# ----------------------------------------------------
if __name__ == "__main__":
    intervals = [[1,3],[2,6],[8,10],[15,18]]
    print("Input:", intervals)
    print("Merged Intervals:", merge(intervals))
    # Expected Output: [[1,6],[8,10],[15,18]]
    
    intervals2 = [[1,4],[4,5]]
    print("Input:", intervals2)
    print("Merged Intervals:", merge(intervals2))
    # Expected Output: [[1,5]]


# ----------------------------------------------------
# Key Notes:
# ----------------------------------------------------
# - Sort intervals → ensures easy merging.
# - Greedy choice: merge as soon as overlap is detected.
# - Used in scheduling, range merging, and timeline problems.
# ----------------------------------------------------


"""
Day 33: Minimum Arrows to Burst Balloons (LC #452)
Author: [Your Name]
Date: [Today's Date]

Problem Statement (LC #452):
There are some spherical balloons taped onto a wall that represent intervals.
Balloons are represented as [x_start, x_end] where x_start < x_end.
You must burst all the balloons by shooting the minimum number of arrows.

An arrow shot at coordinate x will burst all balloons where x_start <= x <= x_end.

Return the minimum number of arrows required.

Example:
Input: points = [[10,16],[2,8],[1,6],[7,12]]
Output: 2
"""

# ----------------------------------------------------
# Approach:
# ----------------------------------------------------
"""
1. Sort balloons by their end coordinate.
2. Greedily place an arrow at the end of the first balloon.
3. For each balloon:
   - If its start <= arrow position → already burst.
   - Else, shoot a new arrow at this balloon's end.
4. Count arrows.

Time Complexity: O(n log n) (sorting)
Space Complexity: O(1)
"""

def findMinArrowShots(points):
    if not points:
        return 0
    
    # Sort by end coordinate
    points.sort(key=lambda x: x[1])
    
    arrows = 1
    arrow_pos = points[0][1]
    
    for start, end in points[1:]:
        if start > arrow_pos:  # Need new arrow
            arrows += 1
            arrow_pos = end  # Place new arrow at current end
    
    return arrows


# ----------------------------------------------------
# Example Usage
# ----------------------------------------------------
if __name__ == "__main__":
    points1 = [[10,16],[2,8],[1,6],[7,12]]
    print("Input:", points1)
    print("Minimum Arrows:", findMinArrowShots(points1))  # Expected: 2
    
    points2 = [[1,2],[3,4],[5,6],[7,8]]
    print("Input:", points2)
    print("Minimum Arrows:", findMinArrowShots(points2))  # Expected: 4
    
    points3 = [[1,2],[2,3],[3,4],[4,5]]
    print("Input:", points3)
    print("Minimum Arrows:", findMinArrowShots(points3))  # Expected: 2


# ----------------------------------------------------
# Key Notes:
# ----------------------------------------------------
# - Sort by balloon end coordinates.
# - Always place arrow at the earliest possible end.
# - Greedy choice ensures minimum arrows used.
# ----------------------------------------------------
