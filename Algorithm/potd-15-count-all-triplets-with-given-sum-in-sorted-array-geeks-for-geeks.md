---
layout: post
title: 'POTD #15 - Count all triplets with given sum in sorted array | Geeks For Geeks'
date: 2025-01-04 18:14:42+00:00
render_with_liquid: false
category: Algorithm
tags:
- Count Triplets
- Sorted Array
- GeeksForGeeks
- PythonSolution
- Mathematics
---



<p class="wp-block-paragraph"></p><h2 class="wp-block-heading">Problem Statement</h2><blockquote class="wp-block-quote is-layout-flow wp-block-quote-is-layout-flow"><p class="wp-block-paragraph">Geeks For Geeks : <a href="https://www.geeksforgeeks.org/problems/count-all-triplets-with-given-sum-in-sorted-array/1">https://www.geeksforgeeks.org/problems/count-all-triplets-with-given-sum-in-sorted-array/1</a></p></blockquote><p class="wp-block-paragraph">Given a sorted array <strong>arr[]</strong> and a <strong>target</strong> value, the task is to count triplets <strong>(i, j, k)</strong> of valid indices, such that <strong>arr[i] + arr[j] + arr[k] = target</strong> and <strong>i &lt; j &lt; k</strong>.</p><p class="wp-block-paragraph"></p><pre class="wp-block-syntaxhighlighter-code">Input: arr[] = [-3, -1, -1, 0, 1, 2], target = -2Output: 4Explanation: Two triplets that add up to -2 are:arr[0] + arr[3] + arr[4] = (-3) + 0 + (1) = -2arr[0] + arr[1] + arr[5] = (-3) + (-1) + (2) = -2arr[0] + arr[2] + arr[5] = (-3) + (-1) + (2) = -2arr[1] + arr[2] + arr[3] = (-1) + (-1) + (0) = -2</pre><p class="wp-block-paragraph"></p><pre class="wp-block-syntaxhighlighter-code">Input: arr[] = [-2, 0, 1, 1, 5], target = 1Output: 0Explanation: There is no triplet whose sum is equal to 1. </pre><p class="wp-block-paragraph"></p><h2 class="wp-block-heading">My Approach:</h2><p class="wp-block-paragraph">Initially i tried to approach the problem, similar to <a href="https://parottasalna.com/2024/12/28/potd-8-find-all-triplets-with-zero-sum-geeks-for-geeks/">this</a>. All testcases but 1 passed. Initial time complexity is O(n3). Failed 6 times. </p><figure class="wp-block-image size-large"><img alt="" class="wp-image-2336" data-recalc-dims="1" decoding="async" height="356" loading="lazy" src="https://i0.wp.com/parottasalna.com/wp-content/uploads/2025/01/image-42.png?resize=928%2C356&amp;ssl=1" width="928"/></figure><pre class="wp-block-syntaxhighlighter-code">class Solution:    def countTriplets(self, arr, target):        hash_set = {}        total = len(arr)        cnt = 0                # Build the hash_set with indices for each value in arr        for i in range(total):            if arr[i] not in hash_set:                hash_set[arr[i]] = []            hash_set[arr[i]].append(i)                # Iterate through all pairs (itr, jtr)        for itr in range(total):            for jtr in range(itr + 1, total):                rem = target - arr[itr] - arr[jtr]                                # Check for remaining value in hash_set                if rem in hash_set:                    # Use binary search to count indices greater than jtr                    indices = hash_set[rem]                    low, high = 0, len(indices)                                        while low &lt; high:                        mid = (low + high) // 2                        if indices[mid] &gt; jtr:                            high = mid                        else:                            low = mid + 1                                        cnt += len(indices) - low        return cnt</pre><p class="wp-block-paragraph"></p><p class="wp-block-paragraph">Then after reading blogs, switched to Two Pointer method</p><pre class="wp-block-syntaxhighlighter-code">class Solution:    def countTriplets(self, arr, target):        n = len(arr)        res = 0         for i in range(n - 2):            left = i + 1            right = n - 1            while left &lt; right:                sum = arr[i] + arr[left] + arr[right]                    if sum &lt; target:                    left += 1                    elif sum &gt; target:                    right -= 1                    else:                    ele1 = arr[left]                    ele2 = arr[right]                    cnt1 = 0                    cnt2 = 0                        while left &lt;= right and arr[left] == ele1:                        left += 1                        cnt1 += 1                        while left &lt;= right and arr[right] == ele2:                        right -= 1                        cnt2 += 1                    if ele1 == ele2:                        res += (cnt1 * (cnt1 - 1)) // 2                    else:                        res += (cnt1 * cnt2)            return res</pre>


## Related Posts
- [[POTD #18 - Pair with given sum in a sorted array | Geeks For Geeks]]
- [[POTD #8 - Find All Triplets with Zero Sum | Geeks For Geeks]]
- [[POTD #16 - Count Pairs whose sum is less than target | Geeks For Geeks]]
- [[POTD #6 - Two Sum - Pair with Given Sum | Geeks For Geeks]]
- [[POTD #14 - Count Subarrays with given XOR  | Geeks For Geeks]]

