---
layout: post
title: 'POTD #14 - Count Subarrays with given XOR  | Geeks For Geeks'
date: 2025-01-03 17:56:19+00:00
render_with_liquid: false
category: Algorithm
tags:
- XOR
- Subarray
- Counting
- GeeksForGeeks
- Arrays
---



<p class="wp-block-paragraph"></p><h2 class="wp-block-heading">Problem Statement</h2><blockquote class="wp-block-quote is-layout-flow wp-block-quote-is-layout-flow"><p class="wp-block-paragraph">Geeks For Geeks: <a href="https://www.geeksforgeeks.org/problems/count-subarray-with-given-xor/1">https://www.geeksforgeeks.org/problems/count-subarray-with-given-xor/1</a></p></blockquote><p class="wp-block-paragraph">Given an array of integers <strong>arr[]</strong> and a number <strong>k</strong>, count the number of subarrays having <strong>XOR</strong> of their elements as <strong>k</strong>.</p><p class="wp-block-paragraph"></p><pre class="wp-block-syntaxhighlighter-code">Input: arr[] = [4, 2, 2, 6, 4], k = 6Output: 4Explanation: The subarrays having XOR of their elements as 6 are [4, 2], [4, 2, 2, 6, 4], [2, 2, 6], and [6]. Hence, the answer is 4.</pre><p class="wp-block-paragraph"></p><p class="wp-block-paragraph"></p><pre class="wp-block-syntaxhighlighter-code">Input: arr[] = [5, 6, 7, 8, 9], k = 5Output: 2Explanation: The subarrays having XOR of their elements as 5 are [5] and [5, 6, 7, 8, 9]. Hence, the answer is 2.</pre><p class="wp-block-paragraph"></p><h2 class="wp-block-heading">My Approach</h2><p class="wp-block-paragraph">This problem is same as <a href="https://parottasalna.com/2025/01/02/potd-13-subarrays-with-sum-k-geeks-for-geeks/">yesterday’s problem</a>. Instead of sum, here its xor. </p><pre class="wp-block-syntaxhighlighter-code">class Solution:    def subarrayXor(self, arr, k):        # code here        n = len(arr)        pre_xor_map = {}        pre_xor = 0        cnt = 0            pre_xor_map[0] = 1        for i in range(n):            pre_xor = pre_xor ^ arr[i]            remove = pre_xor ^ k            cnt += pre_xor_map.get(remove, 0)            pre_xor_map[pre_xor] = pre_xor_map.get(pre_xor, 0) + 1            return cnt</pre>


## Related Posts
- [[POTD #13 - Subarrays with sum K | Geeks For Geeks]]
- [[POTD #6 - Two Sum - Pair with Given Sum | Geeks For Geeks]]
- [[POTD #11 - Longest Consecutive Subsequence | Geeks For Geeks]]
- [[Python Generators – The Lazy Workers of Python]]
- [[POTD #8 - Find All Triplets with Zero Sum | Geeks For Geeks]]

