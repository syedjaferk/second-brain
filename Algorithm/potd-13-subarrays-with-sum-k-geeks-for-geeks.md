---
layout: post
title: 'POTD #13 - Subarrays with sum K | Geeks For Geeks'
date: 2025-01-02 17:11:33+00:00
render_with_liquid: false
category: Algorithm
tags:
- Subarray Sum
- Count Subarrays
- GeeksForGeeks
- Array Problems
- Python Solution
---



<p class="wp-block-paragraph"></p><h2 class="wp-block-heading">Problem Statement</h2><blockquote class="wp-block-quote is-layout-flow wp-block-quote-is-layout-flow"><p class="wp-block-paragraph">Geeks For Geeks: <a href="https://www.geeksforgeeks.org/problems/subarrays-with-sum-k/1">https://www.geeksforgeeks.org/problems/subarrays-with-sum-k/1</a></p></blockquote><p class="wp-block-paragraph">Given an unsorted array of integers, find the number of continuous subarrays having sum exactly equal to a given number <strong>k</strong>.</p><p class="wp-block-paragraph"></p><pre class="wp-block-syntaxhighlighter-code">Input: arr = [10, 2, -2, -20, 10], k = -10Output: 3Explaination: Subarrays: arr[0...3], arr[1...4], arr[3...4] have sum exactly equal to -10.</pre><p class="wp-block-paragraph"></p><p class="wp-block-paragraph"></p><pre class="wp-block-syntaxhighlighter-code">Input: arr = [9, 4, 20, 3, 10, 5], k = 33Output: 2Explaination: Subarrays: arr[0...2], arr[2...4] have sum exactly equal to 33.</pre><p class="wp-block-paragraph"></p><p class="wp-block-paragraph"></p><pre class="wp-block-syntaxhighlighter-code">Input: arr = [1, 3, 5], k = 0Output: 0Explaination: No subarray with 0 sum.</pre><p class="wp-block-paragraph"></p><h2 class="wp-block-heading">My Approach 1 (Brute Force)</h2><p class="wp-block-paragraph">Initially i tried to solve it via bruteforce, but got timedout. </p><figure class="wp-block-image size-large"><img alt="" class="wp-image-2195" data-recalc-dims="1" decoding="async" height="504" loading="lazy" src="https://i0.wp.com/parottasalna.com/wp-content/uploads/2025/01/image-20.png?resize=954%2C504&amp;ssl=1" width="954"/></figure><pre class="wp-block-syntaxhighlighter-code">class Solution:    def countSubarrays(self, arr, k):        # code here        continous_count = 0        total_length = len(arr)        for itr in range(total_length):            _sum = arr[itr]            # print("ITR", arr[itr])            for jtr in range(itr+1, total_length):                # print("JTR", arr[jtr])                if _sum + arr[jtr] == k:                    # print("SUM")                    continous_count += 1                _sum += arr[jtr]        return continous_count</pre><p class="wp-block-paragraph"></p><h2 class="wp-block-heading">My Approach 2 (Optimal)</h2><p class="wp-block-paragraph">After some time, searched for an approach, then came across <strong>prefix-sum</strong> . So tried to apply the same, </p><pre class="wp-block-syntaxhighlighter-code">class Solution:    def countSubarrays(self, arr, k):        n = len(arr)        pre_sum_map = {}        pre_sum = 0        cnt = 0            pre_sum_map[0] = 1        for i in range(n):            pre_sum += arr[i]            remove = pre_sum - k            cnt += pre_sum_map.get(remove, 0)            pre_sum_map[pre_sum] = pre_sum_map.get(pre_sum, 0) + 1            return cnt</pre><p class="wp-block-paragraph"></p><h2 class="wp-block-heading">Reference: </h2><ol class="wp-block-list"><li><a href="https://takeuforward.org/arrays/count-subarray-sum-equals-k/">https://takeuforward.org/arrays/count-subarray-sum-equals-k/</a></li><li><a href="https://www.youtube.com/watch?v=frf7qxiN2qU">https://www.youtube.com/watch?v=frf7qxiN2qU</a></li></ol><p class="wp-block-paragraph"></p>


## Related Posts
- [[POTD #14 - Count Subarrays with given XOR  | Geeks For Geeks]]
- [[POTD #18 - Pair with given sum in a sorted array | Geeks For Geeks]]
- [[POTD #6 - Two Sum - Pair with Given Sum | Geeks For Geeks]]
- [[POTD #16 - Count Pairs whose sum is less than target | Geeks For Geeks]]
- [[POTD #7 - Count pairs with given sum | Geeks For Geeks]]

