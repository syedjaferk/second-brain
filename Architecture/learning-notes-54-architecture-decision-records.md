---
layout: post
title: 'Learning Notes #54 - Architecture Decision Records'
date: 2025-01-14 02:35:39+00:00
render_with_liquid: false
category: Architecture
tags:
- ADR
- Decision Making
- Documentation
- Transparency
---



<p class="wp-block-paragraph"></p><p class="wp-block-paragraph">Last few days, i was learning on how to make a accountable decision on deciding technical stuffs. Then i came across ADR. So far i haven’t used or seen used by our team. I think this is a necessary step to be incorporated to make accountable decisions. In this blog i share details on ADR for my future reference. </p><p class="wp-block-paragraph"></p><h2 class="wp-block-heading">What is an ADR?</h2><p class="wp-block-paragraph">An <strong>Architectural Decision Record (ADR)</strong> is a concise document that captures a single architectural decision, its context, the reasoning behind it, and its consequences. ADRs help teams document, share, and revisit architectural choices, ensuring transparency and better collaboration.</p><p class="wp-block-paragraph"></p><h2 class="wp-block-heading">Why Use ADRs?</h2><ol class="wp-block-list" start="1"><li><strong>Documentation:</strong> ADRs serve as a historical record of why certain decisions were made.</li><li><strong>Collaboration:</strong> They promote better understanding across teams.</li><li><strong>Traceability:</strong> ADRs link architectural decisions to specific project requirements and constraints.</li><li><strong>Accountability:</strong> They clarify who made a decision and when.</li><li><strong>Change Management:</strong> ADRs help evaluate the impact of changes and facilitate discussions around reversals or updates.</li></ol><p class="wp-block-paragraph"></p><h2 class="wp-block-heading">ADR Structure</h2><p class="wp-block-paragraph">A typical ADR document follows a standard format. Here’s an example:</p><ol class="wp-block-list" start="1"><li><strong>Title:</strong> A clear and concise title describing the decision.</li><li><strong>Context:</strong> Background information explaining the problem or opportunity.</li><li><strong>Decision:</strong> A summary of the chosen solution.</li><li><strong>Consequences:</strong> The positive and negative outcomes of the decision.</li><li><strong>Status:</strong> Indicates whether the decision is proposed, accepted, superseded, or deprecated.</li></ol><p class="wp-block-paragraph"></p><h2 class="wp-block-heading">Example: </h2><p class="wp-block-paragraph">Optimistic locking on MongoDB <a href="https://docs.google.com/document/d/1olCbicQeQzYpCxB0ejPDtnri9rWb2Qhs9_JZuvANAxM/edit?usp=sharing">https://docs.google.com/document/d/1olCbicQeQzYpCxB0ejPDtnri9rWb2Qhs9_JZuvANAxM/edit?usp=sharing</a></p><p class="wp-block-paragraph"></p><h2 class="wp-block-heading">References</h2><ol class="wp-block-list"><li><a href="https://cognitect.com/blog/2011/11/15/documenting-architecture-decisions">https://cognitect.com/blog/2011/11/15/documenting-architecture-decisions</a></li><li><a href="https://www.infoq.com/podcasts/architecture-advice-process/">https://www.infoq.com/podcasts/architecture-advice-process/</a></li><li>Recommended: <a href="https://github.com/joelparkerhenderson/architecture-decision-record/tree/main">https://github.com/joelparkerhenderson/architecture-decision-record/tree/main</a></li><li></li></ol>


## Related Posts
- [[Learning Notes #58 - Command Query Responsibility Segregation - An Idea Overview]]
- [[Learning Notes #56 - Push vs Pull Architecture]]
- [[Learning Notes #46 - Expand Contract Pattern | Refactor Pattern]]
- [[Python Generators – The Lazy Workers of Python]]
- [[Learning Notes #37 - Orchestrator Pattern | Cloud Pattern]]

