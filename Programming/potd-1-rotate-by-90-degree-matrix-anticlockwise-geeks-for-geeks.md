---
layout: post
title: 'POTD #1 Rotate by 90 degree - Matrix Anticlockwise | Geeks For Geeks'
date: 2024-12-21 07:13:19+00:00
render_with_liquid: false
category: Programming
tags:
- Matrix Rotation
- GeeksForGeeks
- Competitive Programming
- Python Solution
---



<p class="wp-block-paragraph"></p><p class="wp-block-paragraph">After a long time, i tried competitive programming. Seems i need to do it more. This is a geeks for geeks POTD (Problem of the day) problem. </p><p class="wp-block-paragraph"></p><p class="wp-block-paragraph">Link: <a href="https://www.geeksforgeeks.org/problems/rotate-by-90-degree-1587115621/1">https://www.geeksforgeeks.org/problems/rotate-by-90-degree-1587115621/1</a></p><p class="wp-block-paragraph">Given a square matrix <strong>mat</strong>[][] of size <strong>n x n</strong>. The task is to rotate it by<strong> 90 degrees</strong> in an<strong> anti-clockwise</strong> direction without using any extra space. </p><h3 class="wp-block-heading">Input: </h3><blockquote class="wp-block-quote is-layout-flow wp-block-quote-is-layout-flow"><pre class="wp-block-preformatted"><strong>Input</strong>: mat[][] = [[1, 2, 3],<br/>                [4, 5, 6]<br/>                [7, 8, 9]]<br/><strong>Output</strong>: Rotated Matrix:<br/>[3, 6, 9]<br/>[2, 5, 8]<br/>[1, 4, 7]<br/><br/></pre></blockquote><blockquote class="wp-block-quote is-layout-flow wp-block-quote-is-layout-flow"><pre class="wp-block-preformatted"><strong>Input</strong>: mat[][] = [[1, 2],                [3, 4]]<strong>Output</strong>: Rotated Matrix:[2, 4][1, 3]</pre></blockquote><p class="wp-block-paragraph"></p><h3 class="wp-block-heading">Solution</h3><p class="wp-block-paragraph">I tried to reverse the each row and found the transpose of the matrix. Since i am aware of transpose , i directly went to this approach. </p><pre class="wp-block-syntaxhighlighter-code">#User function Template for python3class Solution:        #Function to rotate matrix anticlockwise by 90 degrees.    def rotateby90(self, mat):         # code here        n = len(mat)                    # reversing        for row in mat:            i = 0            j = len(row) - 1            while i  &lt; j:                row[i], row[j] = row[j], row[i]                i += 1                j -= 1                                            # Performing Transpose        for i in range(n):            for j in range(i + 1, n):                mat[i][j], mat[j][i] = mat[j][i], mat[i][j]</pre><p class="wp-block-paragraph"></p><figure class="wp-block-image size-large"><img alt="" class="wp-image-1646" data-recalc-dims="1" decoding="async" height="407" loading="lazy" src="https://i0.wp.com/parottasalna.com/wp-content/uploads/2024/12/image.png?resize=682%2C407&amp;ssl=1" width="682"/></figure>


## Related Posts
- [[Python Generators – The Lazy Workers of Python]]
- [[POTD #6 - Two Sum - Pair with Given Sum | Geeks For Geeks]]
- [[POTD #4 - Search in a sorted Matrix | Geeks For Geeks]]
- [[POTD #11 - Longest Consecutive Subsequence | Geeks For Geeks]]
- [[📊 Learn PostgreSQL in Tamil: From Zero to 5★ on HackerRank in Just 10 Days]]

