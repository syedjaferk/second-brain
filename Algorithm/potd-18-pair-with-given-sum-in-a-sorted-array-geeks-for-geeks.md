---
layout: post
title: 'POTD #18 - Pair with given sum in a sorted array | Geeks For Geeks'
date: 2025-01-07 18:08:29+00:00
render_with_liquid: false
category: Algorithm
tags:
- GeeksForGeeks
- PairSum
- SortedArray
- PythonSolution
---



<p class="wp-block-paragraph"></p><h2 class="wp-block-heading">Problem Statement: </h2><blockquote class="wp-block-quote is-layout-flow wp-block-quote-is-layout-flow"><p class="wp-block-paragraph">Geeks For Geeks : <a href="https://www.geeksforgeeks.org/problems/pair-with-given-sum-in-a-sorted-array4940/1">https://www.geeksforgeeks.org/problems/pair-with-given-sum-in-a-sorted-array4940/1</a></p></blockquote><p class="wp-block-paragraph">You are given an integer <strong>target</strong> and an array <strong>arr[]</strong>. You have to find number of pairs in <strong>arr[]</strong> which sums up to <strong>target</strong>. It is given that the elements of the <strong>arr[]</strong> are in <strong>sorted </strong>order.<br/><strong>Note:</strong> pairs should have elements of distinct indexes. </p><p class="wp-block-paragraph"></p><pre class="wp-block-syntaxhighlighter-code">Input: arr[] = [-1, 1, 5, 5, 7], target = 6Output: 3Explanation: There are 3 pairs which sum up to 6 : {1, 5}, {1, 5} and {-1, 7}.</pre><p class="wp-block-paragraph"></p><pre class="wp-block-syntaxhighlighter-code">Input: arr[] = [1, 1, 1, 1], target = 2Output: 6Explanation: There are 6 pairs which sum up to 2 : {1, 1}, {1, 1}, {1, 1}, {1, 1}, {1, 1} and {1, 1}.</pre><p class="wp-block-paragraph"></p><pre class="wp-block-syntaxhighlighter-code">Input: arr[] = [-1, 10, 10, 12, 15], target = 125Output: 0Explanation: There is no such pair which sums up to 4.</pre><p class="wp-block-paragraph"></p><h2 class="wp-block-heading">My Approach</h2><ul class="wp-block-list"><li>Store the occurence</li><li>Iterate and update count. </li></ul><pre class="wp-block-syntaxhighlighter-code">class Solution:    def countPairs (self, arr, target) :         #Complete the function        n = len(arr)        hash_set = {}        count = 0                for itr in range(n):            if hash_set.get(arr[itr]) is None:                hash_set[arr[itr]] = [itr]            else:                hash_set[arr[itr]].append(itr)                for itr in range(n):            rem = target - arr[itr]            for index in hash_set.get(rem, []):                if index &gt; itr:                    count += 1                return count</pre>


## Related Posts
- [[POTD #7 - Count pairs with given sum | Geeks For Geeks]]
- [[POTD #15 - Count all triplets with given sum in sorted array | Geeks For Geeks]]
- [[POTD #16 - Count Pairs whose sum is less than target | Geeks For Geeks]]
- [[POTD #6 - Two Sum - Pair with Given Sum | Geeks For Geeks]]
- [[POTD #13 - Subarrays with sum K | Geeks For Geeks]]

