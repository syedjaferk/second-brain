---
layout: post
title: 'Learning Notes #61 - Undo a git pull'
date: 2025-01-18 16:04:28+00:00
render_with_liquid: false
category: Git
tags:
- Undo Pull
- Reflog
- Version Control
---



<p class="wp-block-paragraph"></p><p class="wp-block-paragraph">Today, i came across a <a href="https://adamj.eu/tech/2024/12/31/git-undo-pull-reflog/?ref=parottasalna">blog</a> on undo a <code>git pull</code>. In this blog, i have reiterated the blog in other words. </p><p class="wp-block-paragraph"></p><p class="wp-block-paragraph">Mistakes happen. You run a <code>git pull</code> and suddenly find your repository in a mess. Maybe conflicts arose, or perhaps the changes merged from the remote branch aren’t what you expected. </p><p class="wp-block-paragraph"></p><p class="wp-block-paragraph">Fortunately, Git’s reflog comes to the rescue, allowing you to undo a <code>git pull</code> and restore your repository to its previous state. Here’s how you can do it.</p><p class="wp-block-paragraph"></p><h2 class="wp-block-heading">Understanding Reflog</h2><p class="wp-block-paragraph"><br/>Reflog is a powerful feature in Git that logs every update made to the tips of your branches and references. Even actions like resets or rebases leave traces in the reflog. This makes it an invaluable tool for troubleshooting and recovering from mistakes.</p><p class="wp-block-paragraph"></p><p class="wp-block-paragraph">Whenever you perform a <code>git pull</code>, Git updates the branch pointer, and the reflog records this action. By examining the reflog, you can identify the exact state of your branch before the pull and revert to it if needed.</p><p class="wp-block-paragraph"></p><h2 class="wp-block-heading">Step By Step Guide to UNDO a git pull</h2><p class="wp-block-paragraph">1. <strong>Check Your Current State</strong> Ensure you’re aware of the current state of your branch. If you have uncommitted changes, stash or commit them to avoid losing any work.</p><pre class="wp-block-syntaxhighlighter-code">git stash# orgit add . &amp;&amp; git commit -m "Save changes before undoing pull"</pre><p class="wp-block-paragraph"></p><p class="wp-block-paragraph">2. <strong>Inspect the Reflog</strong> View the recent history of your branch using the reflog,</p><pre class="wp-block-syntaxhighlighter-code">git reflog</pre><p class="wp-block-paragraph">This command will display a list of recent actions, showing commit hashes and descriptions. For example, </p><pre class="wp-block-syntaxhighlighter-code">0a1b2c3 (HEAD -&gt; main) HEAD@{0}: pull origin main: Fast-forward4d5e6f7 HEAD@{1}: commit: Add new feature8g9h0i1 HEAD@{2}: checkout: moving from feature-branch to main</pre><p class="wp-block-paragraph"></p><p class="wp-block-paragraph">3. <strong>Identify the Pre-Pull Commit</strong> Locate the commit hash of your branch’s state before the pull. In the above example, it’s <code>4d5e6f7</code>, which corresponds to the commit made before the <code>git pull</code>.</p><p class="wp-block-paragraph"></p><p class="wp-block-paragraph">4. <strong>Reset to the Previous Commit</strong> Use the <code>git reset</code> command to move your branch back to its earlier state, </p><pre class="wp-block-syntaxhighlighter-code">git reset &lt;commit-hash&gt;</pre><p class="wp-block-paragraph">By default, it’s mixed so changes wont be removed but will be in staging. </p><p class="wp-block-paragraph"></p><p class="wp-block-paragraph">The next time a pull operation goes awry, don’t panic—let the reflog guide you back to safety!</p>


## Related Posts
- [[Git Reset - A tool to correct your (commited) mistakes.]]
- [[Learning Notes #46 - Expand Contract Pattern | Refactor Pattern]]
- [[Problem Statements : Git &amp; Github Session - St. Joseph's GDG Meeting]]
- [[Git Stash Explained: Save Your Work Efficiently]]
- [[Learning Notes #67 - Build and Push to a Registry (Docker Hub) with GH-Actions]]

