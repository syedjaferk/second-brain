---
layout: post
title: 'POTD #8 - Find All Triplets with Zero Sum | Geeks For Geeks'
date: 2024-12-28 01:21:54+00:00
render_with_liquid: false
category: Algorithm
tags:
- Triplets
- Sorting
- ZeroSum
- GeeksForGeeks
---



<p class="wp-block-paragraph"></p><h2 class="wp-block-heading">Problem Statement</h2><p class="wp-block-paragraph">Given an array <strong>arr[]</strong>, find all possible triplets <strong>i, j, k</strong> in the <strong>arr[]</strong> whose sum of elements is equals to <strong>zero</strong>. <br/>Returned triplet should also be internally sorted i.e. <strong>i&lt;j&lt;k.</strong></p><p class="wp-block-paragraph"></p><pre class="wp-block-syntaxhighlighter-code">Input: arr[] = [0, -1, 2, -3, 1]Output: [[0, 1, 4], [2, 3, 4]]Explanation: Triplets with sum 0 are:arr[0] + arr[1] + arr[4] = 0 + (-1) + 1 = 0arr[2] + arr[3] + arr[4] = 2 + (-3) + 1 = 0</pre><p class="wp-block-paragraph"></p><pre class="wp-block-syntaxhighlighter-code">Input: arr[] = [1, -2, 1, 0, 5]Output: [[0, 1, 2]]Explanation: Only triplet which satisfies the condition is arr[0] + arr[1] + arr[2] = 1 + (-2) + 1 = 0</pre><p class="wp-block-paragraph"></p><pre class="wp-block-syntaxhighlighter-code">Input: arr[] = [2, 3, 1, 0, 5]Output: [[]]Explanation: There is no triplet with sum 0.</pre><p class="wp-block-paragraph"></p><h2 class="wp-block-heading">My Approach</h2><ul class="wp-block-list"><li>Created a dict with val as key and index as value, after iterating through the array. </li><li>Started iterating the array, and another iteration from the next index position. </li><li>a + b + c = 0. I need to check c (c = 0 – a – b). Will check if c is in dict. </li><li>if c is in dict, then will sort a,b,c and store in result set. </li></ul><p class="wp-block-paragraph"></p><pre class="wp-block-syntaxhighlighter-code">class Solution:    def findTriplets(self, arr):        # Your code here        hash_set = {}        index = 0        total = len(arr)        result = []        result_set = {}                for itr in range(total):            hash_set[arr[itr]] = itr                for first in range(total):            for itr in range(first+1, total):                rem = 0 - arr[itr] - arr[first]                if hash_set.get(rem) is not None and hash_set.get(rem) != first and hash_set.get(rem) != itr:                    val = [first, itr, hash_set.get(rem)]                    val.sort()                    if result_set.get(tuple(val)) is None:                        result_set[tuple(val)] = True                        result.append(val)                        return result</pre><p class="wp-block-paragraph"></p><figure class="wp-block-image size-large"><img alt="" class="wp-image-1905" data-recalc-dims="1" decoding="async" height="1010" loading="lazy" src="https://i0.wp.com/parottasalna.com/wp-content/uploads/2024/12/screenshot-from-2024-12-28-06-36-05.png?resize=1920%2C1010&amp;ssl=1" width="1920"/></figure>


## Related Posts
- [[POTD #6 - Two Sum - Pair with Given Sum | Geeks For Geeks]]
- [[POTD #15 - Count all triplets with given sum in sorted array | Geeks For Geeks]]
- [[POTD #11 - Longest Consecutive Subsequence | Geeks For Geeks]]
- [[POTD #14 - Count Subarrays with given XOR  | Geeks For Geeks]]
- [[POTD #18 - Pair with given sum in a sorted array | Geeks For Geeks]]

