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
int search(vector<int>& nums, int target) {
    int start = 0, end = nums.size() - 1;
    while (start <= end) {
        int mid = (start + end)/2;
        if (nums[mid] == target)
            return mid;

        if (nums[start] < nums[mid]) {
            if (nums[start] <= target && target < nums[mid])
                end = mid - 1;
            else
                start = mid + 1;
        } 
        else if (nums[mid] < nums[end]) {
            if (nums[mid] < target && target <= nums[end])
                start = mid + 1;
            else
                end = mid - 1;
        }
        else
            ++start;
    }
    return -1;
}
```

## Find Minimum in Rotated Sorted Array
https://leetcode.com/problems/find-minimum-in-rotated-sorted-array/

```C++
int findMin(vector<int>& nums) {
    int right = nums.size() - 1, left = 0;
    if (nums[left] <= nums[right])
        return nums[0];
    while (right >= left) {
        int mid = (right + left)/2;
        if (nums[mid] > nums[mid + 1])
            return nums[mid + 1];
        if (nums[left] < nums[mid])
            left = mid;
        else 
            right = mid;
    }
    return -1;
}
```

## Find K Closest Elements
https://leetcode.com/problems/find-k-closest-elements/

```C++
vector<int> findClosestElements(vector<int>& arr, int k, int x) {
    int left = 0, right = arr.size() - 1;
    for (int i = 0; i < arr.size() - k; ++i) {
        if (x - arr[left] <= arr[right] - x)
            --right;
        else
            ++left;
    }
    vector<int> res(arr.begin() + left, arr.begin() + right + 1);
    return res;
}
```
