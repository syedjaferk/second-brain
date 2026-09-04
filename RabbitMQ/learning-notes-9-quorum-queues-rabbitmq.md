---
layout: post
title: 'Learning Notes #9 - Quorum Queues | RabbitMQ'
date: 2024-12-25 16:42:22+00:00
render_with_liquid: false
category: RabbitMQ
tags:
- Quorum Queues
- Raft Consensus
- Message Queue
- High Availability
---



<p class="wp-block-paragraph"></p><h2 class="wp-block-heading"><strong>What Are Quorum Queues?</strong></h2><ul class="wp-block-list"><li>Quorum Queues are <strong>distributed queues</strong> built on the Raft consensus algorithm.</li><li>They are designed for <strong>high availability</strong>, <strong>durability</strong>, and <strong>data safety</strong> by replicating messages across multiple nodes in a RabbitMQ cluster.</li><li>Its a replacement of Mirrored Queues.</li></ul><p class="wp-block-paragraph"></p><h2 class="wp-block-heading"><strong>Key Characteristics</strong></h2><ol class="wp-block-list"><li><strong>Replication</strong>:<ul class="wp-block-list"><li>Messages are replicated across a quorum (a majority of nodes).</li><li>A quorum consists of an <strong>odd number of replicas</strong> (e.g., 3, 5, 7) to ensure a majority can elect a leader during failovers.</li></ul></li><li><strong>Leader-Follower Architecture</strong>:<ul class="wp-block-list"><li>Each Quorum Queue has one <strong>leader</strong> and multiple <strong>followers</strong>.</li><li>The leader handles all write and read operations, while followers replicate messages and provide redundancy.</li></ul></li><li><strong>Durability</strong>:<ul class="wp-block-list"><li>Messages are written to disk on all quorum nodes, ensuring persistence even if nodes fail.</li></ul></li><li><strong>High Availability</strong>:<ul class="wp-block-list"><li>If the leader node fails, RabbitMQ elects a new leader from the remaining quorum, ensuring continued operation.</li></ul></li><li><strong>Consistency</strong>:<ul class="wp-block-list"><li>Quorum Queues prioritize <strong>consistency over availability</strong>.</li><li>Messages are acknowledged only after replication is successful on a majority of nodes.</li></ul></li><li><strong>Message Ordering</strong>:<ul class="wp-block-list"><li>Message ordering is preserved during normal operations but may be disrupted during leader failovers.</li></ul></li></ol><p class="wp-block-paragraph"></p><p class="wp-block-paragraph"></p><h2 class="wp-block-heading"><strong>Use Cases</strong></h2><ul class="wp-block-list"><li><strong>Mission-Critical Applications</strong> – Systems where message loss is unacceptable (e.g., financial transactions, order processing).</li><li><strong>Distributed Systems</strong> – Environments requiring high availability and fault tolerance.</li><li><strong>Data Safety</strong> – Applications prioritizing consistency over throughput (e.g., event logs, audit trails).</li></ul><p class="wp-block-paragraph"></p><h2 class="wp-block-heading">Setups</h2><h3 class="wp-block-heading">Using rabbitmqctl</h3><pre class="wp-block-syntaxhighlighter-code">rabbitmqctl add_queue quorum_queue --type quorum</pre><p class="wp-block-paragraph"></p><h3 class="wp-block-heading">Using python</h3><pre class="wp-block-syntaxhighlighter-code">channel.queue_declare(queue="quorum_queue", arguments={"x-queue-type": "quorum"})</pre><p class="wp-block-paragraph"></p><p class="wp-block-paragraph"></p><h2 class="wp-block-heading">References:</h2><ol class="wp-block-list"><li><a href="https://www.rabbitmq.com/docs/quorum-queues">https://www.rabbitmq.com/docs/quorum-queues</a></li><li></li></ol>


## Related Posts
- [[Learning Notes #7 - AMQP Protocol and RabbitMQ | An Overview]]
- [[Python Generators – The Lazy Workers of Python]]
- [[Learning Notes #36 - Active Active / Active Passive Patterns | HA Patterns]]
- [[Learning Notes #10 - Lazy Queues | RabbitMQ]]
- [[HAProxy EP 9: Load Balancing with Weighted Round Robin]]

