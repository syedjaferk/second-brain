---
layout: post
title: 'POTD #22 - Longest substring with distinct characters | Geeks For Geeks'
date: 2025-01-11 16:44:57+00:00
render_with_liquid: false
category: Algorithm
tags:
- Substring
- Distinct Characters
- Sliding Window
- GeeksForGeeks
---



<p class="wp-block-paragraph"></p><h2 class="wp-block-heading">Problem Statement</h2><blockquote class="wp-block-quote is-layout-flow wp-block-quote-is-layout-flow"><p class="wp-block-paragraph">Geeks For Geeks : <a href="https://www.geeksforgeeks.org/problems/longest-distinct-characters-in-string5848/1">https://www.geeksforgeeks.org/problems/longest-distinct-characters-in-string5848/1</a></p></blockquote><p class="wp-block-paragraph">Given a string <strong>s</strong>, find the length of the longest substring with all distinct characters. </p><p class="wp-block-paragraph"></p><pre class="wp-block-syntaxhighlighter-code">Input: s = "geeksforgeeks"Output: 7Explanation: "eksforg" is the longest substring with all distinct characters.</pre><p class="wp-block-paragraph"></p><pre class="wp-block-syntaxhighlighter-code">Input: s = "abcdefabcbb"Output: 6Explanation: The longest substring with all distinct characters is "abcdef", which has a length of 6.</pre><p class="wp-block-paragraph"></p><h2 class="wp-block-heading">My Approach – Sliding Window</h2><pre class="wp-block-syntaxhighlighter-code">class Solution:    def longestUniqueSubstr(self, s):        # code here        char_index = {}        max_length = 0        start = 0                for i, char in enumerate(s):            if char in char_index and char_index[char] &gt;= start:                start = char_index[char] + 1 #crux                        char_index[char] = i                        max_length = max(max_length, i - start + 1)                return max_length                </pre>


## Related Posts
- [[POTD #11 - Longest Consecutive Subsequence | Geeks For Geeks]]
- [[POTD #14 - Count Subarrays with given XOR  | Geeks For Geeks]]
- [[Learning Notes #22 - Claim Check Pattern | Cloud Pattern]]
- [[Redis Strings – The Building Blocks of Key Value Storage]]
- [[POTD #6 - Two Sum - Pair with Given Sum | Geeks For Geeks]]

