# 搜索算法教程

这个教程介绍了几种常见的搜索算法，并通过代码示例进行讲解。这些算法包括：

- Linear Search
- Binary Search

### 线性搜索

线性搜索是一种简单的搜索算法，通过逐一检查每个元素来找到目标值。时间复杂度为 \(O(n)\)。

```python name=linear_search.py
def linear_search(arr, x):
    """
    线性搜索：在数组中找到目标元素
    时间复杂度: O(n)
    """
    for i in range(len(arr)):
        if arr[i] == x:
            return i
    return -1

# 示例
arr = [2, 3, 4, 10, 40]
x = 10
result = linear_search(arr, x)
if result != -1:
    print(f"元素在索引 {result} 处")
else:
    print("元素不在数组中")
```

### 二分搜索

二分搜索是一种高效的搜索算法，适用于排序数组。通过逐步缩小搜索范围来找到目标值。时间复杂度为 \(O(\log n)\)。

```python name=binary_search.py
def binary_search(arr, x):
    """
    二分搜索：在排序数组中找到目标元素
    时间复杂度: O(log n)
    """
    l, r = 0, len(arr) - 1
    while l <= r:
        mid = l + (r - l) // 2
        if arr[mid] == x:
            return mid
        elif arr[mid] < x:
            l = mid + 1
        else:
            r = mid - 1
    return -1

# 示例
arr = [2, 3, 4, 10, 40]
x = 10
result = binary_search(arr, x)
if result != -1:
    print(f"元素在索引 {result} 处")
else:
    print("元素不在数组中")
```
