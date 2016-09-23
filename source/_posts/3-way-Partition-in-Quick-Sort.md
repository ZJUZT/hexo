---
title: 3-way Partition in Quick Sort
date: 2016-09-22 20:18:24
category: Algorithm
tags:
---

Quick Sort is a great sorting algorithm with an average time complexity O(nlogn). However, quick sort will degrade to O(n^2) when the array to be sorted has few unique elements. Fortunately, it is possible to improve this algorithm, using 3-way partition. In this blog, we will focus on the partition part and leave other components of quick sort aside(like divide and conquer).

<!-- more -->

## 2-way partition

Traditional quick sort uses 2-way partition. Firstly we choose one pivot in some way (leftmost, rightmost, random...). Then we use 2 pointers to traverse the array, p1 from left to right, p2 from right to left.

When we find element less or equal than pivot, we exchange the two elements. We keep this process until the two pointers come across. 

```java
 private static int partition2(int[] a, int l, int r) {

        int i = l,j=r+1;
        int pivot = a[l];

        while (true){
            while (a[--j]>pivot);
            while (a[++i]<=pivot){
                if(i==r){
                    break;
                }
            }

            if(i>=j){
                break;
            }

            int t = a[i];
            a[i] = a[j];
            a[j] = t;
        }

        int t = a[j];
        a[j] = a[l];
        a[l] = t;
        return j;

    }
```



## 3-way partition

2-way partition doesn't handle well on the condition that the array has too many duplicate elements. 

We adjust the partition a little bit to deal with this extreme situation. We divide the array into 4 segments:

{% asset_img 1.png  %}

We mantain four pointers. The two additional pointers are used to mark the two equal-to-pivot segments. When the two traversing pointers find elements equal to pivot, we swap it to the two ends. At last, we move the two ends to the center.

{% asset_img 2.png  %}

```java
private static int[] partition3(int[] a, int l, int r) {

        int i = l, j = r + 1, m = l, n = r + 1;
        int pivot = a[l];

        while (true) {
            while (a[--j] > pivot) ;
            while (a[++i] < pivot) {
                if (i == r) {
                    break;
                }
            }

            if (i >= j) {
                break;
            }

            //swap

            int t = a[i];
            a[i] = a[j];
            a[j] = t;

            if (a[i] == pivot) {
                m++;
                t = a[i];
                a[i] = a[m];
                a[m] = t;
            }

            if (a[j] == pivot) {
                n--;
                t = a[j];
                a[j] = a[n];
                a[n] = t;
            }
        }

        int t = a[l];
        a[l] = a[j];
        a[j] = t;
        i = j + 1;
        j = j - 1;

        // move the equal part to the center

        for (int k = l + 1; k < m + 1; k++, j--) {
            t = a[j];
            a[j] = a[k];
            a[k] = t;
        }

        for (int k = r; k > n - 1; k--, i++) {
            t = a[i];
            a[i] = a[k];
            a[k] = t;
        }
        return new int[]{j, i};
    }
```

Acknowledgement: <https://www.cs.princeton.edu/~rs/talks/QuicksortIsOptimal.pdf>