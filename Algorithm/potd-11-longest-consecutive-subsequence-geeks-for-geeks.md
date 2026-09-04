---
layout: post
title: 'POTD #11 - Longest Consecutive Subsequence | Geeks For Geeks'
date: 2024-12-31 17:43:34+00:00
render_with_liquid: false
category: Algorithm
tags:
- Consecutive Sequence
- Array Problem
- GeeksForGeeks
- Subsequence
- Algorithms
---



<p class="wp-block-paragraph"></p><h2 class="wp-block-heading">Problem Statement</h2><blockquote class="wp-block-quote is-layout-flow wp-block-quote-is-layout-flow"><p class="wp-block-paragraph">Geeks For Geeks – <a href="https://www.geeksforgeeks.org/problems/longest-consecutive-subsequence2449/1">https://www.geeksforgeeks.org/problems/longest-consecutive-subsequence2449/1</a></p></blockquote><p class="wp-block-paragraph">Given an array <strong>arr[]</strong> of non-negative integers. Find the <strong>length</strong> of the longest sub-sequence such that elements in the subsequence are consecutive integers, the<strong> consecutive numbers</strong> can be in <strong>any order.</strong></p><p class="wp-block-paragraph"></p><pre class="wp-block-syntaxhighlighter-code">Input: arr[] = [2, 6, 1, 9, 4, 5, 3]Output: 6Explanation: The consecutive numbers here are 1, 2, 3, 4, 5, 6. These 6 numbers form the longest consecutive subsquence.</pre><p class="wp-block-paragraph"></p><pre class="wp-block-syntaxhighlighter-code">Input: arr[] = [1, 9, 3, 10, 4, 20, 2]Output: 4Explanation: 1, 2, 3, 4 is the longest consecutive subsequence.</pre><p class="wp-block-paragraph"></p><h2 class="wp-block-heading">My Approach</h2><p class="wp-block-paragraph">1. Sort the array.Initialize two variables:</p><ul class="wp-block-list"><li><code>max_sequence</code> to 1 (to store the length of the longest consecutive subsequence).</li><li><code>cont_sub_sequence</code> to 1 (to track the current consecutive subsequence length).</li></ul><p class="wp-block-paragraph">2. Loop through the array starting from the second element:</p><ul class="wp-block-list"><li>If the current element is equal to the previous one, skip it (handle duplicates).</li><li>Else, if the difference between the current and previous element is 1:<ul class="wp-block-list"><li>Increment <code>cont_sub_sequence</code> by 1.</li></ul></li><li>Otherwise:<ul class="wp-block-list"><li>Update <code>max_sequence</code> as the maximum of <code>max_sequence</code> and <code>cont_sub_sequence</code>.</li><li>Reset <code>cont_sub_sequence</code> to 1.</li></ul></li></ul><p class="wp-block-paragraph">3. After the loop, update <code>max_sequence</code> one final time as the maximum of <code>max_sequence</code> and <code>cont_sub_sequence</code>.</p><p class="wp-block-paragraph">4. Return <code>max_sequence</code>.</p><p class="wp-block-paragraph"></p><pre class="wp-block-syntaxhighlighter-code">class Solution:        # arr[] : the input array        #Function to return length of longest subsequence of consecutive integers.    def longestConsecutive(self,arr):        #code here        arr.sort()        max_sequence = 1        cont_sub_sequence = 1        for itr in range(1, len(arr)):            if arr[itr] == arr[itr-1]:                continue            elif arr[itr] - arr[itr-1] == 1:                cont_sub_sequence += 1            else:                if cont_sub_sequence &gt; max_sequence:                    max_sequence = cont_sub_sequence                cont_sub_sequence = 1                if cont_sub_sequence &gt; max_sequence:            max_sequence = cont_sub_sequence        return max_sequence</pre><p class="wp-block-paragraph"></p><figure class="wp-block-image size-large"><img alt="" class="wp-image-2100" data-recalc-dims="1" decoding="async" height="1008" loading="lazy" src="https://i0.wp.com/parottasalna.com/wp-content/uploads/2024/12/screenshot-from-2024-12-31-22-03-44.png?resize=1920%2C1008&amp;ssl=1" width="1920"/></figure>


## Related Posts
- [[POTD #6 - Two Sum - Pair with Given Sum | Geeks For Geeks]]
- [[POTD #14 - Count Subarrays with given XOR  | Geeks For Geeks]]
- [[Python Generators – The Lazy Workers of Python]]
- [[Understanding Common Table Expressions (CTE) in SQL — Simplifying Complex Queries]]
- [[Redis Strings – The Building Blocks of Key Value Storage]]

