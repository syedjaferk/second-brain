---
layout: post
title: 'POTD #6 - Two Sum - Pair with Given Sum | Geeks For Geeks'
date: 2024-12-26 06:05:54+00:00
render_with_liquid: false
category: Algorithm
tags:
- Two Sum Problem
- Array Search
- GeeksForGeeks
---



<p class="wp-block-paragraph"></p><h2 class="wp-block-heading">Problem Statement</h2><blockquote class="wp-block-quote is-layout-flow wp-block-quote-is-layout-flow"><p class="wp-block-paragraph">Geeks For Geeks : <a href="https://www.geeksforgeeks.org/problems/key-pair5616/1">https://www.geeksforgeeks.org/problems/key-pair5616/1</a></p></blockquote><p class="wp-block-paragraph">Given an array <strong>arr[]</strong> of positive integers and another integer <strong>target</strong>. Determine if there exists two distinct indices such that the sum of there elements is equals to <strong>target.</strong><br/></p><h2 class="wp-block-heading">Examples</h2><pre class="wp-block-syntaxhighlighter-code">Input: arr[] = [1, 4, 45, 6, 10, 8], target = 16Output: trueExplanation: arr[3] + arr[4] = 6 + 10 = 16.</pre><p class="wp-block-paragraph"></p><pre class="wp-block-syntaxhighlighter-code">Input: arr[] = [1, 2, 4, 3, 6], target = 11Output: falseExplanation: None of the pair makes a sum of 11.</pre><p class="wp-block-paragraph"></p><h2 class="wp-block-heading">My Approach</h2><ul class="wp-block-list"><li>Iterate through the array</li><li>For each element, check whether the remaining (target – element) is also present in the array using the supportive hashmap. </li><li>If the remaining is also present then return True.</li><li>Else, save the element in the hashmap and go to the next element. </li></ul><pre class="wp-block-syntaxhighlighter-code">#User function Template for python3class Solution:	def twoSum(self, arr, target):		# code here		maps = {}		for item in arr:		    rem = target - item		    if maps.get(rem):		        return True		    maps[item] = True		return False		</pre><p class="wp-block-paragraph"></p><figure class="wp-block-image size-large"><img alt="" class="wp-image-1819" data-recalc-dims="1" decoding="async" height="1011" loading="lazy" src="https://i0.wp.com/parottasalna.com/wp-content/uploads/2024/12/screenshot-from-2024-12-26-11-26-09.png?resize=1909%2C1011&amp;ssl=1" width="1909"/></figure>


## Related Posts
- [[POTD #11 - Longest Consecutive Subsequence | Geeks For Geeks]]
- [[POTD #14 - Count Subarrays with given XOR  | Geeks For Geeks]]
- [[POTD #16 - Count Pairs whose sum is less than target | Geeks For Geeks]]
- [[Python Generators – The Lazy Workers of Python]]
- [[POTD #8 - Find All Triplets with Zero Sum | Geeks For Geeks]]

