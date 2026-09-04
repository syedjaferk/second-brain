---
layout: post
title: Is 'Latest' Tag actually refers to the latest image in docker ?
date: 2024-06-09 12:46:08+00:00
render_with_liquid: false
category: Docker
tags:
- ImageTagging
- DevOps
- RegistryManagement
- ContainerDeployment
- Versioning
---



<p class="wp-block-paragraph"></p><p class="wp-block-paragraph">During feature development, we created a PR to be tested in DEV. The pipeline creates the image with my branch and push the image to the registry. Then it will be deploying the container to the DEV environment. But after successful deployment, i am not able to see my code changes. I tried re-deploying the image, but no use. My code changes aren’t showing up in the dev environment.</p><p class="wp-block-paragraph">Then i went through the build files (yaml files), then i saw they were tagging the image with ‘<em>latest</em>‘ in docker build. The image with tag ‘latest’ also present in registry. Then why this problem ?</p><p class="wp-block-paragraph">After going through internet i found,</p><p class="wp-block-paragraph">The ’<strong>latest</strong>’ tag does not actually mean latest, it doesn’t mean anything. Its just a tag. Some people expect that :latest always points to the most-recently-pushed version of an image. That’s not true. It’s just the tag which is applied to an image by default which does not have a tag. Those two commands will both result in a new image being created and tagged as :latest: </p><pre class="wp-block-syntaxhighlighter-code">docker build -t company/image_name . </pre><pre class="wp-block-syntaxhighlighter-code">docker build -t company/image_name:latest .</pre><p class="wp-block-paragraph"></p><p class="wp-block-paragraph">Above two commands will produce the same output.Latest is Not Dynamic. So many people are not realizing that :latest is not dynamic. If you push a new image with a tag which is neither empty nor ’latest’, :latest will not be affected or created.</p><ol class="wp-block-list"></ol><h3 class="wp-block-heading">Best Practices</h3><ol class="wp-block-list"><li>Tag images with defined version number, like <code>docker build -t company/image_name:1.0.0 .</code></li><li>You should avoid using the :latest tag when deploying containers in production, because this makes it hard to track which version of the image is running and hard to roll back.</li><li>If you’re working with an image which is tagged with “latest”, that’s all the information you have apart from the image ID. Operations like deploying a new version of your app, or rolling back are simply not possible, if you don’t have two distinctly tagged images which are stable.</li></ol>


## Related Posts
- [[Can we build image on the FLY and USE IT ?]]
- [[Antipatterns while using docker containers]]
- [[Docker Cookbook]]
- [[Learning Notes #67 - Build and Push to a Registry (Docker Hub) with GH-Actions]]
- [[💾 Redis Is Open Source Again - What that means ?]]

