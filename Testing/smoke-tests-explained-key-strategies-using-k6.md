---
layout: post
title: 'Smoke Tests Explained: Key Strategies Using K6'
date: 2025-02-16 07:12:52+00:00
render_with_liquid: false
category: Testing
tags:
- Smoke Testing
- K6
- Software Engineering
- Test Cases
---



<p class="wp-block-paragraph"></p><p class="wp-block-paragraph">In this blog, i jot down notes on what is smoke test, how it got its name, and how to approach the same in k6. </p><p class="wp-block-paragraph"></p><p class="wp-block-paragraph">The term <strong>smoke testing</strong> originates from <strong>hardware testing</strong>, where engineers would power on a circuit or device and check if smoke appeared. </p><figure class="wp-block-image aligncenter size-large is-resized"><img alt="" class="wp-image-3594" data-recalc-dims="1" decoding="async" height="849" loading="lazy" src="https://i0.wp.com/parottasalna.com/wp-content/uploads/2025/02/image-14.png?resize=1200%2C849&amp;ssl=1" style="width:485px;height:auto" width="1200"/></figure><p class="wp-block-paragraph">If smoke was detected, it indicated a fundamental issue, and further testing was halted. This concept was later adapted to software engineering.</p><p class="wp-block-paragraph"></p><h2 class="wp-block-heading has-large-font-size">What is Smoke Testing?</h2><p class="wp-block-paragraph">Smoke testing is a subset of test cases executed to verify that the major functionalities of an application work as expected. If a smoke test fails, the build is rejected, preventing further testing of a potentially unstable application. This test helps catch major defects early, saving time and effort.</p><h3 class="wp-block-heading has-medium-font-size">Key Characteristics</h3><ul class="wp-block-list"><li>Ensures that the application is <strong>not broken</strong> in major areas.</li><li>Runs <strong>quickly</strong> and is <strong>not exhaustive</strong>.</li><li>Usually <strong>automated</strong> as part of a CI/CD pipeline.</li></ul><p class="wp-block-paragraph"></p><h2 class="wp-block-heading has-large-font-size">Writing a Basic Smoke Test with K6</h2><p class="wp-block-paragraph">A basic smoke test using K6 typically checks API endpoints for HTTP 200 responses and acceptable response times.</p><pre class="wp-block-syntaxhighlighter-code">import http from 'k6/http';import { check } from 'k6';export let options = {    vus: 1, // 1 virtual user    iterations: 5, // Runs the test 5 times};export default function () {    let res = http.get('https://example.com/api/health');    check(res, {        'is status 200': (r) =&gt; r.status === 200,        'response time &lt; 500ms': (r) =&gt; r.timings.duration &lt; 500,    });}</pre><p class="wp-block-paragraph"></p><h2 class="wp-block-heading has-large-font-size">Advanced Smoke Test Example</h2><p class="wp-block-paragraph"></p><pre class="wp-block-syntaxhighlighter-code">import http from 'k6/http';import { check, sleep } from 'k6';export let options = {    vus: 2, // 2 virtual users    iterations: 10, // Runs the test 10 times};export default function () {    let res = http.get('https://example.com/api/login');    check(res, {        'status is 200': (r) =&gt; r.status === 200,        'response time &lt; 400ms': (r) =&gt; r.timings.duration &lt; 400,    });    sleep(1);}</pre><p class="wp-block-paragraph"></p><h2 class="wp-block-heading has-large-font-size">Running and Analyzing Results</h2><p class="wp-block-paragraph">Execute the test using</p><pre class="wp-block-syntaxhighlighter-code">k6 run smoke-test.js</pre><h3 class="wp-block-heading has-medium-font-size">Sample Output</h3><pre class="wp-block-syntaxhighlighter-code">checks...✔ is status 200✔ response time &lt; 500ms</pre><p class="wp-block-paragraph">If any of the checks fail, K6 will report an error, signaling an issue in the application.</p><p class="wp-block-paragraph"></p><p class="wp-block-paragraph">Smoke testing with K6 is an effective way to ensure that key functionalities in your application work as expected. By integrating it into your CI/CD pipeline, you can catch major defects early, improve application stability, and streamline your development workflow.</p>


## Related Posts
- [[Boost System Performance During Traffic Surges with Spike Testing]]
- [[How Stress Testing Can Make More Attractive Systems ?]]
- [[Python Generators – The Lazy Workers of Python]]
- [[Top Command in Linux: Tips for Effective Usage]]
- [[Achieving Better User Engaging via Realistic Load Testing in K6]]

