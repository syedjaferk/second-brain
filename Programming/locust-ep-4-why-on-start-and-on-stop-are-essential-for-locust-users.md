---
layout: post
title: 'Locust ep 4: Why on_start and on_stop are Essential for Locust Users'
date: 2024-11-19 04:30:00+00:00
render_with_liquid: false
category: Programming
tags:
- Locust
- Testing
- Automation
- Python
---



<p class="wp-block-paragraph">Locust provides two special methods, <code>on_start</code> and <code>on_stop</code>, to handle setup and teardown actions for individual users. These methods allow you to execute specific code when a simulated user starts or stops, making it easier to simulate real-world scenarios like login/logout or initialization tasks.</p><p class="wp-block-paragraph">In this blog, we’ll cover,</p><ol class="wp-block-list"><li>What <code>on_start</code> and <code>on_stop</code> do.</li><li>Why they are important.</li><li>Practical examples of using these methods.</li><li>Running and testing Locust scripts.</li></ol><h3 class="wp-block-heading">What Are <code>on_start</code> and <code>on_stop</code>?</h3><ul class="wp-block-list"><li><strong><code>on_start</code></strong>: This method is executed once when a new simulated user starts. It’s commonly used for tasks like logging in or setting up the environment.</li><li><strong><code>on_stop</code></strong>: This method is executed once when a simulated user stops. It’s often used for cleanup tasks like logging out.</li></ul><p class="wp-block-paragraph">These methods are executed <em>only once per user</em> during the lifecycle of a test, as opposed to tasks that are run repeatedly.</p><h3 class="wp-block-heading">Why Use <code>on_start</code> and <code>on_stop</code>?</h3><ol class="wp-block-list"><li><strong>Simulating Real User Behavior</strong>: Real users often start a session with an action (e.g., login) and end it with another (e.g., logout).</li><li><strong>Initial Setup</strong>: Some tasks require initializing data or setting up user state before performing other actions.</li><li><strong>Cleanup</strong>: Ensure that actions like logout are performed to leave the system in a clean state.</li></ol><h3 class="wp-block-heading">Examples</h3><h4 class="wp-block-heading">Basic Usage of <code>on_start</code> and <code>on_stop</code></h4><p class="wp-block-paragraph">In this example, we just print <code>on start and </code>`on stop` for each user while running a task. </p><pre class="wp-block-syntaxhighlighter-code">from locust import User, task, between, constant, constant_pacingfrom datetime import datetimeclass MyUser(User):    wait_time = between(1, 5)    def on_start(self):        print("on start")    def on_stop(self):        print("on stop")    @task    def print_datetime(self):        print(datetime.now())</pre>


## Related Posts
- [[Locust ep 5: How to use test_start and test_stop Events in Locust]]
- [[Top Command in Linux: Tips for Effective Usage]]
- [[Locust EP 2: Understanding Locust Wait Times with Complete Examples]]
- [[Git Stash Explained: Save Your Work Efficiently]]
- [[Learning Notes #23 - Retry Pattern | Cloud Patterns]]

