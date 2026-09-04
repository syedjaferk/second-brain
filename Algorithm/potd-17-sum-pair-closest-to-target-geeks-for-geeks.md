---
layout: post
title: 'POTD #17 - Sum Pair closest to target | Geeks For Geeks'
date: 2025-01-06 17:36:31+00:00
render_with_liquid: false
category: Algorithm
tags:
- GeeksForGeeks
- ArrayProblem
- ClosestSumPair
---



<p class="wp-block-paragraph"></p><h2 class="wp-block-heading">Problem Statement</h2><blockquote class="wp-block-quote is-layout-flow wp-block-quote-is-layout-flow"><p class="wp-block-paragraph">Geeks For Geeks : <a href="https://www.geeksforgeeks.org/problems/pair-in-array-whose-sum-is-closest-to-x1124/1">https://www.geeksforgeeks.org/problems/pair-in-array-whose-sum-is-closest-to-x1124/1</a></p></blockquote><p class="wp-block-paragraph">Given an array <strong>arr[]</strong> and a number <strong>target</strong>, find a pair of elements (a, b) in <strong>arr[], </strong>where a&lt;=b whose sum is closest to <strong>target.</strong><br/><strong>Note: </strong>Return the pair in sorted order and if there are multiple such pairs return the pair with maximum absolute difference. If no such pair exists return an empty array.</p><p class="wp-block-paragraph"></p><pre class="wp-block-syntaxhighlighter-code">Input: arr[] = [10, 30, 20, 5], target = 25Output: [5, 20]Explanation: As 5 + 20 = 25 is closest to 25.</pre><p class="wp-block-paragraph"></p><pre class="wp-block-syntaxhighlighter-code">Input: arr[] = [5, 2, 7, 1, 4], target = 10Output: [2, 7]Explanation: As (4, 7) and (2, 7) both are closest to 10, but absolute difference of (2, 7) is 5 and (4, 7) is 3. Hence, [2, 7] has maximum absolute difference and closest to target. </pre><p class="wp-block-paragraph"></p><pre class="wp-block-syntaxhighlighter-code">Input: arr[] = [10], target = 10Output: []Explanation: As the input array has only 1 element, return an empty array.</pre><p class="wp-block-paragraph"></p><h2 class="wp-block-heading">My Approach</h2><h3 class="wp-block-heading">O(n2) Approach</h3><pre class="wp-block-syntaxhighlighter-code">#User function Template for python3class Solution:    def sumClosest(self, arr, target):        # code here        arr.sort()        n = len(arr)        left = 0        right = n - 1                pairs = []        diff_to_target = None        abs_diff_in_pairs = None                for itr in range(n):            for jtr in range(itr+1, n):                _sum = arr[itr] + arr[jtr]                diff = abs(target - (arr[itr] + arr[jtr]))                abs_diff = abs(arr[jtr] - arr[itr])                # print("diff to target", diff_to_target)                if diff_to_target is None or (diff &lt; diff_to_target) or (diff == diff_to_target and abs_diff &gt; abs_diff_in_pairs):                    diff_to_target = diff                    abs_diff_in_pairs = abs_diff                    pairs = [arr[itr], arr[jtr]]        #     if abs_diff_in_pairs and abs_diff_in_pairs &gt; abs(arr[-1] - arr[itr]) and diff_to_target != 0:        #         break        return pairs</pre><p class="wp-block-paragraph"></p><p class="wp-block-paragraph">But got timeout :). </p><figure class="wp-block-image size-large"><img alt="" class="wp-image-2471" data-recalc-dims="1" decoding="async" height="345" loading="lazy" src="https://i0.wp.com/parottasalna.com/wp-content/uploads/2025/01/image-62.png?resize=938%2C345&amp;ssl=1" width="938"/></figure><p class="wp-block-paragraph"></p><h2 class="wp-block-heading">Optimal Approach – Two Pointer</h2><pre class="wp-block-syntaxhighlighter-code">class Solution:    def sumClosest(self, arr, target):        # code here        arr.sort()        n = len(arr)        closest_diff = (2 * (10 ** 5)) + 1        result = []        left, right = 0, n - 1        while left &lt; right:            current_sum = arr[left] + arr[right]            current_diff = abs(target - current_sum)            if current_diff &lt; closest_diff:                closest_diff = current_diff                result = [arr[left], arr[right]]            elif current_diff == closest_diff:                if abs(arr[right] - arr[left]) &gt; abs(result[1] - result[0]):                    result = [arr[left], arr[right]]            if current_sum &lt; target:                left += 1            else:                right -= 1        return result</pre>


## Related Posts
- [[POTD #16 - Count Pairs whose sum is less than target | Geeks For Geeks]]
- [[POTD #6 - Two Sum - Pair with Given Sum | Geeks For Geeks]]
- [[POTD #18 - Pair with given sum in a sorted array | Geeks For Geeks]]
- [[POTD #7 - Count pairs with given sum | Geeks For Geeks]]
- [[POTD #11 - Longest Consecutive Subsequence | Geeks For Geeks]]

