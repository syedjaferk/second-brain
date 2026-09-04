---
layout: post
title: 'Learning Notes #69 - Getting Started with k6: Writing Your First Load Test'
date: 2025-02-05 15:38:01+00:00
render_with_liquid: false
category: Programming
tags:
- k6
- load-testing
- performance-testing
- web-applications
- open-source
---



<p class="wp-block-paragraph"></p><p class="wp-block-paragraph">Performance testing is a crucial part of ensuring the stability and scalability of web applications. k6 is a modern, open-source load testing tool that allows developers and testers to script and execute performance tests efficiently. In this blog, we’ll explore the basics of k6 and write a simple test script to get started.</p><p class="wp-block-paragraph"></p><h2 class="wp-block-heading">What is k6?</h2><p class="wp-block-paragraph">k6 is a load testing tool designed for developers. It is written in Go but uses JavaScript for scripting tests. Key features include,</p><ul class="wp-block-list"><li>High performance with minimal resource consumption</li><li>JavaScript-based scripting</li><li>CLI-based execution with detailed reporting</li><li>Integration with monitoring tools like Grafana and Prometheus</li></ul><p class="wp-block-paragraph"></p><h2 class="wp-block-heading">Installation</h2><p class="wp-block-paragraph">For installation check : <a href="https://grafana.com/docs/k6/latest/set-up/install-k6/">https://grafana.com/docs/k6/latest/set-up/install-k6/</a></p><p class="wp-block-paragraph"></p><h2 class="wp-block-heading">Writing a Basic k6 Test</h2><p class="wp-block-paragraph">A k6 test is written in JavaScript. Here’s a simple script to test an API endpoint, </p><pre class="wp-block-syntaxhighlighter-code">import http from 'k6/http';import { check, sleep } from 'k6';export let options = {  vus: 10, // Number of virtual users  duration: '10s', // Test duration};export default function () {  let res = http.get('https://api.restful-api.dev/objects');  check(res, {    'is status 200': (r) =&gt; r.status === 200,  });  sleep(1); // Simulate user wait time}</pre><p class="wp-block-paragraph"></p><h2 class="wp-block-heading">Running the Test</h2><p class="wp-block-paragraph">Save the script as <code>script.js</code> and execute the test using the following command, </p><pre class="wp-block-syntaxhighlighter-code">k6 run script.js</pre><p class="wp-block-paragraph"></p><h2 class="wp-block-heading">Understanding the Output</h2><figure class="wp-block-image size-large"><img alt="" class="wp-image-3269" data-recalc-dims="1" decoding="async" height="715" loading="lazy" src="https://i0.wp.com/parottasalna.com/wp-content/uploads/2025/02/1be64495-0836-4cde-8cc4-d2fc72456d1d.png?resize=1276%2C715&amp;ssl=1" width="1276"/></figure><p class="wp-block-paragraph"></p><p class="wp-block-paragraph">After running the test, k6 will provide a summary including</p><p class="wp-block-paragraph">1. <strong>HTTP requests</strong>: Total number of requests made during the test.</p><ol class="wp-block-list"></ol><p class="wp-block-paragraph">2. <strong>Response time metrics</strong>:</p><ul class="wp-block-list"><li><code>min</code>: The shortest response time recorded.</li></ul><ul class="wp-block-list"><li><code>max</code>: The longest response time recorded.</li></ul><ul class="wp-block-list"><li><code>avg</code>: The average response time of all requests.</li></ul><ul class="wp-block-list"><li><code>p(90)</code>, <code>p(95)</code>, <code>p(99)</code>: Percentile values indicating response time distribution.</li></ul><p class="wp-block-paragraph">3. <strong>Checks</strong>: Number of checks passed or failed, such as status code validation.</p><p class="wp-block-paragraph">4. <strong>Virtual users (VUs)</strong>:</p><ul class="wp-block-list"><li><code>vus_max</code>: The maximum number of virtual users active at any time.</li></ul><ul class="wp-block-list"><li><code>vus</code>: The current number of active virtual users.</li></ul><p class="wp-block-paragraph">5. <strong>Request Rate (RPS – Requests Per Second)</strong>: The number of requests handled per second.</p><p class="wp-block-paragraph">6. <strong>Failures</strong>: Number of errors or failed requests due to timeouts or HTTP status codes other than expected.</p><p class="wp-block-paragraph"></p><h2 class="wp-block-heading">Next Steps</h2><p class="wp-block-paragraph">Once you’ve successfully run your first k6 test, you can explore,</p><ul class="wp-block-list"><li>Load testing different APIs and endpoints</li><li>Running distributed tests</li><li>Exporting results to Grafana</li><li>Integrating k6 with CI/CD pipelines</li></ul><p class="wp-block-paragraph">k6 is a powerful tool that helps developers and QA engineers ensure their applications perform under load. Stay tuned for more in-depth tutorials on advanced k6 features!</p>


## Related Posts
- [[Learning Notes #73 - Awesome Tricks on K6]]
- [[Mastering VUs and Test Duration with K6]]
- [[Smoke Tests Explained: Key Strategies Using K6]]
- [[Locust EP 1 : Load Testing: Ensuring Application Reliability with Real-Time Examples and Metrics]]
- [[HAProxy Ep 6: Load Balancing With Least Connection]]

