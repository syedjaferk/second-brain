---
layout: post
title: 'POTD #3 Search in a row-wise sorted matrix | Geeks For Geeks'
date: 2024-12-23 10:25:59+00:00
render_with_liquid: false
category: Algorithm
tags:
- Matrix Search
- Binary Search
- Sorted Matrix
---



<p class="wp-block-paragraph"></p><h3 class="wp-block-heading">Problem Statement</h3><blockquote class="wp-block-quote is-layout-flow wp-block-quote-is-layout-flow"><p class="wp-block-paragraph">GFG Link – <a href="https://www.geeksforgeeks.org/problems/search-in-a-row-wise-sorted-matrix/1">https://www.geeksforgeeks.org/problems/search-in-a-row-wise-sorted-matrix/1</a></p></blockquote><p class="wp-block-paragraph">Given a row-wise sorted 2D matrix <strong>mat</strong>[][] of size <strong>n x m </strong>andan integer <strong>x,</strong> find whether element <strong>x</strong> is present in the matrix.<br/>Note: In a row-wise sorted matrix, each row is sorted in itself, i.e. for any i, j within bounds, mat[i][j] &lt;= mat[i][j+1].</p><pre class="wp-block-syntaxhighlighter-code">Input: mat[][] = [[3, 4, 9],[2, 5, 6],[9, 25, 27]], x = 9Output: trueExplanation: 9 is present in the matrix, so the output is true.</pre><p class="wp-block-paragraph"></p><pre class="wp-block-syntaxhighlighter-code">Input: mat[][] = [[19, 22, 27, 38, 55, 67]], x = 56Output: falseExplanation: 56 is not present in the matrix, so the output is false.</pre><p class="wp-block-paragraph"></p><p class="wp-block-paragraph"><strong>My Approach:</strong></p><p class="wp-block-paragraph">Today’s problem is same as <a href="https://parottasalna.com/2024/12/22/potd-2-search-in-a-row-column-sorted-matrix-geeks-for-geeks/">yesterday’s problem</a>. But i got timed out. So instead of calculating the len(arr) each time (which is same always ) i just stored it in a variable and passed. </p><pre class="wp-block-syntaxhighlighter-code">class Solution:    def binary_search(self, arr, x, start, stop):        if start &gt; stop:            return False        mid = (start + stop) // 2        if start == stop and arr[start] != x:            return False        if arr[mid] == x:            result = self.binary_search(arr, x, 0, length)        elif arr[mid] &gt; x:            return self.binary_search(arr, x, start, mid)        else:            return self.binary_search(arr, x, mid+1, stop)        #Function to search a given number in row-column sorted matrix.    def searchRowMatrix(self, mat, x):     	# code here     	length = len(mat[0]) - 1    	for arr in mat:            result = self.binary_search(arr, x, 0, length)            if result:                return True        return False</pre>


## Related Posts
- [[POTD #2 Search in a Row-Column sorted matrix | Geeks For Geeks]]
- [[POTD #4 - Search in a sorted Matrix | Geeks For Geeks]]
- [[POTD #5 - Set Matrix Zeroes | Geeks For Geeks]]
- [[POTD #6 - Two Sum - Pair with Given Sum | Geeks For Geeks]]
- [[Understanding Common Table Expressions (CTE) in SQL — Simplifying Complex Queries]]

