---
layout: post
title: COPY or ADD in DOCKERfile ?
date: 2024-06-17 06:26:32+00:00
render_with_liquid: false
category: DockerTips
tags:
- Dockerfile
- COPY
- ADD
---



<p class="wp-block-paragraph">While i was reading on the best practices of writing a Dockerfile, its mentioned that COPY is preferred than ADD.</p><p class="wp-block-paragraph">The <code>COPY</code> and <code>ADD</code> commands in Docker are both used to copy files or directories from the host machine to the Docker image. However, there are key differences between the two:</p><pre class="wp-block-syntaxhighlighter-code">COPY ./app /appADD http://github.com/syedjafer/file.txt /app/ADD archive.tar.gz /app/</pre><blockquote class="wp-block-quote is-layout-flow wp-block-quote-is-layout-flow"><p class="wp-block-paragraph"><em>Use of Local Files</em></p></blockquote><ul class="wp-block-list"><li>COPY: Primarily used for copying local files and directories from the host machine to the image. It is straightforward and is the recommended choice for simple file copying tasks.</li><li>ADD: Similar to <code>COPY</code>, but it also has additional features, such as the ability to copy remote URLs and extract compressed files. For eg; <code>ADD archive.tar.gz /app/</code> will extract the tar file and copy the same to /app folder.</li></ul><blockquote class="wp-block-quote is-layout-flow wp-block-quote-is-layout-flow"><p class="wp-block-paragraph"><em>URLs and Compression</em></p></blockquote><ul class="wp-block-list"><li>COPY: Only handles local files and directories.</li><li>ADD: Can fetch files from URLs and automatically extract compressed files (e.g., tar and zip) during the copy process. While this can be convenient, it also introduces complexity and potential security risks.</li></ul><p class="wp-block-paragraph">In order to avoid confusion of the working, <code>COPY</code> is preferred than <code>ADD</code>.</p>


## Related Posts
- [[Can we use PUT in place of IDEMPOTENT POST ?]]
- [[Learning Notes #59 - What is an Event ? Is this same as Task ?]]
- [[Python - Operators CondItionals and Input()]]
- [[💾 Redis Is Open Source Again - What that means ?]]
- [[Top Command in Linux: Tips for Effective Usage]]

