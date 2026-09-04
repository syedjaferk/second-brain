---
layout: post
title: Can we use PUT in place of IDEMPOTENT POST ?
date: 2024-06-16 05:59:59+00:00
render_with_liquid: false
category: API Design
tags:
- PUT Method
- POST Method
- Idempotent Requests
---



<p class="wp-block-paragraph">Consider we have created an idempotent post request. So now the functionalities of PUT and POST are similar. So is it okay to use PUT inplace for POST ?</p><p class="wp-block-paragraph">We should understand what PUT and POST from IETF documentation. </p><p class="wp-block-paragraph"><strong>PUT:</strong></p><p class="wp-block-paragraph"><a href="https://www.rfc-editor.org/rfc/rfc9110#section-9.3.3">https://www.rfc-editor.org/rfc/rfc9110#section-9.3.3</a></p><pre class="wp-block-preformatted">The PUT method requests that the state of the target resource be <strong>created or replaced</strong> with the state defined by the representation enclosed in the request message payload.<br/><br/><strong>POST:</strong><br/><br/><a href="https://www.rfc-editor.org/rfc/rfc9110#name-put">https://www.rfc-editor.org/rfc/rfc9110#name-put</a><br/><br/>The POST method requests that the target <strong>resource process</strong> the  representation enclosed in the request according to the resource's own specific semantics.  For example, POST is used for the following   functions (among others):<br/><br/>1. Providing a block of data, such as the fields entered into an HTML form, to a data-handling process.<br/>2. Posting a message to a bulletin board, newsgroup, mailing list, blog, or similar group of articles.<br/>3. <strong>Creating a new resource</strong> that has yet to be identified by the origin server.<br/>4. Appending data to a <strong>resource's existing</strong> representation(s).<br/></pre><p class="wp-block-paragraph">From the doc, we can see that <strong>both methods can create a resource</strong>, then what is the difference. </p><p class="wp-block-paragraph">Even though PUT can create a resource, PUT is an idempotent. Which means, even if you are sending the request 100 times it will return the same response. If the resource is not there it will create, if its there it will update. </p><p class="wp-block-paragraph">But in case of POST request, most of the time it will create a new resource and not idempotent. </p><p class="wp-block-paragraph">So if you are in a situation where to use an idempotent POST request then we can consider PUT. Not really 🙂</p><p class="wp-block-paragraph">As the doc says, </p><blockquote class="wp-block-quote is-layout-flow wp-block-quote-is-layout-flow"><pre class="wp-block-preformatted"> Proper interpretation of a PUT request presumes that the user agent<br/> knows which target resource is desired.  A service that selects a<br/> proper URI on behalf of the client, after receiving a state-changing<br/> request, SHOULD be implemented using the POST method rather than PUT.</pre></blockquote><p class="wp-block-paragraph">You can use PUT, only when</p><ol class="wp-block-list"><li>The endpoint is idempotent: so safe to redo the request over and over again;</li><li>The URI must be the address to the resource being updated.</li></ol><p class="wp-block-paragraph">If a post can create a resource then it should send 201 status code as a response. </p>


## Related Posts
- [[COPY or ADD in DOCKERfile ?]]
- [[Learning Notes #59 - What is an Event ? Is this same as Task ?]]
- [[💾 Redis Is Open Source Again - What that means ?]]
- [[Python - Operators CondItionals and Input()]]
- [[Postgres - Write-Ahead Logging (WAL) in PostgreSQL]]

