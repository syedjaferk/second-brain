---
layout: post
title: 'POTD #16 - Count Pairs whose sum is less than target | Geeks For Geeks'
date: 2025-01-05 17:13:05+00:00
render_with_liquid: false
category: Algorithm
tags:
- Count Pairs
- Sorting
- GeeksForGeeks
---



<p class="wp-block-paragraph"></p><h2 class="wp-block-heading">Problem Statement</h2><blockquote class="wp-block-quote is-layout-flow wp-block-quote-is-layout-flow"><p class="wp-block-paragraph">Geeks For Geeks : <a href="https://www.geeksforgeeks.org/problems/count-pairs-whose-sum-is-less-than-target/1">https://www.geeksforgeeks.org/problems/count-pairs-whose-sum-is-less-than-target/1</a></p></blockquote><p class="wp-block-paragraph">Given an array <strong>arr[]</strong> and an integer <strong>target</strong>. You have to find the number of pairs in the array whose sum is strictly less than the <strong>target</strong>.</p><p class="wp-block-paragraph"></p><pre class="wp-block-syntaxhighlighter-code">Input: arr[] = [7, 2, 5, 3], target = 8Output: 2Explanation: There are 2 pairs with sum less than 8: (2, 5) and (2, 3). </pre><p class="wp-block-paragraph"></p><pre class="wp-block-syntaxhighlighter-code">Input: arr[] = [5, 2, 3, 2, 4, 1], target = 5Output: 4Explanation: There are 4 pairs whose sum is less than 5: (2, 2), (2, 1), (3, 1) and (2, 1).</pre><p class="wp-block-paragraph"></p><h2 class="wp-block-heading">My Approach</h2><p class="wp-block-paragraph">Sorted the array and used two pointer approach to find the possible pairs. </p><pre class="wp-block-syntaxhighlighter-code">class Solution:    #Complete the below function    def countPairs(self, arr, target):        #Your code here        arr.sort()        n = len(arr)        cnt = 0        left = 0        right = n - 1        while right &gt; left:            if arr[right] + arr[left] &lt; target:                cnt += right - left                left += 1            elif arr[right] + arr[left] &gt;= target:                right -= 1                    return cnt                    </pre>


## Related Posts
- [[POTD #6 - Two Sum - Pair with Given Sum | Geeks For Geeks]]
- [[POTD #17 - Sum Pair closest to target | Geeks For Geeks]]
- [[POTD #18 - Pair with given sum in a sorted array | Geeks For Geeks]]
- [[POTD #7 - Count pairs with given sum | Geeks For Geeks]]
- [[POTD #13 - Subarrays with sum K | Geeks For Geeks]]

