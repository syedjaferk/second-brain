---
layout: post
title: Docker Cookbook
date: 2024-06-20 11:40:49+00:00
render_with_liquid: false
category: Docker Commands
tags:
- Container Management
- Image Usage
- Logging
- Port Mapping
- Syntax Highlighting
---



<ul class="wp-block-list"><li>List all images ?</li></ul><ol class="wp-block-list"></ol><pre class="wp-block-syntaxhighlighter-code">docker images</pre><ul class="wp-block-list"><li>List all containers ?</li></ul><pre class="wp-block-syntaxhighlighter-code">docker container ls -a / docker ps -a</pre><ul class="wp-block-list"><li>List all containers belong to a particular image ?</li></ul><pre class="wp-block-syntaxhighlighter-code">docker ps --all --filter ancestor=&lt;image_name_or_id&gt;</pre><ul class="wp-block-list"><li>See all the envs passed to a container used during creating it. ?</li></ul><pre class="wp-block-syntaxhighlighter-code">docker container inspect &lt;container id&gt;</pre><ul class="wp-block-list"><li>Run the docker in detached mode</li></ul><pre class="wp-block-syntaxhighlighter-code">docker run -d</pre><ul class="wp-block-list"><li>Docker: publish port 5004 of container to 8000 of host</li></ul><pre class="wp-block-syntaxhighlighter-code">docker run -p 8000:5004 &lt;image&gt;</pre><ul class="wp-block-list"><li>See the logs of the docker when the docker runs in a detached mode ?</li></ul><pre class="wp-block-syntaxhighlighter-code">docker logs -f &lt;container-id&gt;</pre><ul class="wp-block-list"><li>Close the container by giving time to close all the operations inside it ?</li></ul><pre class="wp-block-syntaxhighlighter-code">docker stop &lt;container-id&gt;</pre><ul class="wp-block-list"><li>Kill all the container and all the operations inside the container ?</li></ul><pre class="wp-block-syntaxhighlighter-code">docker container kill &lt;container-id&gt;</pre><ul class="wp-block-list"><li>How do you see all the docker events happening in a system ?</li></ul><pre class="wp-block-syntaxhighlighter-code">docker system events</pre><ul class="wp-block-list"><li>See the statistics of a container</li></ul><pre class="wp-block-syntaxhighlighter-code">docker stats &lt;container-id&gt;</pre><ul class="wp-block-list"><li>How do you transmit stdin, stdout of the container to the terminal ?</li></ul><pre class="wp-block-syntaxhighlighter-code">docker attach &lt;container-id&gt;</pre><ul class="wp-block-list"><li>What to give as a additional parameter such that the previous step container is not stopped ?</li></ul><p class="wp-block-paragraph">If the container started with -d or -i then Ctrl C</p><p class="wp-block-paragraph">Dockerfile for a simple flask/python application ?</p><pre class="wp-block-syntaxhighlighter-code">FROM python:3.8-slim-buster WORKDIR /backend ARG URL ENV ENVIRONMENT=""COPY ./service/requirements.txt /backend/service/requirements.txt RUN pip install --no-cache-dir --upgrade -r /backend/service/requirements.txt COPY ./service /backend/serviceEXPOSE 8080CMD ["uvicorn", "service.app:app", "--host", "0.0.0.0", "--port", "8080"]</pre><ul class="wp-block-list"><li>Clean up</li></ul><pre class="wp-block-syntaxhighlighter-code">docker kill $(docker ps -q)docker rm $(docker ps -a -q)docker rmi $(docker images -q)</pre><ul class="wp-block-list"><li>Conditional Logic in Docker Build</li></ul><pre class="wp-block-syntaxhighlighter-code">FROM node:alpineRUN mkdir -p /usr/src/appWORKDIR /usr/src/appCOPY package.json /usr/src/app/RUN npm installCOPY . /usr/src/appENV PORT 3000ARG DOCKER_ENVENV NODE_ENV=${DOCKER_ENV}RUN if [ "$DOCKER_ENV" = "stag" ] ; then  echo   your NODE_ENV for stage is $NODE_ENV;  \else  echo your NODE_ENV for dev is $NODE_ENV; \fi</pre><ul class="wp-block-list"><li>when you build this Dockerfile with this command</li></ul><p class="wp-block-paragraph">docker build –build-arg DOCKER_ENV=stag -t test-node . You will see at layer</p><p class="wp-block-paragraph">—&gt; Running in a6231eca4d0b your NODE_ENV for stage is stag When you run this docker container and run this command your output will be</p><pre class="wp-block-syntaxhighlighter-code">/usr/src/app # echo $NODE_ENVstag</pre>


## Related Posts
- [[Python List : The Delivery Man's Busy Day]]
- [[Problem Statements : Git &amp; Github Session - St. Joseph's GDG Meeting]]
- [[Antipatterns while using docker containers]]
- [[Learning Notes #68 - Buildpacks and Dockerfile]]
- [[Learning Notes #67 - Build and Push to a Registry (Docker Hub) with GH-Actions]]

