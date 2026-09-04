---
layout: post
title: 'Learning Notes #8 - SLI, SLA, SLO'
date: 2024-12-25 16:11:50+00:00
render_with_liquid: false
category: Tech Notes
tags:
- SLI
- SLO
- SLA
- Service Reliability
---



<p class="wp-block-paragraph"></p><p class="wp-block-paragraph">In this blog, i write about SLI, SLA, SLO . I got a refreshing session from a podcast <a href="https://open.spotify.com/episode/2Ags7x1WrxaFLRd3KBU50K?si=vbYtW_YVQpOi8HwT9AOM1g">https://open.spotify.com/episode/2Ags7x1WrxaFLRd3KBU50K?si=vbYtW_YVQpOi8HwT9AOM1g</a>. This blog is about that. </p><p class="wp-block-paragraph"></p><p class="wp-block-paragraph">In the world of service reliability and performance, the terms SLO, SLA, and SLI are often used interchangeably but have distinct meanings. This blog explains these terms in detail, their importance, and how they relate to each other with practical examples.</p><p class="wp-block-paragraph"></p><h3 class="wp-block-heading"><strong>1. What are SLIs, SLOs, and SLAs?</strong></h3><h4 class="wp-block-heading"><strong>Service Level Indicators (SLIs)</strong></h4><p class="wp-block-paragraph">An SLI is a metric that quantifies the level of service provided by a system. It measures specific aspects of performance or reliability, such as response time, uptime, or error rate.</p><p class="wp-block-paragraph"><strong>Example</strong>:</p><ul class="wp-block-list"><li>Percentage of successful HTTP requests over a time window.</li><li>Average latency of API responses.</li></ul><p class="wp-block-paragraph"></p><h4 class="wp-block-heading"><strong>Service Level Objectives (SLOs)</strong></h4><p class="wp-block-paragraph">An SLO is a target value or range for an SLI. It defines what “acceptable” performance or reliability looks like from the perspective of the service provider or user.</p><p class="wp-block-paragraph"><strong>Example</strong>:</p><ul class="wp-block-list"><li>“99.9% of HTTP requests must succeed within 500ms.”</li><li>“The application should have 99.95% uptime per quarter.”</li></ul><p class="wp-block-paragraph"></p><h4 class="wp-block-heading"><strong>Service Level Agreements (SLAs)</strong></h4><p class="wp-block-paragraph">An SLA is a formal contract between a service provider and a customer that specifies the agreed-upon SLOs and the consequences of failing to meet them, such as penalties or compensations.</p><p class="wp-block-paragraph"><strong>Example</strong>:</p><ul class="wp-block-list"><li>“If the uptime drops below 99.5% in a calendar month, the customer will receive a 10% credit on their monthly bill.”</li></ul><p class="wp-block-paragraph"></p><h3 class="wp-block-heading"><strong>2. Relationship Between SLIs, SLOs, and SLAs</strong></h3><ul class="wp-block-list"><li><strong>SLIs</strong> are the metrics measured.</li><li><strong>SLOs</strong> are the goals or benchmarks derived from SLIs.</li><li><strong>SLAs</strong> are agreements that formalize SLOs and include penalties or incentives.</li></ul><pre class="wp-block-syntaxhighlighter-code">SLI: Average latency of API requests.SLO: 95% of API requests should have latency under 200ms.SLA: If latency exceeds the SLO for two consecutive weeks, the provider will issue service credits.</pre><p class="wp-block-paragraph"></p><h3 class="wp-block-heading"><strong>3. Practical Examples</strong></h3><h4 class="wp-block-heading"><strong>Example 1: Web Hosting Service</strong></h4><ul class="wp-block-list"><li><strong>SLI</strong>: Percentage of time the website is available.</li><li><strong>SLO</strong>: The website must be available 99.9% of the time per month.</li><li><strong>SLA</strong>: If uptime falls below 99.9%, the customer will receive a refund of 20% of their monthly fee.</li></ul><h4 class="wp-block-heading"><strong>Example 2: Cloud Storage Service</strong></h4><ul class="wp-block-list"><li><strong>SLI</strong>: Time taken to retrieve a file from storage.</li><li><strong>SLO</strong>: 95% of retrieval requests must complete within 300ms.</li><li><strong>SLA</strong>: If retrieval times exceed 300ms for more than 5% of requests in a billing cycle, customers will get free additional storage for the next month.</li></ul><h4 class="wp-block-heading"><strong>Example 3: API Service</strong></h4><ul class="wp-block-list"><li><strong>SLI</strong>: Error rate of API responses.</li><li><strong>SLO</strong>: Error rate must be below 0.1% for all requests in a day.</li><li><strong>SLA</strong>: If the error rate exceeds 0.1% for more than three days in a row, the customer is entitled to a credit worth 5% of their monthly subscription fee.</li></ul>


## Related Posts
- [[Learning Notes #7 - AMQP Protocol and RabbitMQ | An Overview]]
- [[Learning Notes #58 - Command Query Responsibility Segregation - An Idea Overview]]
- [[Learning Notes #40 - SAGA Pattern | Cloud Patterns]]
- [[Top Command in Linux: Tips for Effective Usage]]
- [[Python Generators – The Lazy Workers of Python]]

