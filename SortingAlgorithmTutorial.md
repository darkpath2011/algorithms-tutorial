# 排序算法教程

这个教程介绍了几种常见的排序算法，并通过代码示例进行讲解。这些算法包括冒泡排序、选择排序、插入排序、归并排序、快速排序、堆排序、计数排序、桶排序和基数排序。每个算法都附带详细的注释，适合初学者学习。

## 冒泡排序（Bubble Sort）

通过重复遍历列表并交换相邻元素，将较大的元素逐渐移到列表的末端。时间复杂度: \(O(n^2)\)。

```python name=bubble_sort.py
def bubble_sort(arr):
    n = len(arr)  # 获取数组的长度
    for i in range(n):
        # 从头到尾遍历数组，最后i个元素已经排好，不需要再遍历
        for j in range(0, n-i-1):
            # 如果当前元素大于下一个元素，则交换它们
            if arr[j] > arr[j+1]:
                arr[j], arr[j+1] = arr[j+1], arr[j]
    return arr

# 示例
arr = [64, 34, 25, 12, 22, 11, 90]
print("排序前的数组:", arr)
sorted_arr = bubble_sort(arr)
print("排序后的数组:", sorted_arr)
```

## 选择排序（Selection Sort）

每次从未排序部分中选择最小（或最大）的元素，并将其放到已排序部分的末尾。时间复杂度: \(O(n^2)\)。

```python name=selection_sort.py
def selection_sort(arr):
    n = len(arr)  # 获取数组的长度
    for i in range(n):
        min_idx = i  # 假设当前索引为最小值索引
        # 遍历未排序部分，找出最小值的索引
        for j in range(i+1, n):
            if arr[j] < arr[min_idx]:
                min_idx = j
        # 交换找到的最小值与当前索引的值
        arr[i], arr[min_idx] = arr[min_idx], arr[i]
    return arr

# 示例
arr = [64, 34, 25, 12, 22, 11, 90]
print("排序前的数组:", arr)
sorted_arr = selection_sort(arr)
print("排序后的数组:", sorted_arr)
```

## 插入排序（Insertion Sort）

通过将每个元素插入到已排序部分的正确位置来构建有序列表。时间复杂度: \(O(n^2)\)。

```python name=insertion_sort.py
def insertion_sort(arr):
    for i in range(1, len(arr)):
        key = arr[i]  # 选定要插入的元素
        j = i - 1
        # 将选定元素插入到已排序部分的正确位置
        while j >= 0 and key < arr[j]:
            arr[j + 1] = arr[j]
            j -= 1
        arr[j + 1] = key
    return arr

# 示例
arr = [64, 34, 25, 12, 22, 11, 90]
print("排序前的数组:", arr)
sorted_arr = insertion_sort(arr)
print("排序后的数组:", sorted_arr)
```

## 归并排序（Merge Sort）

采用分治法，将列表分成小部分分别排序，然后合并已排序的小部分。时间复杂度: \(O(n \log n)\)。

```python name=merge_sort.py
def merge_sort(arr):
    if len(arr) > 1:
        mid = len(arr) // 2  # 找到列表的中间点
        L = arr[:mid]  # 分成两部分
        R = arr[mid:]

        merge_sort(L)  # 对左半部分排序
        merge_sort(R)  # 对右半部分排序

        i = j = k = 0

        # 合并两个已排序的部分
        while i < len(L) and j < len(R):
            if L[i] < R[j]:
                arr[k] = L[i]
                i += 1
            else:
                arr[k] = R[j]
                j += 1
            k += 1

        # 检查是否有剩余元素
        while i < len(L):
            arr[k] = L[i]
            i += 1
            k += 1

        while j < len(R):
            arr[k] = R[j]
            j += 1
            k += 1
    return arr

# 示例
arr = [64, 34, 25, 12, 22, 11, 90]
print("排序前的数组:", arr)
sorted_arr = merge_sort(arr)
print("排序后的数组:", sorted_arr)
```

## 快速排序（Quick Sort）

采用分治法，选择一个“基准”元素，将列表分成比基准小的部分和比基准大的部分，分别排序。时间复杂度: 平均 \(O(n \log n)\)，最坏情况下 \(O(n^2)\)。

```python name=quick_sort.py
def quick_sort(arr):
    if len(arr) <= 1:
        return arr
    else:
        pivot = arr[len(arr) // 2]  # 选择一个基准元素
        left = [x for x in arr if x < pivot]  # 小于基准的部分
        middle = [x for x in arr if x == pivot]  # 等于基准的部分
        right = [x for x in arr if x > pivot]  # 大于基准的部分
        return quick_sort(left) + middle + quick_sort(right)  # 分别排序并合并

# 示例
arr = [64, 34, 25, 12, 22, 11, 90]
print("排序前的数组:", arr)
sorted_arr = quick_sort(arr)
print("排序后的数组:", sorted_arr)
```

## 堆排序（Heap Sort）

利用堆数据结构，将列表转换为一个最大堆或最小堆，然后逐个移除堆顶元素构建有序列表。时间复杂度: \(O(n \log n)\)。

```python name=heap_sort.py
def heapify(arr, n, i):
    largest = i  # 假设当前节点为最大值
    l = 2 * i + 1  # 左子节点
    r = 2 * i + 2  # 右子节点

    # 如果左子节点存在且大于当前节点，则更新最大值
    if l < n and arr[i] < arr[l]:
        largest = l

    # 如果右子节点存在且大于当前节点，则更新最大值
    if r < n and arr[largest] < arr[r]:
        largest = r

    # 如果最大值不是当前节点，则交换并继续堆化
    if largest != i:
        arr[i], arr[largest] = arr[largest], arr[i]
        heapify(arr, n, largest)

def heap_sort(arr):
    n = len(arr)

    # 构建最大堆
    for i in range(n // 2 - 1, -1, -1):
        heapify(arr, n, i)

    # 一个个移除元素
    for i in range(n-1, 0, -1):
        arr[i], arr[0] = arr[0], arr[i]
        heapify(arr, i, 0)
    return arr

# 示例
arr = [64, 34, 25, 12, 22, 11, 90]
print("排序前的数组:", arr)
sorted_arr = heap_sort(arr)
print("排序后的数组:", sorted_arr)
```

## 计数排序（Counting Sort）

适用于整数排序，通过计数每个元素出现的次数来构建有序列表。时间复杂度: \(O(n + k)\)，其中 \(k\) 是元素的范围。

```python name=counting_sort.py
def counting_sort(arr):
    max_val = max(arr)  # 找到数组中的最大值
    m = max_val + 1
    count = [0] * m  # 初始化计数数组

    for a in arr:
        count[a] += 1  # 计数

    i = 0
    for a in range(m):
        for c in range(count[a]):
            arr[i] = a
            i += 1
    return arr

# 示例
arr = [4, 2, 2, 8, 3, 3, 1]
print("排序前的数组:", arr)
sorted_arr = counting_sort(arr)
print("排序后的数组:", sorted_arr)
```

## 桶排序（Bucket Sort）

将元素分布到几个桶中，每个桶内分别排序，然后合并。时间复杂度: \(O(n + k)\)，其中 \(k\) 是桶的数量。

```python name=bucket_sort.py
def bucket_sort(arr):
    bucket = []
    # 创建空的桶
    for i in range(len(arr)):
        bucket.append([])

    # 把元素放入桶中
    for j in arr:
        index_b = int(10 * j)
        bucket[index_b].append(j)

    # 对每个桶内部排序
    for i in range(len(arr)):
        bucket[i] = sorted(bucket[i])

    # 合并所有桶中的元素
    k = 0
    for i in range(len(arr)):
        for j in range(len(bucket[i])):
            arr[k] = bucket[i][j]
            k += 1
    return arr

# 示例
arr = [0.897, 0.565, 0.656, 0.1234, 0.665, 0.3434]
print("排序前的数组:", arr)
sorted_arr = bucket_sort(arr)
print("排序后的数组:", sorted_arr)
```

## 基数排序（Radix Sort）

适用于整数或字符串排序，通过按位或字符进行多次排序。时间复杂度: \(O(d(n + k))\)，其中 \(d\) 是位数或字符数，\(k\) 是基数。

```python name=radix_sort.py
def counting_sort_for_radix(arr, exp):
    n = len(arr)
    output = [0] * n
    count = [0] * 10

    for i in range(n):
        index = (arr[i] // exp)
        count[(index % 10)] += 1

    for i in range(1, 10):
        count[i] += count[i - 1]

    i = n - 1
    while i >= 0:
        index = (arr[i] // exp)
        output[count[(index % 10)] - 1] = arr[i]
        count[(index % 10)] -= 1
        i -= 1

    for i in range(len(arr)):
        arr[i] = output[i]

def radix_sort(arr):
    max_val = max(arr)
    exp = 1
    while max_val // exp > 0:
        counting_sort_for_radix(arr, exp)
        exp *= 10
    return arr

# 示例
arr = [170, 45, 75, 90, 802, 24, 2, 66]
print("排序前的数组:", arr)
sorted_arr = radix_sort(arr)
print("排序后的数组:", sorted_arr)
```

---

### 作者声明

本教程由darkpath2011和GithubCopilot编写，旨在为初学者提供简单易懂的排序算法学习资料。如果你有任何问题或建议，请随时与我联系！
