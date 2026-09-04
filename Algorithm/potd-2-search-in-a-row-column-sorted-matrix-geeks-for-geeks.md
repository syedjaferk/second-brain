---
layout: post
title: 'POTD #2 Search in a Row-Column sorted matrix | Geeks For Geeks'
date: 2024-12-22 05:50:35+00:00
render_with_liquid: false
category: Algorithm
tags:
- Matrix Search
- Binary Search
- Sorting
- GeeksForGeeks
- POTD
---



<p class="wp-block-paragraph"></p><p class="wp-block-paragraph">Second day of POTD Geeks For Geeks. <a href="https://www.geeksforgeeks.org/problems/search-in-a-matrix17201720/1">https://www.geeksforgeeks.org/problems/search-in-a-matrix17201720/1</a>.</p><p class="wp-block-paragraph"></p><p class="wp-block-paragraph">Given a 2D integer matrix <strong>mat</strong>[][] of size <strong>n x m</strong>, where every row and column is sorted in increasing order and a number <strong>x</strong>,the task is to find whether element <strong>x</strong> is present in the matrix.</p><p class="wp-block-paragraph"></p><h3 class="wp-block-heading"><strong>Examples:</strong></h3><pre class="wp-block-syntaxhighlighter-code">Input: mat[][] = [[3, 30, 38],[20, 52, 54],[35, 60, 69]], x = 62Output: falseExplanation: 62 is not present in the matrix, so output is false.</pre><pre class="wp-block-syntaxhighlighter-code">Input: mat[][] = [[18, 21, 27],[38, 55, 67]], x = 55Output: trueExplanation: 55 is present in the matrix.</pre><p class="wp-block-paragraph"></p><h3 class="wp-block-heading">My Approach</h3><p class="wp-block-paragraph">The question states that every row in the matrix is sorted in ascending order. So we can use the binary search to find the element inside each array. </p><p class="wp-block-paragraph">So , </p><ol class="wp-block-list"><li>Iterate each array of the matrix.</li><li>Find the element in array using binary search.</li></ol><p class="wp-block-paragraph"></p><pre class="wp-block-syntaxhighlighter-code">#User function Template for python3class Solution:        def binary_search(self, arr, x, start, stop):        if start &gt; stop:            return False        mid = (start + stop) // 2        if start == stop and arr[start] != x:            return False        if arr[mid] == x:            return True        elif arr[mid] &gt; x:            return self.binary_search(arr, x, start, mid)        else:            return self.binary_search(arr, x, mid+1, stop)                        def matSearch(self, mat, x):        # Complete this function        for arr in mat:            result = self.binary_search(arr, x, 0, len(arr)-1)            if result:                return True        return False</pre>


## Related Posts
- [[POTD #3 Search in a row-wise sorted matrix | Geeks For Geeks]]
- [[POTD #4 - Search in a sorted Matrix | Geeks For Geeks]]
- [[Benefits of Binary Insertion Sort Explained]]
- [[POTD #5 - Set Matrix Zeroes | Geeks For Geeks]]
- [[POTD #18 - Pair with given sum in a sorted array | Geeks For Geeks]]

