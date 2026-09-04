---
layout: post
title: Can we build image on the FLY and USE IT ?
date: 2024-06-29 16:30:49+00:00
render_with_liquid: false
category: Docker
tags:
- Fly
- Image Management
- Security
---



<p class="wp-block-paragraph">This is somewhat similar to antipattern, but goes beyond just doing a git clone directly into an image. This involves cloning, building, and then running the newly created image without ever pushing the image to an intermediary Docker registry.</p><p class="wp-block-paragraph">This is an antipattern for several reasons. </p><p class="wp-block-paragraph">First off, pushing the image to a registry gives you a “backup” of the image. This confers several benefits, the most important of which is that you can easily do a “quick rollback” should your deployment fail. You simply pull that last functioning image and run that, then go fix the current deployment.</p><p class="wp-block-paragraph">Additionally, many current container registries also offer the benefit of scanning your images for potential vulnerabilities. The value of this cannot be overstated – scanning a container image for vulnerabilities helps keep your data and your users safe.</p><p class="wp-block-paragraph">Another reason to avoid this is because the newly created docker image has not been tested <em>at all</em>. You should always test your images before deploying them, especially to a production environment.</p>


## Related Posts
- [[Is 'Latest' Tag actually refers to the latest image in docker ?]]
- [[Docker Cookbook]]
- [[Learning Notes #67 - Build and Push to a Registry (Docker Hub) with GH-Actions]]
- [[Antipatterns while using docker containers]]
- [[Mastering Request Retrying in Python with Tenacity: A Developer's Journey]]

