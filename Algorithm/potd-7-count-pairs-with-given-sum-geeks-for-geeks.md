---
layout: post
title: 'POTD #7 - Count pairs with given sum | Geeks For Geeks'
date: 2024-12-26 18:50:24+00:00
render_with_liquid: false
category: Algorithm
tags:
- Count Pairs
- GeeksForGeeks
- Sum Problem
- Array Manipulation
- Python
---



<p class="wp-block-paragraph"></p><h2 class="wp-block-heading">Problem Statement</h2><blockquote class="wp-block-quote is-layout-flow wp-block-quote-is-layout-flow"><p class="wp-block-paragraph">Geeks For Geeks – <a href="https://www.geeksforgeeks.org/problems/count-pairs-with-given-sum--150253/1">https://www.geeksforgeeks.org/problems/count-pairs-with-given-sum–150253/1</a></p></blockquote><p class="wp-block-paragraph">Given an array <strong>arr[]</strong> and an integer <strong>target</strong>. You have to find numbers of pairs in array <strong>arr[]</strong> which sums up to given <strong>target.</strong></p><pre class="wp-block-syntaxhighlighter-code">Input: arr[] = [1, 5, 7, -1, 5], target = 6 Output: 3Explanation: Pairs with sum 6 are (1, 5), (7, -1) and (1, 5). </pre><p class="wp-block-paragraph"></p><pre class="wp-block-syntaxhighlighter-code">Input: arr[] = [1, 1, 1, 1], target = 2 Output: 6Explanation: Pairs with sum 2 are (1, 1), (1, 1), (1, 1), (1, 1), (1, 1).</pre><p class="wp-block-paragraph"></p><pre class="wp-block-syntaxhighlighter-code">Input: arr[] = [10, 12, 10, 15, -1], target = 125Output: 0</pre><p class="wp-block-paragraph"></p><h2 class="wp-block-heading">My Approach</h2><p class="wp-block-paragraph">Today’s problem is similar to <a href="https://parottasalna.com/2024/12/26/potd-6-two-sum-pair-with-given-sum-geeks-for-geeks/">Two Sum problem</a>, but with a counter. </p><pre class="wp-block-syntaxhighlighter-code">class Solution:    #Complete the below function    def countPairs(self,arr, target):        #Your code here        hash_count = {}        total_count = 0        for num in arr:            rem = target - num            if hash_count.get(rem):                total_count += hash_count.get(rem)            hash_count[num] = hash_count.get(num, 0) + 1        return total_count</pre><p class="wp-block-paragraph"></p><figure class="wp-block-image size-large"><img alt="" class="wp-image-1865" data-recalc-dims="1" decoding="async" height="1011" loading="lazy" src="https://i0.wp.com/parottasalna.com/wp-content/uploads/2024/12/screenshot-from-2024-12-27-00-15-04.png?resize=1915%2C1011&amp;ssl=1" width="1915"/></figure>


## Related Posts
- [[POTD #18 - Pair with given sum in a sorted array | Geeks For Geeks]]
- [[POTD #6 - Two Sum - Pair with Given Sum | Geeks For Geeks]]
- [[POTD #16 - Count Pairs whose sum is less than target | Geeks For Geeks]]
- [[POTD #17 - Sum Pair closest to target | Geeks For Geeks]]
- [[POTD #13 - Subarrays with sum K | Geeks For Geeks]]

