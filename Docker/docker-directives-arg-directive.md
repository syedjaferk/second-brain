---
layout: post
title: Docker Directives - ARG Directive
date: 2024-07-10 01:39:12+00:00
render_with_liquid: false
category: DockerTips
tags:
- ARGDirective
- Dockerfile
- BuildTimeVariables
---



<p class="wp-block-paragraph">The <strong>ARG</strong> directive in a Dockerfile is used to define variables that users can pass at build time to the builder with the <code>docker build</code> command. </p><p class="wp-block-paragraph">These variables behave similarly to environment variables and can be used throughout the Dockerfile but are not persisted in the final image unless explicitly declared using the <strong>ENV</strong> directive.</p><p class="wp-block-paragraph">The <strong>ARG</strong> directive has the following format:</p><pre class="wp-block-syntaxhighlighter-code">ARG &lt;varname&gt;</pre><p class="wp-block-paragraph">We can also add multiple <strong>ARG</strong> directives, as follows:</p><pre class="wp-block-syntaxhighlighter-code">ARG USERARG VERSION</pre><p class="wp-block-paragraph">These arguments can also have optional default values specified within the Dockerfile itself.</p><p class="wp-block-paragraph">If no value is provided by the user during the build process, Docker uses the default value defined in the <strong>ARG</strong> instruction:</p><pre class="wp-block-syntaxhighlighter-code">ARG USER=TestUserARG VERSION=1.0.0</pre><p class="wp-block-paragraph">Unlike the <strong>ENV</strong> variables, <strong>ARG</strong> variables are not accessible from the running container. They are only available during the build process.</p><p class="wp-block-paragraph"></p>


## Related Posts
- [[Docker Directives - Env Directive]]
- [[Effortless Data Storage with LocalBase and IndexedDB]]
- [[Top Command in Linux: Tips for Effective Usage]]
- [[Redis Strings – The Building Blocks of Key Value Storage]]
- [[Python Generators – The Lazy Workers of Python]]

