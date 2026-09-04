---
layout: post
title: 'POTD #5 - Set Matrix Zeroes | Geeks For Geeks'
date: 2024-12-25 06:20:26+00:00
render_with_liquid: false
category: Algorithm
tags:
- Matrix
- Zeroes
- GeeksForGeeks
- ConstantSpace
---



<p class="wp-block-paragraph"></p><h3 class="wp-block-heading">Problem Statement</h3><blockquote class="wp-block-quote is-layout-flow wp-block-quote-is-layout-flow"><p class="wp-block-paragraph">Geeks For Geeks : <a href="https://www.geeksforgeeks.org/problems/set-matrix-zeroes/1">https://www.geeksforgeeks.org/problems/set-matrix-zeroes/1</a></p></blockquote><p class="wp-block-paragraph">You are given a 2D matrix <strong>mat</strong>[][] of size <strong>n×m</strong>. The task is to modify the matrix such that if <strong>mat[i][j]</strong> is 0, all the elements in the <strong>i</strong>-th row and <strong>j</strong>-th column are set to 0 and do it in <strong>constant space complexity</strong>.</p><p class="wp-block-paragraph"></p><pre class="wp-block-syntaxhighlighter-code">Input: mat[][] = [[1, -1, 1],                [-1, 0, 1],                [1, -1, 1]]Output: [[1, 0, 1],        [0, 0, 0],        [1, 0, 1]]Explanation: mat[1][1] = 0, so all elements in row 1 and column 1 are updated to zeroes.</pre><p class="wp-block-paragraph"></p><pre class="wp-block-syntaxhighlighter-code">Input: mat[][] = [[0, 1, 2, 0],                [3, 4, 5, 2],                [1, 3, 1, 5]]Output: [[0, 0, 0, 0],        [0, 4, 5, 0],        [0, 3, 1, 0]]Explanation: mat[0][0] and mat[0][3] are 0s, so all elements in row 0, column 0 and column 3 are updated to zeroes.</pre><p class="wp-block-paragraph"></p><h3 class="wp-block-heading">My Approach</h3><ol class="wp-block-list"><li>Iterate through the matrix and check whether mat[i][j] is zero. If its zero then row i and col j need to made as zeros. </li><li>Collect them in a set</li><li>Finally iterate through the set and update the matrix. </li></ol><pre class="wp-block-syntaxhighlighter-code">#User function Template for python3class Solution:            def setMatrixZeroes(self, mat):        rows_to_zeros = set()        cols_to_zeros = set()                rows = len(mat)        cols = len(mat[0])                for i in range(rows):            for j in range(cols):                if mat[i][j] == 0:                    rows_to_zeros.add(i)                    cols_to_zeros.add(j)                for row in rows_to_zeros:            for itr in range(cols):                mat[row][itr] = 0                        for col in cols_to_zeros:            for itr in range(rows):                mat[itr][col] = 0                       return mat</pre><p class="wp-block-paragraph"></p><figure class="wp-block-image size-large"><img alt="" class="wp-image-1781" data-recalc-dims="1" decoding="async" height="1012" loading="lazy" src="https://i0.wp.com/parottasalna.com/wp-content/uploads/2024/12/screenshot-from-2024-12-25-11-40-29.png?resize=1920%2C1012&amp;ssl=1" width="1920"/></figure>


## Related Posts
- [[POTD #6 - Two Sum - Pair with Given Sum | Geeks For Geeks]]
- [[POTD #4 - Search in a sorted Matrix | Geeks For Geeks]]
- [[POTD #3 Search in a row-wise sorted matrix | Geeks For Geeks]]
- [[POTD #1 Rotate by 90 degree - Matrix Anticlockwise | Geeks For Geeks]]
- [[Learning Notes #5 - Message Queues | RabbitMQ]]

