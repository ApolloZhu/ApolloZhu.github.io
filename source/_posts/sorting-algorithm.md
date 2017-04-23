---
title: 排序算法
date: 2017-03-20 11:14:39
tags:
- algorithm
- Java
categories:
- 编程
---

目前包括：选择排序，插入排序，归并排序

情景：将数组 a 中的 n 个整数从小到大排序

```java
int[] a;
void swap(int[] a, int i, int j) {
    int temp = a[i];
        a[i] = a[j];
        a[j] = temp;
}
```

<!-- more -->

## 选择排序

比较次数：n(n-1)/2

时间复杂度：O(n^2)

### 选择最小

```java
for (int i=0;i<a.length-1;i++) {
    int minIndex = i;
    for (int j=i+1;i<a.length;i++)
        if (a[j] < a[minIndex])
            minIndex = j;
    swap(a, minIndex, i);
}
```

### 选择最大

```java
for (int i=0;i<a.length-1;i++) {
    int maxIndex = i;
    for (int j=0;j<a.length-i;j++)
        if (a[j] > a[maxIndex])
            maxIndex = j;
    swap(a, maxIndex, i);
}
```

## 插入排序

时间复杂度：O(n^2)

```java
for (int i=1;i<a.length;i++) {
    int cur = a[i], newIdx = i;
    while (newIdx > 0 && a[newIdx-1] > cur)
        a[newIdx] = a[--newIdx];
    a[newIdx] = cur;
}
```

## 归并排序

时间复杂度：O(nlogn)

```java
void mergeSort(int[] a) {
    mergeSort(a, 0, a.length-1);
}
void mergeSort(int[] a, int start, int end) {
    if (start >= end) return;
    
    int mid = (start+end)/2,
          i = start,
          j = mid+1,
        len = end-start+1,
     temp[] = new int[len];

    mergeSort(a, i, mid);
    mergeSort(a, j, end);

    for (int k=0;k<len;k++)
        if (j>end || i<=mid && a[i]<a[j])
            temp[k] = a[i++];
        else
            temp[k] = a[j++];

    for (int k=0;k<len;k++)
        a[start+k] = temp[k];
}
```
