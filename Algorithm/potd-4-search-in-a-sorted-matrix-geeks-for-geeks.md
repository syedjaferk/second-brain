---
layout: post
title: 'POTD #4 - Search in a sorted Matrix | Geeks For Geeks'
date: 2024-12-24 06:29:36+00:00
render_with_liquid: false
category: Algorithm
tags:
- Matrix Search
- Binary Search
- GeeksForGeeks
---



<h3 class="wp-block-heading">Problem Statement</h3><blockquote class="wp-block-quote is-layout-flow wp-block-quote-is-layout-flow"><p class="wp-block-paragraph">Geeks For Geeks – <a href="https://www.geeksforgeeks.org/problems/search-in-a-matrix-1587115621/1">https://www.geeksforgeeks.org/problems/search-in-a-matrix-1587115621/1</a></p></blockquote><p class="wp-block-paragraph">Given a strictly sorted 2D matrix<strong> mat</strong>[][] of size <strong>n x m </strong>anda number <strong>x.</strong> Find whether the number <strong>x</strong> is present in the matrix or not.</p><p class="wp-block-paragraph"><br/>Note: In a strictly sorted matrix, each row is sorted in strictly increasing order, and the first element of the <strong>i</strong><sup>th</sup> row (<strong>i</strong>!=0) is greater than the last element of the (<strong>i-1</strong>)<sup>th </sup>row.</p><pre class="wp-block-syntaxhighlighter-code">Input: mat[][] = [[1, 5, 9], [14, 20, 21], [30, 34, 43]], x = 14Output: trueExplanation: 14 is present in the matrix, so output is true.</pre><h3 class="wp-block-heading">My Approach</h3><p class="wp-block-paragraph">Today’s problem is same as <a href="https://parottasalna.com/2024/12/22/potd-2-search-in-a-row-column-sorted-matrix-geeks-for-geeks/">yesterday’s problem</a>. </p><pre class="wp-block-syntaxhighlighter-code">class Solution:        def binary_search(self, arr, x, start, stop):        if start &gt; stop:            return False        mid = (start + stop) // 2        if start == stop and arr[start] != x:            return False        if arr[mid] == x:            return True        elif arr[mid] &gt; x:            return self.binary_search(arr, x, start, mid)        else:            return self.binary_search(arr, x, mid+1, stop)        #Function to search a given number in row-column sorted matrix.    def searchMatrix(self, mat, x):     	# code here     	length = len(mat[0]) - 1        for arr in mat:            result = self.binary_search(arr, x, 0, length)            if result:                return True        return False    	</pre><figure class="wp-block-image size-large"><img alt="" class="wp-image-1744" data-recalc-dims="1" decoding="async" height="1009" loading="lazy" src="https://i0.wp.com/parottasalna.com/wp-content/uploads/2024/12/screenshot-from-2024-12-24-11-52-05.png?resize=1916%2C1009&amp;ssl=1" width="1916"/></figure>


## Related Posts
- [[POTD #3 Search in a row-wise sorted matrix | Geeks For Geeks]]
- [[POTD #2 Search in a Row-Column sorted matrix | Geeks For Geeks]]
- [[POTD #6 - Two Sum - Pair with Given Sum | Geeks For Geeks]]
- [[POTD #5 - Set Matrix Zeroes | Geeks For Geeks]]
- [[POTD #11 - Longest Consecutive Subsequence | Geeks For Geeks]]

