---
layout: post
title: 'POTD #9 - Intersection of Two arrays with Duplicate Elements | Geeks For Geeks'
date: 2024-12-29 01:01:33+00:00
render_with_liquid: false
category: Algorithm
tags:
- Intersection
- Arrays
- Duplicates
- GeeksForGeeks
---



<p class="wp-block-paragraph"></p><h2 class="wp-block-heading">Problem Statement</h2><blockquote class="wp-block-quote is-layout-flow wp-block-quote-is-layout-flow"><p class="wp-block-paragraph">Geeks For Geeks – <a href="https://www.geeksforgeeks.org/problems/intersection-of-two-arrays-with-duplicate-elements/1">https://www.geeksforgeeks.org/problems/intersection-of-two-arrays-with-duplicate-elements/1</a></p></blockquote><p class="wp-block-paragraph">Given two integer arrays a[] and b[], you have to find the intersection of the two arrays. Intersection of two arrays is said to be elements that are common in both arrays. The intersection should not have duplicate elements and the result should contain items in any order.</p><p class="wp-block-paragraph">Note:The driver code will sort the resulting array in increasing order before printing</p><p class="wp-block-paragraph"></p><pre class="wp-block-syntaxhighlighter-code">Input: a[] = [1, 2, 1, 3, 1], b[] = [3, 1, 3, 4, 1]Output: [1, 3]Explanation: 1 and 3 are the only common elements and we need to print only one occurrence of common elements.</pre><p class="wp-block-paragraph"></p><pre class="wp-block-syntaxhighlighter-code">Input: a[] = [1, 1, 1], b[] = [1, 1, 1, 1, 1]Output: [1]Explanation: 1 is the only common element present in both the arrays.</pre><p class="wp-block-paragraph"></p><h2 class="wp-block-heading">My Approach</h2><ul class="wp-block-list"><li>Made an entry to a dict for all num present in a</li><li>While iterating b, if a num is present in the dict, then added it to the result set. </li><li>return the list of the result set.</li></ul><pre class="wp-block-syntaxhighlighter-code">class Solution:    def intersectionWithDuplicates(self, a, b):        # code here        result = set()        hash_set = {}        for item in a:            if hash_set.get(item) is None:                hash_set[item] = True                for item in b:            if hash_set.get(item):                result.add(item)                return list(result)</pre>


## Related Posts
- [[POTD #6 - Two Sum - Pair with Given Sum | Geeks For Geeks]]
- [[POTD #18 - Pair with given sum in a sorted array | Geeks For Geeks]]
- [[POTD #8 - Find All Triplets with Zero Sum | Geeks For Geeks]]
- [[POTD #17 - Sum Pair closest to target | Geeks For Geeks]]
- [[Docker Ep 9: The Building Blocks – Detailed Structure of a Dockerfile]]

