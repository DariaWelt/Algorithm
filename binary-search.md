+ [Binary Search](#binary-search)
+ [Search In Rotated Sorted Array](#search-in-rotated-sorted-array)
+ [Find Minimum in Rotated Sorted Array](#find-minimum-in-rotated-sorted-array)
+ [Find K Closest Elements](#find-k-closest-elements)

## Binary Search
https://leetcode.com/problems/binary-search/
```C++
int search(vector<int>& nums, int target) {
    int left = 0, right = nums.size() - 1;
    while (left < right) {
        int mid = left + (right - left + 1)/2;
        if (nums[mid] > target) 
            right = mid - 1;
        else
            left = mid;
    }
    return nums[left] == target ? left : -1;
}
```

## Search In Rotated Sorted Array
https://leetcode.com/problems/search-in-rotated-sorted-array/

```C++
```

## Find Minimum in Rotated Sorted Array
https://leetcode.com/problems/find-minimum-in-rotated-sorted-array/

```C++
```

## Find K Closest Elements
https://leetcode.com/problems/find-k-closest-elements/

```C++
```
