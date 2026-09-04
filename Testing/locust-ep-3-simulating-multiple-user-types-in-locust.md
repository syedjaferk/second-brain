---
layout: post
title: 'Locust EP 3: Simulating Multiple User Types in Locust'
date: 2024-11-18 04:30:00+00:00
render_with_liquid: false
category: Testing
tags:
- Locust
- Load Testing
- User Simulation
- Performance Analysis
- Web Applications
---



<p class="wp-block-paragraph">Locust allows you to define multiple user types in your load tests, enabling you to simulate different user behaviors and traffic patterns. This is particularly useful when your application serves diverse client types, such as web and mobile users, each with unique interaction patterns.</p><p class="wp-block-paragraph">In this blog, we will</p><ol class="wp-block-list"><li>Discuss the concept of multiple user types in Locust.</li><li>Explore how to implement multiple user classes with weights.</li><li>Run and analyze the test results.</li></ol><h3 class="wp-block-heading">Why Use Multiple User Types?</h3><p class="wp-block-paragraph">In real-world applications, different user groups interact with your system differently. For example,</p><ul class="wp-block-list"><li><strong>Web Users</strong> might spend more time browsing through the UI.</li><li><strong>Mobile Users</strong> could make faster but more frequent requests.</li></ul><p class="wp-block-paragraph">By simulating distinct user types with varying behaviors, you can identify performance bottlenecks across all client groups.</p><h3 class="wp-block-heading">Understanding User Classes and Weights</h3><p class="wp-block-paragraph">Locust provides the ability to define user classes by extending the <code>User</code> or <code>HttpUser</code> base class. Each user class can,</p><ul class="wp-block-list"><li>Have a unique set of tasks.</li><li>Define its own wait times.</li><li>Be assigned a <strong>weight</strong>, which determines the proportion of that user type in the simulation.</li></ul><p class="wp-block-paragraph">For example, if <code>WebUser</code> has a weight of 1 and <code>MobileUser</code> has a weight of 2, the simulation will spawn 1 web user for every 2 mobile users.</p><h3 class="wp-block-heading">Example: Simulating Web and Mobile Users</h3><p class="wp-block-paragraph">Below is an example Locust test with two user types</p><pre class="wp-block-syntaxhighlighter-code">from locust import User, task, between# Define a user class for web usersclass MyWebUser(User):    wait_time = between(1, 3)  # Web users wait between 1 and 3 seconds between tasks    weight = 1  # Web users are less frequent    @task    def login_url(self):        print("I am logging in as a Web User")# Define a user class for mobile usersclass MyMobileUser(User):    wait_time = between(1, 3)  # Mobile users wait between 1 and 3 seconds    weight = 2  # Mobile users are more frequent    @task    def login_url(self):        print("I am logging in as a Mobile User")</pre><h3 class="wp-block-heading">How Locust Uses Weights</h3><p class="wp-block-paragraph">With the above configuration</p><ul class="wp-block-list"><li>For every 3 users spawned, <strong>1 will be a Web User</strong>, and <strong>2 will be Mobile Users</strong> (based on their weights: 1 and 2).</li></ul><p class="wp-block-paragraph">Locust automatically handles spawning these users in the specified ratio.</p><h3 class="wp-block-heading">Running the Locust Test</h3><ol class="wp-block-list"><li><strong>Save the Code</strong><br/>Save the above code in a file named <code>locustfile.py</code>.</li><li><strong>Start Locust</strong><br/>Open your terminal and run `<code>locust -f locustfile.py</code>`</li><li><strong>Access the Web UI</strong><ul class="wp-block-list"><li>Open your browser and go to <a data-proofer-ignore="" href="#">http://localhost:8089</a>.</li></ul></li><li><strong>Enter Test Parameters</strong><ul class="wp-block-list"><li>Number of users (e.g., 30).</li><li>Spawn rate (e.g., 5 users per second).</li><li><strong>Host</strong>: If you are testing an actual API or website, specify its URL (e.g., <code>http://localhost:8000</code>).</li></ul></li><li><strong>Analyze Results</strong><ul class="wp-block-list"><li>Observe how Locust spawns the users according to their weights and tracks metrics like request counts and response times.</li></ul></li></ol><p class="wp-block-paragraph"></p><p class="wp-block-paragraph">After running the test:</p><ul class="wp-block-list"><li>Check the <strong>distribution of requests</strong> to ensure it matches the weight ratio (e.g., for every 1 web user request, there should be ~3 mobile user requests).</li><li>Use the metrics (response time, failure rate) to evaluate performance for each user type.</li></ul><p class="wp-block-paragraph"></p>


## Related Posts
- [[HAProxy EP 3: Sarah’s Adventure with L7 Load Balancing and HAProxy]]
- [[Locust EP 1 : Load Testing: Ensuring Application Reliability with Real-Time Examples and Metrics]]
- [[Locust EP 2: Understanding Locust Wait Times with Complete Examples]]
- [[Achieving Better User Engaging via Realistic Load Testing in K6]]
- [[HAProxy EP 7: Load Balancing with Source IP Hash, URI - Consistent Hashing]]

