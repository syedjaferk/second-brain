---
layout: post
title: 'POTD #19 - Count the number of possible triangles | Geeks For Geeks'
date: 2025-01-08 15:08:24+00:00
render_with_liquid: false
category: Mathematics
tags:
- Triangle Counting
- GeeksForGeeks
- Algorithm Problem
- Arrays
---



<p class="wp-block-paragraph"></p><h2 class="wp-block-heading">Problem Statement</h2><blockquote class="wp-block-quote is-layout-flow wp-block-quote-is-layout-flow"><p class="wp-block-paragraph">Geeks For Geeks – <a href="https://www.geeksforgeeks.org/problems/count-possible-triangles-1587115620/1">https://www.geeksforgeeks.org/problems/count-possible-triangles-1587115620/1</a></p></blockquote><p class="wp-block-paragraph">Given an integer array <strong>arr[]</strong>. Find the number of triangles that can be formed with three different array elements as lengths of three sides of the triangle.  A triangle with three given sides is only possible if sum of any two sides is always greater than the third side.</p><p class="wp-block-paragraph"></p><pre class="wp-block-syntaxhighlighter-code">Input: arr[] = [4, 6, 3, 7]Output: 3Explanation: There are three triangles possible [3, 4, 6], [4, 6, 7] and [3, 6, 7]. Note that [3, 4, 7] is not a possible triangle.  </pre><p class="wp-block-paragraph"></p><pre class="wp-block-syntaxhighlighter-code">Input: arr[] = [10, 21, 22, 100, 101, 200, 300]Output: 6Explanation: There can be 6 possible triangles: [10, 21, 22], [21, 100, 101], [22, 100, 101], [10, 100, 101], [100, 101, 200] and [101, 200, 300]</pre><p class="wp-block-paragraph"></p><h2 class="wp-block-heading">My Approach</h2><pre class="wp-block-syntaxhighlighter-code">class Solution:    #Function to count the number of possible triangles.    def countTriangles(self, arr):        # code here        arr.sort()        n = len(arr)        cnt = 0        for itr in range(2, n):            left = 0            right = itr - 1                        while left &lt; right:                                if arr[left] + arr[right] &gt; arr[itr]:                    cnt += right - left                    right -= 1                else:                    left += 1        return cnt</pre>


## Related Posts
- [[POTD #15 - Count all triplets with given sum in sorted array | Geeks For Geeks]]
- [[POTD #6 - Two Sum - Pair with Given Sum | Geeks For Geeks]]
- [[POTD #16 - Count Pairs whose sum is less than target | Geeks For Geeks]]
- [[POTD #9 - Intersection of Two arrays with Duplicate Elements | Geeks For Geeks]]
- [[POTD #14 - Count Subarrays with given XOR  | Geeks For Geeks]]

