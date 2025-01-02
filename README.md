# GFG_33
---
Difficulty: Medium  
Source: 160 Days of Problem Solving  
Tags:
  - Binary Search
---

# 🚀 _Day 33. Aggressive Cows_ 🧠

The problem can be found at the following link: [Problem Link](https://www.geeksforgeeks.org/batch/gfg-160-problems/track/searching-gfg-160/problem/aggressive-cows)


## 💡 **Problem Description:**

You are given an array `stalls[]` representing the positions of stalls, where each position is unique. You are also given an integer `k`, which is the number of aggressive cows to place. Your task is to assign the cows to the stalls such that the **minimum distance** between any two cows is maximized.

## 🔍 **Example Walkthrough:**

**Input:**  
`stalls[] = [1, 2, 4, 8, 9], k = 3`  
**Output:**  
`3`

**Explanation:**  
- Place the first cow at `stalls[0]`, the second at `stalls[2]`, and the third at `stalls[3]`.  
- The minimum distance between cows is `3`, which is the largest possible.



**Input:**  
`stalls[] = [10, 1, 2, 7, 5], k = 3`  
**Output:**  
`4`

**Explanation:**  
- Place cows at positions `10`, `1`, and `5`.  
- The minimum distance is `4`.



### Constraints:
- $`2 <= stalls.size() <= 10^6`$
- $`0 <= stalls[i] <= 10^8`$
- $`1 <= k <= stalls.size()`$



## 🎯 **My Approach:**

1. **Binary Search on the Distance:**  
   - To maximize the minimum distance between cows, we can use **binary search** on the range of distances.  
   - The range of distances is `[1, stalls[n-1] - stalls[0]]`.

2. **Check Feasibility:**  
   - For a given `mid` (distance), determine if it’s possible to place all `k` cows in the stalls such that the distance between consecutive cows is at least `mid`.  
   - If placing cows is feasible, increase the minimum distance. Otherwise, decrease it.

3. **Steps:**  
   - Sort the `stalls` array.  
   - Use binary search to determine the largest minimum distance.  
   - For each mid, iterate through stalls to count the cows that can be placed with at least `mid` distance.



## 🕒 **Time and Auxiliary Space Complexity** 

**Expected Time Complexity:** 

`O(n * log(m))`, where `n` is the size of the array, and `m` is the range of stall positions (`max - min`). Sorting takes `O(n log m)`, and binary search with feasibility checking takes `O(n * log m)`.  

**Expected Auxiliary Space Complexity:** 

`O(1)`, as we use a constant amount of additional space.

## 📝 **Solution Code**
## Code (Python)

```python
class Solution:
    def aggressiveCows(self, stalls, k):
        stalls.sort()
        low, high = 1, stalls[-1] - stalls[0]

        while low <= high:
            mid = (low + high) // 2
            count, last_placed = 1, stalls[0]
            for i in range(1, len(stalls)):
                if stalls[i] - last_placed >= mid:
                    count += 1
                    last_placed = stalls[i]
            if count >= k:
                low = mid + 1
            else:
                high = mid - 1
        return high
```
